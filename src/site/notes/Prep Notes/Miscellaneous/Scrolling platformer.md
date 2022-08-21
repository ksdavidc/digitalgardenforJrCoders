---
{"dg-publish":true,"permalink":"/prep-notes/miscellaneous/scrolling-platformer/","dgHomeLink":true,"dgPassFrontmatter":false}
---


div class="blocks">

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

## Step 2
>Step 1 is  a good beginning, but we will have to change it  
>so that we can make a bigger faster game.   
>  
>In step 2, we build a framework for our game.  
>This framework helps us keep the code organized.  
>It also makes it easier to adjust and change the code as we need.  

Games work better with just one green flag.
We use a broadcast that then goes to every sprite.
```
when @greenFlag clicked
broadcast [green flag v] and wait
broadcast [Play Game v]

``` 
As always, a broadcast block is paired with (at least one) receive block.
We will make the `when I receive [green flag v]`{: .scratch} stack later.

The `when I receive [Play Game v]`{: .scratch} is the overall project loop. 
This is where we come back to if we want to replay the game.
```
when I receive [Play Game v]
``` 
we add a myblock is to initialize each time we play the game.
```
Game on::custom
``` 
> [!info] Note about myblocks:
> When you see a red block like the one above, 
> you may need to create a myblock first, if it doesn't already exist.
> A myblock has two parts.
> First the **definition block**, which is a hat block.
> That means it has a round top:
> ```
> define Game on
> ```
> It gets put into your project when you create a new block.
> 
>  Then there is the **call block**, which is what is above.
>  It is not a hat. Don't mix them up.
>  It looks like this:
> ```
> Game on::custom
> ```
>  You need to drag thest into your project from the "blocks" area.

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
The game repeats this loop over and over
until we lose or win the game.
For now, don't put anything in the brackets < >
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

Grab the first two blocks from step 1 and put them in Game On myblock definition. 
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
and move it to tick.
```
define tick
change [speed y v] by (-1)
``` 
The rest of Step 1 will go into its own myblock.
Here is the hat/definition of that my block.
```
define Change player y by (speed y) and then pull up {fix overlap}
``` 
Make sure that you add an input called speed y.


Then get a call block and put it at the bottom of tick (this is the call part of the myblock):
```
Change player y by (speed y) and then pull up {fix overlap}::custom
``` 

Go back to the definition of Change player y...


```
define Change player y by (speed y) and then pull up {fix overlap}
``` 
You can put the rest of Step 1 below it, 
but you have to change the first speed y, 
by dragging the red input into it.
```
change y by (speed y::custom)
``` 
this is the rest.
```
if <touching [Platform v]?> then
    repeat until <not <touching [Platform v]?>>
        change y by (1)
    end
    set [speed y v] to [0]
end

``` 

</div>

