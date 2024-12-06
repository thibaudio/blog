---
title: "Skaffold with ECR and replication"
date: 2022-07-18T17:17:35+02:00
draft: false
toc: false
images:
tags:
---

Our product is deployed on kubernetes, and the dev team was working locally; which meant a lot of integration issues.  
We decided to try skaffold for continuous development and deployment.

## Login to ECR automatically with skaffold
We use private ECR as artifacts repositories, so we need to log in before being able to push.  

One solution we found is to create a simple script to perform a `docker login`:  
```sh
tmp=${SKAFFOLD_IMAGE_REPO#*ecr.}
REGION=${tmp%.amazonaws*}	
aws ecr get-login-password --region $REGION | docker login --username AWS --password-stdin $SKAFFOLD_IMAGE_REPO
```

And having this script be called by skaffold before every push:
```yaml
.docker_login: &docker_login
  - command: ["sh", "-c", "./docker-login.sh"]
    os: [darwin, linux]
apiVersion: skaffold/v2beta28
kind: Config
build:
  artifacts:
    - image: my-image
      hooks:
        before: *docker_login
```

## Production pipeline gotchas
This is working fine in a development environment, a quick `skaffold dev` and everything is built, deployed and watched.  
But we faced several issues when integrating skaffold with our CD pipeline.  

### Docker login in the pre-deploy hook
One thing we didn't see was that `$SKAFFOLD_IMAGE_REPO` is not available in skaffold deploy hooks, only build hooks.
We updated our docker-login script to use `$SKAFFOLD_DEFAULT_REPO` instead, but we found out that it was not made available by `skaffold config set default-repo`, only when exporting the environment variable.

### artifacts.json
We have multiple EKS clusters spread around the world and, to speed-up pod boot time, we use a regional registry for each cluster.  
We have replication enabled, so we only need to push to the main registry, but each cluster is pulling from a different one.

{{< figure src="/svgs/replication.svg" alt="Hello Friend" position="center" style="border-radius: 8px;" >}}

When building with `skaffold build --file-output artifacts.json`, artifacts are referenced with their full path:
```json
{
  "builds": [
    {
      "imageName": "my-image",
      "tag": "some-account.dkr.ecr.some-region.amazonaws.com/my-image:my-tag@sha256:meow"
    }
  ]
}
```
Even with a default repository set, `skaffold deploy -a artifacts.json` don't rewrite the path of the images... but, as we just saw, we are using a different one for each cluster!  
  
Our quick solution was to build a small wrapper for our build process, which remove the registry from the image path:
```sh
echo $(skaffold build -q $@ | jq '.builds[].tag |=(sub("^.+/"; ""))') > "artifacts.json"
```

Now the images in our `artifacts.json` file are referenced only by their names, and skaffold deploy prepend the default repository as expected:  
```json
{
  "builds": [
    {
      "imageName": "my-image",
      "tag": "my-image:my-tag@sha256:meow"
    }
  ]
}
```

