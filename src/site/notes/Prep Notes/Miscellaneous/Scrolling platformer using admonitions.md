---
{"dg-publish":true,"permalink":"/prep-notes/miscellaneous/scrolling-platformer-using-admonitions/","dgHomeLink":true,"dgPassFrontmatter":false}
---


- [[Prep Notes/Miscellaneous/Scrolling platformer using admonitions#Step 1|Step 1]]
- [[Prep Notes/Miscellaneous/Scrolling platformer using admonitions#Step 2|Step 2]]
- [[Prep Notes/Miscellaneous/Scrolling platformer using admonitions#Step 3|Step 3]]



## Step 1
First, this is the basic falling routine.  
```ad-scratch
~~~
when @greenFlag clicked
set [speed y v] to [0]
go to x: (0) y: (100)
forever
    change [speed y v] by (-1)
    change y by (speed y)
    if <touching [Platform v]?> then
        repeat until <not <touching [Platform v]?>>
            change y by (1)
        end
        set [speed y v] to [0]
    end
end
~~~
```

This program works as is, but we will have to give it some structure
 or a framework, so we can make a bigger and faster game. 

## Step 2

>In step 2, we build a framework for our game.  
>This framework is like a map, that helps keep our journey organized.  
>It tells us where we are, and makes it easier to change our path.
>It keeps us from getting lost, and lets us know where we need to go next.

* First we will build the framework. It won't have code from our Step 1.
* Then we will take the different blocks in Step 1, and put them where they belong within the framework. 
* In the end, the project will run exactly the same way, but all the pieces will be where they belong in our map.
* Later, the map will be able to take us to new places.

The first thing, and this is a general rule, is that games work better with just one green flag. 
There is one Master Sprite that controls the others. 
In our game, the Player is the master sprite.
Its one green flag talks to all the other sprites using broadcasts  like this:
```ad-scratch
~~~
when @greenFlag clicked
broadcast [green flag v] and wait
broadcast [Play Game v]
~~~

```

Go ahead and add that.

As always, a broadcast block is paired with (at least one) receive block.
We will make the ```when I receive [green flag v]``` stack later.

The ```when I receive [Play Game v]``` is the overall project loop. 
This is where we come back to if we want to replay the game.
```ad-scratch
~~~
when I receive [Play Game v]
~~~
``` 
we add a "Game on" myblock that sets up the game each time we play it.
```ad-scratch
~~~
Game on::custom
~~~
``` 

````ad-tip
When you see a red block like the one above, 
you may need to create its myblock definition first, if it doesn't already exist.
A myblock has two parts.
First the **definition block**, which is a hat block.
That means it has a round top:
```ad-scratch
~~~
define Game on
~~~
```
It gets put into your project automatically when you create a new myblock. 
* There is only 1 for each definition. 
* It is always at the top of a stack. 
* It only connects on the bottom.

Then there is the **call block**.
It is not a hat. 
It looks like this:
```ad-scratch
~~~
Game on::custom
~~~
```
Don't mix them up. 
You need to drag these into your project from the "blocks" area.
* There can be (and often are) more than 1 call block in each sprite.
* It is never at the top of a stack. 
* It can connect on both sides.
````
So, now your **Play Game** stack should look like this:
```ad-scratch
~~~
when I receive [Play Game v]
Game on::custom
~~~
``` 
Now add these, we will use them later.
```ad-scratch
~~~
broadcast [reset level v]
broadcast [set up this level v]
~~
``` 
Next is the main game loop.
The game **repeats** this loop over and over,
**until** we either win or lose the game.
For now, don't put anything in the brackets \< \>
```ad-scratch
~~~
repeat until <>
    Each time through the loop, we figure how much  
    each sprite will change on the screen,  
    and any other changes to the screen. 
    This is called a tick. Like the tick of a clock. (Not the insect, silly.)
    tick::custom
    When you define tick, make sure it is *without screen refresh*.
    This myblock will be used to keep the player in the middle of the screen:
    set scroll and position::custom
    Just add this here, for now:
    broadcast [tick once v] and wait
end
~~~
``` 

Now we are going to start taking the blocks we had in Step 1 and put them into our framework.  

Grab the first two blocks from step 1 and put them in Game On **hat/definition block**. 
```ad-scratch
~~~
define Game on
set [speed y v] to [0]
go to x: (0) y: (100)
~~~
``` 
This sets up or initializes the game
by setting the initial speed y
and putting the player at the center top of the screen.  

Next we do the tick step. 
Take the next block from our game:
```ad-scratch
~~~
change [speed y v] by (-1)
~~~
``` 
and move it to tick:
```ad-scratch
~~~
define tick
change [speed y v] by (-1)
~~~
``` 
Almost done. 
The rest of the code from Step 1 will go into its own myblock.
Here is the hat/definition of that my block.
```ad-scratch
~~~
define Change player y by (speed y) and then pull up -fix overlap
~~~
``` 
Make sure that you add an input called speed y.

You can create this myblock, and the definition will appear there.
Then get a **call block** (*no hat*) for this myblock and put it at the bottom of tick:
```ad-scratch
~~~
define tick
change [speed y v] by (-1)
Change player y by (speed y) and then pull up -fix overlap::custom
~~~
``` 

Now, go back to the **definition block** of Change player y that you created  (this:) 
```ad-scratch
~~~
define Change player y by (speed y) and then pull up -fix overlap
~~~
``` 
You can put the rest of Step 1 below it, 
but you have to change the first 
```ad-scratch
~~~
(speed y)
~~~
``` 
by dragging the red 
```ad-scratch
~~~
(speed y ::custom)
~~~
```  
from the definition into the change y to replace it:
```ad-scratch
~~~
change (y) by (speed y::custom)
~~~
``` 

The rest of Step 1's code goes after this.
```ad-scratch
~~~
if <touching [Platform v]?> then
    repeat until <not <touching [Platform v]?>>
        change y by (1)
    end
    set [speed y v] to [0]
end
~~~

``` 

All done with Step 2.

## Step 3
In Step 3 we take **blue move blocks** such as this one:
```ad-scratch
~~~
set y to (10)
~~~
```
and make them **orange** variable type blocks like this one. 
```ad-scratch
~~~
set (y) to (10)
~~~
```

Later, we will actually **Position** the sprite (use up just the supplies we need), and use the blue blocks like this:
````ad-scratch
```
set y to (y)
```
````
We will do this **Position** step in a special myblock. (don't do it yet)

```ad-tip
title: Why are we doing this?
The framework in Step 2 is a little like a map of a camping trip. The stacks and blocks are the places we will camp along the way. The blue (move) blocks are like using our supplies right away, without thinking about the rest of our trip. The orange (variable) blocks are like keeping track of what supplies we have used and need later, to make sure we know how much we have, and can compare it with how much we need now and on the rest of our trip.
```


Right now, there are 3 places we have to do this.

1. The first is in our old Game On myblock:
````ad-scratch
``` 
define Game on
set [speed y v] to [0]
go to x: (0) y: (100)
```
````

We change the blue block to make it look like this:
````ad-scratch
``` 
define Game on
set [speed y v] to [0]
set [x v] to [0]
set [y  v] to [100]
```
````
Make sure that **x** and **y** are for this sprite only variables.
Notice we used 2 **set** blocks for the one **go to**.

After that, the position step will so something like this:
````ad-scratch
``` 
go to x: (x) y: (y)
```
````
**Don't do it yet.**

First, make the myblock that will do this Position step:
````ad-scratch
``` 
define Position 
go to x: ((x) - (SCROLL X)) y: ((y ) - (SCROLL Y))
```
````
(don't worry about SCROLL X and Y yet)

2. The second place we need to change is the old Change player myblock, change this blue block:
````ad-scratch
``` 
change y by (speed y::custom)
```
````
into this orange block:
````ad-scratch
``` 
change [y  v] by (speed y::custom)
```
````

and the put this Position call block right after it:
````ad-scratch
``` 
Position (at screen x and y)::custom
```
````

3. Lastly, in the platform loop, instead of
````ad-scratch
``` 
change y by (1)
```
````
do this:
````ad-scratch
``` 
change [y  v] by (1)
Position (at screen x and y)::custom
```
````


We need one more Position block. In the Play game stack, after this:
````ad-scratch
``` 
set scroll and position::custom
```
````
put this:
````ad-scratch
``` 
Position (at screen x and y)::custom
```
````

Lastly, let's make tick detect left and right arrow presses:
````ad-scratch
``` 
define tick
if <key [right arrow v] pressed?> then
    change [x v] by (10)
end
if <key [left arrow v] pressed?> then
    change [x v] by (-10)
end
change [speed y v] by (-1)
Change player y by (speed y) and then pull up (fix overlap)::custom
```
````



