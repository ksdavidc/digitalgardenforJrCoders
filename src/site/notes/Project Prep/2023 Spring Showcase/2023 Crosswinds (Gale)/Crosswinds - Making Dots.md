---
{"dg-publish":true,"permalink":"/project-prep/2023-spring-showcase/2023-crosswinds-gale/crosswinds-making-dots/"}
---


## Create the Dots Sprite

Make a dots sprite. This will be for the first player, who is trying to make lines that go left to right. 

A good costume for this is a triangle going right like this "🚩". It should be pretty small, say about 10 x 10 pixels. 

When we receive the `make dots` broadcast, we will "make" the dots. There will be 4 rows and 5 columns of dots.



## Creating the Dot Clones

### Row 1
Let's make the first row. We go to the position of the first dot. In this case it will be `x: (-100) y: (125)`.

Then we make a copy of the sprite, a **clone**. Think of these as *baby* sprites, and our normal sprite is the *mother* sprite. It will show up right there (though it will cover our mother sprite.)

```ad-scratch
title: 
~~~scratchblock
when I receive [make dots v]
go to x: (-100) y: (125)
create clone of [myself v]
~~~
``` 

Now we do the same thing, but first we move 50 pixels to the right. That means `x` changes from -100 to -50. `y` stays the same.

```ad-scratch
title: 
~~~scratchblock
when I receive [make dots v]
go to x: (-100) y: (125)
create clone of [myself v]
go to x: (-50) y: (125)
create clone of [myself v]
~~~
``` 


Do this 3 more times, changing x by 50 each time. 


Now the first row has 5 clones, all at y = 125.

### A Better Way: A Loop for Columns

But there is a better way to do this. 

It would be nice if we could do something like this:

```ad-scratch
title: 
~~~scratchblock
when I receive [make dots v]
repeat (5)
go to x: (-100) y: (125)
create clone of [myself v]
end
~~~
``` 

The problem is that this would put all 5 clones in the same place. Repeating is good, but we want to **repeat with a small change**. `x` has to change each time through the loop. 

Luckily, there's a trick that will help us. 

If you have a number in your code, you can replace that number with a variable. In this case, the number is -100. That's the number that changes in the repeat loop. 

Create a variable called `(x value)`. Make sure it is a **for this sprite only** variable. This will make sure only this sprite uses these variables.
{ .hasInlineScratch }

The first thing we do is set the variable to the starting number.

```ad-scratch
title: 
~~~scratchblock
when I receive [make dots v]
set (x value) to (-100) 
repeat (5)
go to x: (-100) y: (125)
create clone of [myself v]
end
~~~
``` 

Then we use the variable instead of the number where it appears. 

```ad-scratch
title: 
~~~scratchblock
when I receive [make dots v]
set (x value) to (-100) 
repeat (5)
go to x: (x value) y: (125)
create clone of [myself v]
end
~~~
``` 


So far this doesn't help us. But, at the end of the loop, we can change `x value` after creating the clone. Now each time through the repeat loop, the `x value` changes. 


```ad-scratch
title: Dots 1
~~~scratchblock
when I receive [make dots v]
set (x value) to (-100) 
repeat (5)
go to x: (x value) y: (125)
create clone of [myself v]
change [x value v] by (50)
end
~~~
``` 

The first time it is -100, then -50, then 0, then 50, then 100. This is what we want.

Why do we do this? 
1. The code is shorter. If there is a lot of code in the loop, this can make it much shorter.
2. The code is easier to adjust. For example, if we decide we want 6 columns, we just have to change the number 5 to 6 (and maybe adjust the starting `x value` or the amount of change). 

### Row 2
Can you make the next row? Again, we want to create 5 more clones the same way, but make y = 75. Use a repeat loop if you can.

### Rows 3 and 4
After that we need 2 more rows, one with y = 25 and one with y = -25. 

You should now have 4 rows of 5 dots each. 

### A Better Way: A Loop for Rows

Did you notice that when we created the four rows we had another example of **repeating something with a small change**. This time `y value` changes. If you want to make your code better, you could use the same trick above. The first step is to make a variable called `y value`, and set it to its starting value, -125. Again, make sure it is a **for this sprite only** variable.

```ad-scratch
title: Dots 1
~~~scratchblock
when I receive [make dots v]
set (y value) to (-125) 
...

~~~
``` 

Then we will add a repeat loop around **ONE of the row loops** code. The red part is JUST the code for the **FIRST ROW** you created above. 


```ad-scratch
title: Dots 1
~~~scratchblock
when I receive [make dots v]
set (y value) to (125) 
repeat (4)
the code for FIRST ROW goes here ::custom #F00
end
~~~
``` 

Then, we use the variable in the places where  `y value` appears.


```ad-scratch
title: Dots 1
~~~scratchblock
when I receive [make dots v]
set (y value) to 125) 
repeat (4)
the code for the FIRST ROW with (y value) ::custom #F00
end
~~~
``` 

And last, at the bottom of the repeat loop, change `y value`.

```ad-scratch
title: Dots 1
~~~scratchblock
when I receive [make dots v]
set (y value) to (-150) 
repeat (4)
the code for the FIRST ROW with (y value) ::custom #F00
change [y value v] by (-50)
end
~~~
``` 

## Hiding and Showing the Dots

### Hide on creation
We are creating the dots in the **Setting Up** stage pf the project. We will create the clones only once for the whole game. 

We want each clone to be hidden when it is created. We will only show them during the game loop, after the player has been chosen. So, we hide them when they are created:

```ad-scratch
title: 
~~~scratchblock
when I start as a clone
hide
~~~
``` 

### Show after player chosen

If you look at the code for each player, once the player is chosen, we broadcast **show current player**. 

```ad-scratch
title: Player 1 sprite
~~~scratchblock
when this sprite clicked
hide
set [CURRENT PLAYER v] to [1]
broadcast [show current player v] and wait

~~~
``` 

Thaat's the moment we want the clones to appear in the game loop.
```ad-scratch
title: Dots 1
~~~scratchblock
when I receive [show current player v]
show
~~~
``` 


### Hiding in Start Game Loop

However, once the round is finished, we go back to the **start game loop** position. We have to hide the dots at this point, so that they are hidden when we choose the player. So we add this:

```ad-scratch
title: Dots 1
~~~scratchblock

when I receive [START GAME LOOP v]
hide

~~~
``` 

### Hiding the Mother

One last thing. We don't want to see the mother sprite. She is just there to watch and make babies. So we hide her right away, in the receive make dots routine. 

Careful:
* This is not a new stack, but make dots stack we created above.
* Remember, the grey dots mean "the code that is already there". We are putting the hide block right after the receive block and before the other code.

```ad-scratch
title: Dots 1
~~~scratchblock
when I receive [make dots v]
hide
...
~~~
``` 
## Dots 2

Player 1 now has his dots. Player 1 is going right to left. But we need a second set of dots for player 2. He is going top to bottom. 

Player 2's dots are almost the same. To start, just **duplicate the entire sprite**.

But we have to make some changes. Here are the differences:

* This time the costume is a down arrow::small_red_triangle_down: 
* Make it a different color.
* 4 columns of dots per row, and 5 rows! 
* The start x and y values are different:
	* `x value` = -75
	* `y value` = 150

If you used repeat loops, it will be quick and easy. If not, not so quick and easy.


## Good Job!

That's it. Good job!