---
title: "Looking Back on September"
date: 2022-10-09T00:08:36+02:00
draft: false
toc: false
images:
tags:
---

Hi friends,
I hope you had a great week!

To start off, I wanted to reflect back on September a bit.

At the start of the month, I [challenged myself]({{<ref "scoping-with-time.md">}}): I'd be gamedev'in 10 hours a week and releasing a micro game every month.
Well, so far so good! In September I released a [micro platformer](https://thibaudio.itch.io/pixel-platformer), and I even released a new game this week!  
To be fair, the scope of both these games is incredibly small, but they got me started. With 3 weeks to go in October, I'll aim for a little bit bigger scope - in the form of a multiplayer game.  

This week though, I didn't do much game development. It was still a pretty productive week. Let's dive in!

## loupyestu
I released loupyestu, the puzzle game I was working on, on itch.io. Here is the page if you want to try it:  
<iframe src="https://itch.io/embed/1726014?linkback=true&amp;dark=true" width="208" height="167" frameborder="0"><a href="https://thibaudio.itch.io/loupyestu">Loupyestu by Thibaud</a></iframe>

The first 3 levels are tutorials, while the last 2 are a bit more puzzly. Nothing crazy though, I found very difficult to come out with good puzzles. First I'm not a big puzzle player, and the set of mechanism I added is a bit simplistic.

Anyway, here's what the todo list looked like at the end:
- [X] Turn based actions
- [X] Wolf pathfinding
- [X] Loose condition
- [X] Obstacles
- [X] Door
- [X] Opening the door with Wolf -> Loose as well
- [X] Hunter kills wolf
- [X] Transitions
- [X] Gramgram can be eaten by the wolf, which gives us a little more time to escape
- [X] CI/CD
- [X] Better indication that we need to kill the wolf before escaping
- [X] Sound effect
- [X] Win screen
- [X] Plate to open locked door
- [X] 5 levels
- [ ] Menu
- [ ] Options
- [ ] Save
- [ ] In game menu
- [ ] Better death animation

As you can see, I didn't add menus and saves. That's because I already added them to my other project of this week:  
## godot starting template
I started working on a template for all my games. It's open source, and you can find it here: https://gitlab.com/thibaudio/godot_game_template.
There's still a lot missing, but I'm planning to add more features while I'm building new games.   

## rust-nested-windows-manager
Another project I started this week was a custom window manager, inspired by the one [Kebabskal](https://www.twitch.tv/kebabskal) built.  
The goal is to be able to tag a window, for example godot, and have it handle by the window manager. Then it will just stacked all the tagged window in a dedicated portion of my screen. 
It's in rust and not finished at all, but you can still check it out here: https://github.com/thibaudio/rust-nested-window-manager.

## cherry on top
This week I even spent some time revamping my [site](https://blog.thibaud.io): I updated the front page a bit, and also added a space to showcase my [projects]({{<ref "games.md">}}).

## Next game project
With that said, it's time to get back in the gamez! This week I'll start working on my new project. For now, all I know is that it will be a 2vs2 multiplayer game with 10-15min session time.  
More on that next week!

&nbsp;  
  
All right, thanks for reading!  
See you all next time.

P.S. [This awesome tweet](https://twitter.com/_IAmSaKo_/status/1578934019353214976?s=20&t=B9OYOoF9RLSBhLCwxxruLg)