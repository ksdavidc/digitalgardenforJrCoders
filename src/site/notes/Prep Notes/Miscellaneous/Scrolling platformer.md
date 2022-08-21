---
{"dg-publish":true,"permalink":"/prep-notes/miscellaneous/scrolling-platformer/","dgHomeLink":true,"dgPassFrontmatter":false}
---


- [[Prep Notes/Miscellaneous/Scrolling platformer#Step 1|Step 1]]
- [[Prep Notes/Miscellaneous/Scrolling platformer#Step 2|Step 2]]
- [[Prep Notes/Miscellaneous/Scrolling platformer#Step 3|Step 3]]


<div class="blocks">

## Step 1

> first   
> this is the basic falling routine.  
```
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
```

This program works as is, but we will have to give it some structure
 or a framework, so we can make a bigger and faster game. 

## Step 2

>In step 2, we build a framework for our game.  
>This framework helps us keep the code organized.  
>It also makes it easier to adjust and change the code as we need.  

Right off the bat, games work better with just one green flag. 
There is one Master Sprite that controls the others. 
In our game, the Player is the master sprite.
Its one green flag talks to all the other sprites 
using broadcasts, like this:
```
when @greenFlag clicked
broadcast [green flag v] and wait
broadcast [Play Game v]
``` 
go ahead and add that.

As always, a broadcast block is paired with (at least one) receive block.
We will make the ```when I receive [green flag v]``` stack later.

The ```when I receive [Play Game v]``` is the overall project loop. 
This is where we come back to if we want to replay the game.
```
when I receive [Play Game v]
``` 
we add a "Game on" myblock that sets up the game each time we play it.
```
Game on::custom
``` 

````ad-tip
collapse: open
When you see a red block like the one above, 
you may need to create its myblock definition first, if it doesn't already exist.
A myblock has two parts.
First the **definition block**, which is a hat block.
That means it has a round top:
```
define Game on
```
It gets put into your project automatically when you create a new myblock. 
* There is only 1 for each definition. 
* It is always at the top of a stack. 
* It only connects on the bottom.

Then there is the **call block**.
It is not a hat. 
It looks like this:
```
Game on::custom
```
Don't mix them up. 
You need to drag these into your project from the "blocks" area.
* There can be (and often are) more than 1 call block in each sprite.
* It is never at the top of a stack. 
* It can connect on both sides.
````
So, now your **Play Game** stack should look like this:
```
when I receive [Play Game v]
Game on::custom
``` 
Now add these, we will use them later.
```
broadcast [reset level v]
broadcast [set up this level v]
``` 
Next is the main game loop.
The game **repeats** this loop over and over
**until** we lose or win the game.
For now, don't put anything in the brackets \< \>
```
repeat until <>
    Each time through the loop, we figure how much  
    each sprite will change on the screen,  
    and any other changes to the screen. 
    This is called a tick. Like the tick of a clock. (Not the insect, silly.)
    tick::custom
    Then we actually make the changes to the screen, once per frame.
    set scroll and position::custom
    Just add this here, for now.
    broadcast [tick once v] and wait
end
``` 

Now we are going to start taking the blocks we had in Step 1 and put them into our framework.  

Grab the first two blocks from step 1 and put them in Game On **hat/definition block**. 
```
define Game on
set [speed y v] to [0]
go to x: (0) y: (100)
``` 
This sets up or initializes the game
by setting the initial speed y
and putting the player at the center top of the screen.  

Next we do the tick step. 
Take the next block from our game:
```
change [speed y v] by (-1)
``` 
and move it to tick:
```
define tick
change [speed y v] by (-1)
``` 
Almost done. 
The rest of the code from Step 1 will go into its own myblock.
Here is the hat/definition of that my block.
```
define Change player y by (speed y) and then pull up -fix overlap
``` 
Make sure that you add an input called speed y.

You can create this myblock, and the definition will appear there.
Then get a **call block** (*no hat*) for this myblock and put it at the bottom of tick:
```
define tick
change [speed y v] by (-1)
Change player y by (speed y) and then pull up -fix overlap::custom
``` 

Now, go back to the **definition block** of Change player y that you created  (this:) 
```
define Change player y by (speed y) and then pull up -fix overlap
``` 
You can put the rest of Step 1 below it, 
but you have to change the first 
```
(speed y)
``` 
by dragging the red 
```
(speed y)::custom
```  
from the definition into the change y to replace it:
```
change y by (speed y::custom)
``` 

after, this is the rest of step 1's code.
```
if <touching [Platform v]?> then
    repeat until <not <touching [Platform v]?>>
        change y by (1)
    end
    set [speed y v] to [0]
end

``` 

All done with step 2.

## Step 3


In this step we take **blue move blocks** like this:
``` 
set y to (10)
```
and make them **orange** look like
``` 
set (y) to (10)
```

Which, later in the program, 
actually **Position** the sprite using blue blocks like this:
``` 
set y to (y)
```
we will do this **Position** step in a special myblock. (don't do it yet)

For example:

Here is our old Game on:
``` 
define Game on
set [speed y v] to [0]
go to x: (0) y: (100)
```

Now make it look like:
``` 
define Game on
set [speed y v] to [0]
set [x v] to [0]
set [y  v] to [100]
```
Make sure that **x** and **y** are for this sprite only variables.
Notice we used 2 **set** blocks for the one **go to**.

After that, the position step will so something like this:
``` 
go to x: (x) y: (y)
```
**Don't do it yet. **

**First** make the myblock that will do this Position step:
``` 
define Position 
go to x: ((x) - (SCROLL X)) y: ((y ) - (SCROLL Y))
```
(don't worry about SCROLL X and Y yet)

In the  old Change player myblock, change this blue block:
``` 
change y by (speed y::custom)
```

into an orange block:
``` 
change [y  v] by (speed y::custom)
```

and the put the Position call block right after it:
``` 
Position (at screen x and y)::custom
```

In the platform loop, instead of
``` 
change y by (1)
```
do this:
``` 
change [y  v] by (1)
Position (at screen x and y)::custom
```


In the Play game stack:
after 
``` 
set scroll and position::custom
```
add this:
``` 
Position (at screen x and y)::custom
```

Lastly, let's make tick detect left and right arrow presses:
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

```scratchblocks
test
```

```javascript
if () {
test
}
```


</div>

```scratchblocks
test
```

>[!scratch] test
>test 
>```
>test
>```


> [!scratch] 
> ```
> go to x: (0) y: (0)
> ```


````ad-scratch
collapse: open

```
go to x: (0) y: (0)
```
````

```ad-scratch
~~~
go to x: (0) y: (0)
~~~
```

```ad-scratch
collapse: open

~~~
o to x: (0) y: (0)
~~~
```

