---
layout: post
title:  "Godot Wild Jam #17 - Day 01"
subtitle: "Lets give the Godot engine a try"
date:   2020-01-10 12:20:00 +0000
category: WGJ-17
featured_image: '/assets/backdrops/godot-wild-jam.png'
description: 'A Week long games jam featuring a theme choosen from suggestions on the Godot Wild Jam Discord server with 3 random Wild cards to optionally include in your title.'
---

# Its Jam time

Explain the Jam!

So its here, after a long week the theme for the Godot Wild Jam #17 has been announced. 'Second Chance' revieled in this totally over the top release video, I love it!.

<iframe width="500" height="281" src="https://www.youtube.com/embed/zZOJmcEQBKE" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Along with the theme there is also 3 optional 'Wild Cards' to include in your game. Those are:

![Wildcards][wildcards-png]


See the Itch.io page [here](https://itch.io/jam/godot-wild-jam-17)

## End of Day 1 

I got a pretty good idea of the kind of game I want to make, I am aiming for a top down 2D dungeon crawler rouge like with a second chance mechanic that when you die a QTE mini game will pop up and give you the chance to revive yourself. This will be timed and will increase in difficultly the more it is used. I want to aim to get at least one of the wild cards done, I've my sights set on the incorperating coop multiplayer into the game. So today was mostly planning and hashing out my idea. 

I did however get a few good starting point tasks done that being setting up a Trello board with a list of all the mechanics I hope to implement and short checklist of features required for that mechanic. Set up the github repository, source control is vital less code needing to be rewritten or copyed to and from USB drives the better. Also something I have never done this early into development of a game I went searching for game art, I wanted to get a feel for what was out there and what kind of atmosphere I can achieve using free assets after all I am cheap and the internet has near endless amounts of resources that can be scoured



[wildcards-png]: {{ site.url }}/assets/wild_jam_17/wild_cards.png
[temp-assets-png]: {{ site.url }}/assets/wild_jam_17/wild_cards.png
[trello-board-png]: {{ site.url }}/assets/wild_jam_17/wild_cards.png

TODO:
* WRITE DAY 1
* CROP IMAGES
* ADD IMAGES AND VIDEO
* SPELL CHECK AND FINAL READ

## Day 1: When was my first chance ?



There is nothing here Opps 


[IMAGE]{}
## Day 2: Upgrades and Core Mechanics

All in all it was a good day of development, I spent a couple hours in the morning; Took a break to meet Amy for lunch and then worked on it for the afternoon into the night were I had to eventually pull myself away. I got the following done:

* Updated Godot from 3.1.1 -> 3.2, this is related to a new `draw_arc` function in the newer version of Godot.
* Cleaned up and tiled my Sandbox area that I use for testing features.
* Made a little health and mana indicator and gave it a lil bob effect.
* Most importantly I fleshed out second chance mechanic.

[Sandbox-Test-Area]:  {{ site.url }}/assets/wild_jam_17/Day2_screenshot.png
### Sandbox 
Just a simple test area I tend to use a throw away scene purely for testing

[Health-Bar]:  {{ site.url }}/assets/wild_jam_17/Day2_healthbar.png
### Health Bar
The health mechanic is reminisent of the Zedla Breath of the Wild Stamina meter, this is not a game I own or have played but non the less I can still appreciate the game dev wonder that is is.

[Second-Chance]:  {{ site.url }}/assets/wild_jam_17/Day2_second_chance.png
### Second Chance Mechanic
The second chance mechanic is the center point of this whole games jam so I figured it would be best to get it started early so we can improve it going forward. So copying some of the work I did for the health bar I broke my idea down into its smallest possible components. That is a dynamically drawing shape generated by a series of points, a timer with a circluar countdown clock to illistrate the timer and the QTE button presses which would require some Keys, randomly generating them and placing them.

[PAPER IMAGE HERE]


#### Timer
For counting down the minigame playtime. The visual representation of this will be made using a cool tutorial found on Youtube were I get most of my knowledge. It was intended to mimic the stamina bar from Zelda Breath of the wild.

#### Shape
This is for scaling difficultly my original plan was to add more button presses the more difficult the minigame is meant to be. I wrote a little piece of code to find a number of points along the edge of a circle. Then I had to to deal with having the first point be at Vector(0, -1) for ascethic reasons. This is all simple maths that I had learnt in college but trying to muster up the equations was near to impossible. Google is your friend.

#### Key Generation
Given that we have a number of points from the previous step all I had to do was randomly generate a list of keys of the same length of points and position them at the points we found. Then a simple controller function to allow for progression and failure.


[Second-Chance]:  {{ site.url }}/assets/wild_jam_17/Day2_second_chance_fail.png

With the coming week being a busy one in work, unfortunitly I am not sure how much time I will have to work on it hence I am aiming low and so happy with my progress


[IMAGE]{}
## Day 3: Animations

This being the first short day of dev I was interested in getting as much quality into the game in as small of a time as possible. I figured the best quality of life improvement that I was capible of approaching at this stage is animations. So I added the AnimatedSprite node to the player and broke out my spritesheets using an online tool, and reimported as 2D pixel sprites. Now that I had a bunch of new states that are not implemented I moved on to implementing the attack. I achieved this by placing a Area2D node onto the player, add it to a different Collision layer to the player so they dont collide and disabled it by default unless the Players `Attack` animation is playing. I added a simple Enemy which at this stage is just a collection of AniamtedSprite, Area2D for detection area and KinematicBody2D for physics. For a shor tday I felt pretty good with the amount of work I got finished.
 
[IMAGE]{}
## Day 4: State Machines
At the moment my game is pretty user input driven if the user is not pressing buttons nothing is happening, I hope to resolve this by implementing a State Machine in both my player and enemy. This is important as this decides if you are doing A and an event is triggered should we move to state B or C well rather than flooding the script with if statments the proper way to implement this is using the State Machine pattern. 

After implementing I was looking for a way to test and expand my implemenation so next I added a DEAD state to the player which kicks in when health is zero using debug keys I was able to remove health 10 pts at a time and when the players health hit 0 the state will change to Second Chance and after failure change to Dead, this will change the animation, toggling the user input. I finished the evening off my creating a couple of sprites and including them in the Player AnimatedSprite

[IMAGE]{}
## Day 5: AStar
As per my game dev philophascy it is best to start work looking at what you last finished with. I noticed I was getting some clipping within the tile map and figured it was my fast and loose creation of the tiles that perhaps made this bug. After remaking the tile sheet and set my sizes for tiles for the game I still see the issue, turns out it had to do with linear 2D camera movement. After changing some toggle boxes in the project settings I got this resolved.

I got the AStar Godot functionality working follow GDQuests helpful video tutorial which I would recommend. Next was to hook up my hollow enemy who just animates and dies to be able to move, select target (in this case the player) and losing the player if out of sight. Using a mixture of Timers and Area2D for a detection area I was able to create what I think was a liberal use of AStar to avoid recalculating every frame. To finish off the evening I threw a second chance logo onto the players health bar.


## Day 6: Burnout and Stress
Got home from work, this being demo day I was working til around half 7, getting deadlines and attending remote demo via hangouts. Burn in began to set it with cooking, cleaning, working late and demo stress I didn't feel up to developing, the hope being I would be fresh for the final weekend.

## Day 7 - End of Jam: Pivot and Acceptance 
This was difficult for me to do but I decided halve way through Friday night I came to the realisation that to get the Jam done I would have to be flat out, this is something I am ofcourse used too but this weekend fell on possible the most important weekend of the year for me this was my Anniversary, 11 years to be specific. Amy is my favourite person my partner in crime and I wouldn't be half the man I am if it wasn't for her. So I prioritsed my personal life over the Jam.

It was a strange sense of calm that washed over me in the minutes after coming to this decision. I am quiet a driven person but I am the first to admit I am also tough on myself when it comes to dead lines I feel like if I dont hold myself accountable who will, if I am making excuses at the end then I didnt apply myself along the way. This is usually my down turn but I am enjoying the Jam and my game too much to rush and put up only 10% of what I wanted for the Jam so my descion is to drop the deadline of the Jam and continue to develop the game in my free time. I am going to give it a maximum of 3-4 weeks. Seeing what I can get done in a week I would love to take the foot off the gas and enjoy the ride alittle more. So hopefully some time in February there will be a `final` update for my Godot Wild Jam #17 entry.