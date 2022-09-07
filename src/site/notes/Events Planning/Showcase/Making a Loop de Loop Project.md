---
{"dg-publish":true,"permalink":"/events-planning/showcase/making-a-loop-de-loop-project/","dgHomeLink":true,"dgPassFrontmatter":false}
---

# Making a Loop de Loop 
## Loop de Loop Costumes

The Loop de Loop Costumes are part of the [Sonic Loop De Loop Scroller project](https://scratch.mit.edu/projects/727409961/).

In the project there are Platform and AntiPlatform Sprites. Some of the costumes in those sprites are for the loop de loop. I will show you how I made them, so you can design your own to suit your project. Mine are green and ugly, and yours can be different.    
    
There are 2 loops in the project. The first is Sonic Style, but the second one is the template I used to make it. This is the one that we are going to make today.       
    
To make a Loop, you need 4 costumes. 
* 2 normal gravity costumes (in the Platformer Sprite), and 
* 2 antigravity costumes (in the Antiplaform Sprite).  
* Each Sprite has a loop start and and loop return costume.   



When the player goes in from one side, as he reaches the top half of the loop, gravity goes up and the back of the loop moves to the front, so we can exit. Little buttons detect the player as he moves and control the changes in the costumes.
   
The costumes are easy. They all start from a Loop Base, which is basically 2 circles and 4 lines. One of the lines is just to arrange the other lines, and is deleted in the final Base.    

Once  you have the base, a few simple steps creates the 4 costumes. I will show you how to make the Platform Start and Return costume, and I will show you what the Antiplatform  costumes look like so you can make your own. In fact, this is not the only shapes these costumes could have for a loop, but this is the way I am doing it in this project. 

## Creating a Loop Base
This is what the Loop Base should look like this:

![Base for Loop De Loop](https://i.imgur.com/XOCMGUC.png)

1. Go into vector drawing mode.
2. Draw **circle 1** with a thick border and no fill. Center it.
3. Copy and Paste, and center **circle 2** if you need to. They should be in the same place.
4. Make sure you have only **circle 2** selected with the arrow tool, and use Option/Alt and drag a corner to make **circle 2** bigger while keeping the center the same.
5. Add lines:
	1. At the bottom, overlapping the bottom point of **circle 2**, from the left edge to the right edge, draw a **big circle base line** (see below).
	2. At the bottom of **circle 1**, another line overlapping the bottom point of **circle 1**, from the left edge to the right edge. Don't worry if it doesn't look right. You will delete this line later. This is the **small circle base line**.
	3. Now we put 2 lines right **on top of this line**:
		1. The **left small base line** goes from the bottom of **circle 1** to the left edge.
		2. The **right small base line** goes from where the line crosses **circle 2** to the right edge.
		3. These 2 base lines should go right over the small circle base line, but not cover the **gap** between the two circles on the right.
	4. Now you can delete line 5.2, the **small circle base line**! You can nowsee the **gap** in the front track.



Now we are going to create 4 costumes from this.

#### Loop Return (for Platform Sprite)

![](https://i.imgur.com/199xT9m.png)


1. Copy the Loop Base.
2. Select all and flip it, so it faces the other way.
3. Switch to bitmap mode and use the square selection tool to delete **the right half of the loop**.
4. Go to Vector Mode and draw red lines to close the ends of the bottom tracks. Don't put a red line at the top.
5. In bitmap mode again, use the fill tool to fill the tracks, as in the green below.

#### Loop Start2 (for Platform Sprite)


![Loop Start](https://i.imgur.com/IGxRDRU.png)


Basically the same:
1. Copy the Loop Return.
2. Flip the image left to right.
3. In bitmap mode, use the square selection tool to delete **just a little from the top**. The cutoff is a little above where the path turns. We need a little bit of curve to keep the player from flying off, but we don't want to go the whole way, because we need the Antiplatform costume will catch the upward gravity.

Then repeat steps 4 and 5 above.

Here are the other 2 as challenges for you:

#### Antiloop Return2

This is the easiest.

![Antiloop Return](https://i.imgur.com/zP2NbbN.png)


#### This is Antiloop start2

This is easy if you see the trick.

![](https://i.imgur.com/2y0ilLK.png)



Now that you have the basic idea, you can make any kind of loop you want. It can be as thick as you want, and you can fill the track with whatever colors or images you want. You can even make it out of other shapes. See the other loop [in my project](https://scratch.mit.edu/projects/727409961/) for an example.

### Small Dots

Once you are done with all that, you can convert all your costumes to vector. It turns out you need to add small dots at the bottom to keep the images off screen as you scroll. This is a quirk in Scratch. You can see the small dots if you look at some other costumes. They are at the very bottom of the costume, off screen. You can see them now. To really hide them, make them transparent.

