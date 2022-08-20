---
{"dg-publish":true,"permalink":"/prep-notes/miscellaneous/scrolling-platformer/","dgHomeLink":true,"dgPassFrontmatter":false}
---


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

## Step 2
>Step 1 is  agood beginning, but we will have to change it  
>so that we can make a bigger faster game.   
>  
>In this step we build a framework for our game.  
>This framework helps us keep the code organized.  
>It also makes it easier to adjust and change the code as we need.  

Games work better with just one green flag.
We use a broadcast that then goes to every sprite.
```
when @greenFlag clicked
broadcast [green flag v] and wait
broadcast [Play Game v]

``` 
This is the overall game loop. 
This is where we come back to if we want to replay the game.
```
when I receive [Play Game v]
``` 
This myblock is to initialize each time we play the game.

```
Game on::custom
``` 

> [!info] Note about myblocks:
> When you see a red block like the one above, you may need to create a myblock.
> A myblock has two parts.
> First the definition block, which is a hat block.
> It has a round top:
> ```
> define Game on
> ```
> and then, the call block, which is what is above. It is not a hat. Don't mix them up.



Just add these, we will use them later.
```
broadcast [reset level v]
broadcast [set up this level v]
``` 
Next is the main game loop.
The game repeats this loop over and over
until we lose or win the game.
for now, don'T put anything in the brackets < >
```
repeat until <>
``` 
Each time through the loop, we figure how much
each sprite will change on the screen, and any other changes to the screen. 
This is a tick. Like the tick of a clock. Not the insect, silly.
```
    tick::custom
``` 
Then we actually make the changes to the screen, once per frame.
```
    set scroll and position::custom
``` 
Just add this here, for now.
```
    broadcast [tick once v] and wait
end

``` 

Now we are going to start taking the blocks we had in Step 1 and put them into our framework.

Grab the first two blocks from step 1 and put them in Game On myblock definition. 
This sets up or initializes the game
by setting the initial speed y
and putting the player at the center top of the screen.
```
define Game on
set [speed y v] to [0]
go to x: (0) y: (100)

``` 
Next we do the tick step. 
The next block from our game,
```
change [speed y v] by (-1)
``` 
goes in tick.
```
define tick
change [speed y v] by (-1)
``` 
The rest of Step 1 will go into its own myblock.
Here is the definition of that my block.
Make sure that you add an input called speed y.
```
define Change player y by (speed y) and then pull up {fix overlap}
``` 
Then add this at the bottom of tick:
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