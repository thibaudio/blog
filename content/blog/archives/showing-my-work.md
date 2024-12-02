---
title: "Showing My Work"
date: 2022-07-15T13:21:25+02:00
draft: false
toc: false
images:
tags:
---

I've just finish reading the book *[Show your work!](https://austinkleon.com/show-your-work/)* by [Austin Kleon](https://austinkleon.com/), and it gave me the push I needed to start my little place online.
I'm planning to share here some of my work around site reliability engineering and game development. Wish me luck!

But first, let's talk about the stack of this very site.

{{< figure src="/svgs/hugo-logo-wide.svg" alt="Hello Friend" position="center" style="border-radius: 8px;" >}}

I wanted something static: it's easy to maintain and there's basically no operations needed. I had a look at what was available and choosed [Hugo](https://gohugo.io).    
I've picked a theme, [hello-friend-ng](https://github.com/rhazdon/hugo-theme-hello-friend-ng), from https://themes.gohugo.io/ and rolled with it.  
For hosting, I followed the [official hugo guide to host on github pages](https://gohugo.io/hosting-and-deployment/hosting-on-github/).  

After this simple setup, what was left to do was:
- Integrating a newsletter, with the help of the following [guide](https://fullstackalmanac.com/post/2020-10/add-a-newsletter-to-hugo/)
- Having external links be open in another browser tab, with the help of this [forum post](https://discourse.gohugo.io/t/how-to-open-plain-url-links-in-a-new-tab/25523/3)

Now I want to figure out how to generate a newsletter when I publish a new post, ideally with a github action.
