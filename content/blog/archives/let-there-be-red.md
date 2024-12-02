---
title: "Let There Be Red"
date: 2022-09-17T14:56:44+02:00
draft: false
toc: false
images:
tags:
---

Hi everyone, I hope you all had a great weekend!

Today I'm releasing my micro game, and you can all play it and give me some feedback on the [itch.io page](https://thibaudio.itch.io/pixel-platformer)

It all started [3 weeks ago](http://localhost:1313/posts/scoping-with-time), when I settled on releasing on game each month.
This month, I started following [HeartBeast great godot tutorial](https://www.youtube.com/watch?v=f3WGFwCduY0&list=PL9FzW-m48fn16W1Sz5bhTd1ArQQv4f-Cm), that I wanted to turn into a small but finished game.

Here's the final todo-list:
- [X] Complete the tutorial
- [X] Options menu
- [X] Save/Load System
- [X] Option to select the character skin
- [X] Main Menu
- [X] Option to adjust the sound level
- [X] Collectibles
- [X] itch.io page
- [X] gitlab CI/CD to automatically build and push to itch.io 
- [X] Tweak the character controller 
- [X] Add a shooting enemy
- [X] Win screen
- [X] In game menu
- [X] Credits
- [X] Add music
- [X] 3 levels
- [X] Fix starting music
- [X] Controller support
- [X] Fix HTML export?
- [X] Find better fonts
- [X] Shield? (to block and throw at enemies) - removed
- [ ] Unlockable abilities (double jump, dash, ...)
- [ ] Option to rebind controls?
- [ ] Level selection screen?

At the end, I decided to remove the shield ability, as it was not fitting at all with the rest of the game.

## Godot exporting issues
I had a weird issues when exporting to html: levels refusing to load, sliders not registering...  
In the console, I had errors like:
```
ERROR: In Object of type 'HSlider': Attempt to connect nonexistent signal 'drag_ended' to method 'Control._on_MasterVolumeSlider_drag_ended'. index.js:362:18
   at: connect (core/object.cpp:1462) - Condition "!signal_is_valid" is true. Returned: ERR_INVALID_PARAMETER index.js:362:18
```

Took a long time to figure out what was happening, I even started writing this blog post stating that the game will not release with a browser version!  
Thanks to [godot discord](https://discord.gg/4JBkykG), I found that I was using godot 3.4 in my CI template, but I was on godot 3.5.  
Updating the docker image used in `.gitlab-ci.yaml` from `image: barichello/godot-ci:3.4.2` to `image: barichello/godot-ci:3.5` solved all my issues.  

## Next game
For my next game, I settle on a small puzzle game.  
You play as the Little Red Riding Hood on a 6x6 grid and each time you move, the big bad wolf moves as well.  
To be able to exit the level, you need to make the wolf pass the hunter without getting caught first.

{{< figure src="/images/little_red_riding_hood.png" alt="Little Red Riging Hood" position="center" style="border-radius: 8px;" >}}  

&nbsp;  
  
I'll tell you all about the game, the process and how bad I am at drawing!

Thanks for reading and see you next week!