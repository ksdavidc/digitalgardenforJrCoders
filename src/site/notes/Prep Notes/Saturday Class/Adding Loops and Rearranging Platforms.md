---
{"dg-publish":true,"permalink":"/prep-notes/saturday-class/adding-loops-and-rearranging-platforms/","dgHomeLink":true,"dgPassFrontmatter":false}
---

We are on page `= this.file.name`.
fixes:
remove loop reflip
- [[#`= this.file.name`.|`= this.file.name`.]]
	- [[#`= this.file.name`.#SUMMARY|SUMMARY]]
	- [[#`= this.file.name`.#DETAILS|DETAILS]]
		- [[Prep Notes/Saturday Class/Adding Loops and Rearranging Platforms#DETAILS|Set up the Costume Numbers]]
		- [[Prep Notes/Saturday Class/Adding Loops and Rearranging Platforms#DETAILS|Add to the Costume List]]
			- [[Prep Notes/Saturday Class/Adding Loops and Rearranging Platforms#Add to the Costume List|Here is how we do it]]
		- [[Prep Notes/Saturday Class/Adding Loops and Rearranging Platforms#DETAILS|Bringing Loop Buttons to New Positions]]
		- [[Prep Notes/Saturday Class/Adding Loops and Rearranging Platforms#DETAILS|Copy some code to make the new loop buttons work]]
		- [[Prep Notes/Saturday Class/Adding Loops and Rearranging Platforms#DETAILS|Add dots]]
		- [[Prep Notes/Saturday Class/Adding Loops and Rearranging Platforms#DETAILS|Change the other gravity changers]]
		- [[Prep Notes/Saturday Class/Adding Loops and Rearranging Platforms#DETAILS|Change one of the Goodies (collectibles)]]
		- [[Prep Notes/Saturday Class/Adding Loops and Rearranging Platforms#DETAILS|Change the portal]]
		- [[Prep Notes/Saturday Class/Adding Loops and Rearranging Platforms#DETAILS|Make your own level 2]]



# `= this.file.name`.

## SUMMARY
We have 9 things to do:

1.  [[Prep Notes/Saturday Class/Adding Loops and Rearranging Platforms#Adding Loops and Rearranging Platforms|Set up the Costume Numbers]]

The platform in the Platform and the Antiplatform and the Lava need to be in the same order, 1-for-1. 

2. [[Prep Notes/Saturday Class/Adding Loops and Rearranging Platforms#WHERE DO WE CHOOSE THE ORDER OF THE COSTUMES???|Add to the Costume List]]

Right now the level 1 platforms in this order in a list. 

> *1  .  2  .  4  .  1  .  2  .  1  .  **5**  .  1  .  **18**  .  1*

These numbers are costumes, and **5** and **18** are our loop costumes. 

We are going to add your loop costumes (**21**) and two other costumes (**1**) into the list like this:

> *1  .  2  .  **<u>1</u>**  .  **<u>21</u>**  .  **<u>1</u>**  .  4  .  1  .  2  .  1  .  **5**  .  1  .  **18**  .  1*


3. - [[Prep Notes/Saturday Class/Adding Loops and Rearranging Platforms#DETAILS|Bringing Loop Buttons to New Positions]]

The loops are controlled by loop buttons. The old loops changed position, so we have to change the loop buttons as well. To this we change a block in the Gravity Changer sprite. We also have to add some new loop buttons.


4. [[Prep Notes/Saturday Class/Adding Loops and Rearranging Platforms#WHERE DO WE CHOOSE THE ORDER OF THE COSTUMES???|Copy some code to make the new loop buttons work]]

The Loop Buttons use `if loops` to make the loop costume change as we gp through the loop. The `if loops` are in the Platform and Antiplatform sprites. We have to **Copy**, **Paste** , and **Change** that code to make our new loop work.

5. [[Prep Notes/Saturday Class/Adding Loops and Rearranging Platforms#WHERE DO WE CHOOSE THE ORDER OF THE COSTUMES???|Add dots]]

This makes the costumes go offscreen.

6. [[Prep Notes/Saturday Class/Adding Loops and Rearranging Platforms#WHERE DO WE CHOOSE THE ORDER OF THE COSTUMES???|Change the other gravity changers]]

At some points in the game, we hit buttons and gravity changers and Sonic flies up. We have to change the position of these gravity change buttons.

7. [[Prep Notes/Saturday Class/Adding Loops and Rearranging Platforms#WHERE DO WE CHOOSE THE ORDER OF THE COSTUMES???|Change one of the Goodies (collectibles)]]

To win the game you have to collect 3 "Goodies". The last one changed position, so we have to fix it.

8. [[Prep Notes/Saturday Class/Adding Loops and Rearranging Platforms#WHERE DO WE CHOOSE THE ORDER OF THE COSTUMES???|Change the portal]]

Since our level is longer, we have to move the Portal as well.

9. [[Prep Notes/Saturday Class/Adding Loops and Rearranging Platforms#WHERE DO WE CHOOSE THE ORDER OF THE COSTUMES???|Make your own level 2]]

You made or will make a storyboard. We can put it into our game as a new level, by changing or creating items in the costume list. We may have to add one or more platform costumes.

## DETAILS

### Set up the Costume Numbers

You should now have 4 costumes for the loop. To make this easier, give them the following names: 

- Platform: **My loop start** and **My loop return**
- Antiplatform: **My antiloop start** and **My antiloop return**


The important thing is that the start and return costumes have the **same number in each sprite**. To make it easier, use **21** and **22**, like I am doing.  In other words, make costumes **20**, **21**, and **22** like this:

Your costume **20** is probably the Loop Base. We won't actually use this in the game, but leave it or put a blank costume 20 if you need to.
![Base for Loop De Loop|50](https://i.imgur.com/XOCMGUC.png)


**COSTUME 21**: **My loop start** ![Loop Start|25](https://i.imgur.com/IGxRDRU.png) is costume **21** in Platform, and so is **My antiloop start** ![Antiloop Start|25](https://i.imgur.com/2y0ilLK.png)
(in Antiplatform)
**COSTUME 21**: **My loop return** ![Loop Return|25](https://i.imgur.com/199xT9m.png) is costume **22** in Platform, and so is **My antiloop return** ![Antiloop Return|25](https://i.imgur.com/zP2NbbN.png)(in Antiplatform)

Same *number*, but *different costumes*. Move any **other** costumes you made **to the end of the sprite**. Keep costumes 1-19 the same. 

### Add to the Costume List 

In your storyboard, 

![storyboard](https://i.imgur.com/J05HIwO.jpg)
you had 5 platforms, a straight one, the loop, another straight one, and two bumpy ones. 

We give each different costume in this a number:

![costume numbers](https://i.imgur.com/Hov7BeT.jpg)

* The two straight ones are the same, so we  use the same number, costume 1. 
* The loop is costume 2. 
* Let's say the two bumpy ones are the same, let's say costume 3. (*You may decide not to make them the same. This is just an example to show you how to reuse costumes.*)

So, the game has 5 platforms, but only needs 3 costumes.

When you make your game, you will put your level into a list like this:

> *1  .  2  .  1  .  3  .  3

To show you how, let's look at my project.  My level 1 looks like this:

> *1  .  2  .  4  .  1  .  2  .  1  .  **5**  .  1  .  **18**  .  1*
>   
>*The **5** represents the Sonic Loop de loop.
>The **18** is the green loop de loop.* 
>
>*The other numbers are other kinds of platform. 
>You can see them in the costume tab of the Platform Sprite.*

We are going to add your loop (**21**) and two other sprites (**1**) into level like this:

> level 1: 
> 	>*1  .  2  .  **<u>1</u>**  .  **<u>21</u>**  .  **<u>1</u>**  .  4  .  1  .  2  .  1  .  **5**  .  1  .  **18**  .  1*
> 
> *The **<u>21</u>** will be your new Loop de Loop.*
> *The  **<u>1</u>**'s are plain platforms.* 

#### Here is how we do it
The order of the platform costumes used in the games is stored in a list called **costume list for all level**. This list and its code in the platform sprite is where we tell scratch where each costume goes. Find it in the Platform sprite. 


```ad-scratch
~~~scratchblock

define initialize start of costumes list
don't touch this:
delete all of [location of platform v]
delete all of [costume list for all level v]
delete all of [start of costumes for this level new v]
/ / [level 1]::custom
add [1] to [start of costumes for this level new v]

*level 1 starts here  
add [1] to [costume list for all level v] // straight platform
add [2] to [costume list for all level v] // floor and ceiling
**YOU WILL ADD YOUR STUFF HERE**!!!!
add [4] to [costume list for all level v] // the wall
add [1] to [costume list for all level v]
add [2] to [costume list for all level v] // floor and ceiling
add [1] to [costume list for all level v]
add [5] to [costume list for all level v]// platform 7: Sonic Loop
add [1] to [costume list for all level v]
add [1] to [costume list for all level v]
add [18] to [costume list for all level v]// platform 10: green loop
add [1] to [costume list for all level v]
and ends here.  

Don't touch this:  
/ / [lvl 2]::custom
add ((length of [costume list for all level v]::data) + (1)) to [start of costumes for this level new v]

*This is the data for level 2:
add [2] to [costume list for all level v]
add [3] to [costume list for all level v]
add [4] to [costume list for all level v]
...
more stuff
this is the end of level 2

More stuff. Don't touch:
/ / [pt 2]::custom
set [NUMBER OF LEVELS v] to (length of [start of costumes for this level new v]::data)
/ / [used to get number of platforms this level, when setting up last level]::custom
add ((length of [costume list for all level v]::data) + (1)) to [start of costumes for this level new v]

~~~
```


The Sonic Loop in our game is costume number 5, it looks like this:

```ad-scratch
~~~scratchblock
add [ 5 ] to [costume list for all level v]  
~~~
```

Do you see it? It is the 7th block in the list. 

The second green loop in the game has costume 18. Can you find it? Which number is it?

We are going to change this to add your new loop. We can add it anywhere, but in this case, we will add it near the beginning after the first antigravity section. You can change this later. When  you make your own, this is where you will start.

The general way to add a platform is to add the costume number:
```ad-scratch
~~~scratchblock
add [loop start costume number] to [costume list for all level v]  

~~~
```

What do we add for your costume? We are going to add 3 blocks. We will add a plain straight platform (costume 1), then our loop (costume 21), then another plain straight platform. So in our case: 

```ad-scratch
~~~scratchblock

add [ 1 ] to [costume list for all level v] // a straight platform 
add [ 21 ] to [costume list for all level v] // your new loop  
add [ 1 ] to [costume list for all level v]  //another straight platform

~~~
```

Add this to the list like this:

```ad-scratch
~~~scratchblock
define initialize start of costumes list
delete all of [location of platform v]
delete all of [costume list for all level v]
delete all of [start of costumes for this level new v]
/ /* [level 1]::custom
add [1] to [start of costumes for this level new v]
add [1] to [costume list for all level v]
add [2] to [costume list for all level v]  
add [ 1 ] to [costume list for all level v]  // NEW
add [ 21 ] to [costume list for all level v] // NEW: this is the loop, platform 4
add [ 1 ] to [costume list for all level v] // NEW
add [4] to [costume list for all level v]
add [1] to [costume list for all level v]
add [2] to [costume list for all level v]
add [1] to [costume list for all level v]
add [5] to [costume list for all level v]// Sonic is now platform 10
add [1] to [costume list for all level v]
add [1] to [costume list for all level v]
add [18] to [costume list for all level v]// green loop is now 13
add [1] to [costume list for all level v]
...
and so on...
~~~
```

That's it! If you run the game it will show-- BUT it won't work!!! We will have to do some more coding.

### Bringing Loop Buttons to New Positions

We need to go to the Gravity Changer Sprite. Find these two blocks:

```ad-scratch
~~~scratchblock

Make blocks at platform [7] starting with id [3]::custom
Make blocks at platform [10] starting with id [8]::custom

~~~
```

At first, we had a platform with costume 7.

```ad-scratch
~~~scratchblock
Make blocks at platform [7] starting with id [3]::custom
~~~
```

This starts with id 3. This my block creates 3 new antigravity buttons, with ids 3, 4, and 7. (ids 5 and 6 are created elsewhere in the game.)

The next time we did platform with costume 10 and started with the next id, button 8:

```ad-scratch
~~~scratchblock
Make blocks at platform [10] starting with id [8]::custom
~~~
```


But, we added 3 platforms, so our old platform 7 became platform 10:

```ad-scratch
~~~scratchblock
Make blocks at platform [10] starting with id [3]::custom 
~~~
```

And platform 10 became platform 13:
```ad-scratch
~~~scratchblock
Make blocks at platform [13] starting with id [8]::custom
~~~
```

Our new loop is platform 4,  and the next available id is 13.

```ad-scratch
~~~scratchblock
Make blocks at platform [4] starting with id [13]::custom
~~~
```

So in the end, we have this:

```ad-scratch
~~~scratchblock
/ / 7 becomes 10
Make blocks at platform [10] starting with id [3]::custom 
/ / 10 becomes 13
Make blocks at platform [13] starting with id [8]::custom 

and add this: 
Make blocks at platform [4] starting with id [13]::custom
~~~
```


### Copy some code to make the new loop buttons work

In the Platform and Antiplatform sprite there are some `if  blocks` like this:


```ad-scratch
~~~scratchblock
when I receive [switch to loop start v]
if <(costume [name v]) = [loop return]> then
    set [brightness v] effect to (0)::looks
    switch costume to [loop start v]
    go to [front v] layer
end
if <(costume [name v]) = [Loop return2]> then
    set [brightness v] effect to (0)::looks
    switch costume to [Loop start2 v]
    go to [front v] layer
end

~~~
```

We will **copy** one of the if loops, **paste** it to the end, and **change** it a little:

```ad-scratch
~~~scratchblock
when I receive [switch to loop start v]
if <(costume [name v]) = [loop return]> then
    set [brightness v] effect to (0)::looks
    switch costume to [loop start v]
    go to [front v] layer
end
if <(costume [name v]) = [Loop return2]> then
    set [brightness v] effect to (0)::looks
    switch costume to [Loop start2 v]
    go to [front v] layer
end
/ / new
if <(costume [name v]) = [My loop return]> then
    set [brightness v] effect to (0)::looks
    switch costume to [My loop start v]
    go to [front v] layer
end
~~~
```

We changed the name of the costume in the if statement, and we changed the name of the costume that we switch to.

We need to do the same thing (**copy**, **paste**, **change**) in the 

```ad-scratch
~~~scratchblock
when I receive [switch platform to back v]
...
~~~
```
and
```ad-scratch
~~~scratchblock
when I receive [switch to loop return v]
...
~~~
```

blocks. Make sure you type in the correct costume name and choose the correct costume to switch to.

Then, do the same thing for the three if blocks in the Antiplatfrom sprite.

### Add dots

You might see some costumes stay a little bit onscreen when they reach the edge. We add dots to the bottom of their costumes to make them go offscreen as we move past them.

### Change the other gravity changers


change 1700 to 3100
and change 2100 to 3500


### Change one of the Goodies (collectibles)

Add 480  * 3 to the third one.

### Change the portal

Add 480  * 3 to the where you spawn it.


### Make your own level 2
change the placement of the platforms. Add loops (with antigravity buttons)

Add goodies and baddies. 

