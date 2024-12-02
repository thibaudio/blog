---
title: "Back to Normal"
date: 2022-09-10T17:19:50+02:00
draft: false
toc: false
images:
tags:
---
Hi friends!  
I hope you all had a great week.  

[Last week](/posts/back-to-school) I talked about how I had more time than I anticipated to be gamedev'in, well turns out that this week was the opposite.
I thought I would have 10 hours, but I only had 4: sometimes I'm too burned-out by my day job to open an editor in the evening.  
Anyway, I still made a bit of progress, here's what the todo-list looks like now:
- [X] Options menu
- [X] Save/Load System
- [X] Option to select the character skin
- [X] Main Menu
- [X] Option to adjust the sound level
- [X] Collectibles
- [X] itch.io page
- [X] gitlab CI/CD to automatically build and push to itch.io 
- [ ] Unlockable abilities (double jump, dash, ...)
- [ ] Tweak the character controller 
- [ ] Add a shooting enemy
- [ ] 10 Levels (1/10 done)
- [ ] Win condition
- [ ] Add music
- [ ] Controller support
- [ ] Find better fonts
- [ ] Option to rebind controls?
- [ ] Level selection screen?
- [ ] Shield? (to block and throw at enemies)

## VimJam3
I wanted to add a special mechanic to the game, and [VimJam3](https://itch.io/jam/vimjam3) gave me the prompt I needed.  
Like usual there's a Theme in this jam, and this year it's `Turn up the Heat`. You can get inspired by it, and it will be taken into account by the voters, but it's not required in your submission. There is another constraint though: a Focus, that you need to implement in your game.
This year it was `Multi-Use`, and even though I was not planning on participating, it did spawn an idea in my head: a shield that can be use to block, charge (dash), or to be thrown at enemies.  A really unique idea, no one ever thought of; not even Blizzard or Marvel.  
{{< figure src="/images/d3-paladin.jpg" alt="Diablo3 Paladin" position="center" style="border-radius: 8px;" >}}  
I added it to the todo-list, but I don't think I will have time to get to that point: I only have 20hours remaining.

## Gitlab CI/CD
Implementing a automatic build and deployment system was fairly easy! Just setup all the needed export in godot and, with the file `export-config.cfg` committed, add a `.gitlab-ci.yaml` based on https://github.com/abarichello/godot-ci and voilà!  
&nbsp;  
{{< figure src="/images/gitlab-ci.png" alt="Screenshot of my gitlab-ci pipeline" position="center" style="border-radius: 8px;" >}}  
I will definitively keep this setup for my next games.

## One last thought
I'm reading `Atomic Habits` by [James Clear](https://jamesclear.com/) at the moment, and I wanted to share one idea that resonated with me:
> Focus on the process, not the outcome  

Here it is!  
Thanks a lot for reading and have a great week!