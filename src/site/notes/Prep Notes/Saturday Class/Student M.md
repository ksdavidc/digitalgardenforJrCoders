---
{"dg-publish":true,"permalink":"/prep-notes/saturday-class/student-m/","dgHomeLink":true,"dgPassFrontmatter":false}
---


# Student M

## 2022 08 20

div class="blocks">

> I have added a CHECK COVERAGE sprite that does the checking to see how much of each section is covered. You don't need to code this, but the two key blocks are:

> 1. this checks for how much is drawn. 
```
When I receive [check DRAWN v]
```

> 2. This checks for how much is not white. (it is used in teh begininng to get the initial size of the quadrants)
```
When I receive [check not white v]
```

> The result from these is the put into the global variable RESULT.



### TESTER Sprite

>The Tester Sprite calls the coverage stacks to find out how much each quadrant is covered.
>
>When the game starts, ti gets the initial coverage:

```
when I receive [get initial values v]
clear graphic effects
erase all
set [is clone v] to [0]
switch backdrop to [blank v]
switch costume to [top left no bg v]
show
we will do this for each quadrant
check not white, and then put the result in the QUAD variable.
costume top left
broadcast [check not white v] and wait
set [QUAD1 FULL v] to (RESULT)
then next is top right:
next costume
broadcast [check not white v] and wait
set [QUAD2 FULL v] to (RESULT)
bottom left:
next costume
broadcast [check not white v] and wait
set [QUAD3 FULL v] to (RESULT)
bottom right:
next costume
broadcast [check not white v] and wait
set [QUAD4 FULL v] to (RESULT)
clear the screen and run the stamp all costumes myblock
erase all
stamp full costumes::custom
```

> The *stamp full costumes* myblock stamps each quadrant onto the background when the game starts:

```
define stamp full costumes
    it clears the screen
erase all
switch backdrop to [blank v]
go to x: (0) y: (0)
    set up first quadrant
switch costume to [top left2 v]
	then 4 times stamps the 4 quadrant costumes
wait (1) seconds
repeat (4)
    stamp
    next costume
end

```

> The way the program works is like this. It checks each quadrant to see how much is covered. If more than 80% is covered, then it creates a clone that covers that quadrant to make it look like it is being eaten. 
> The way it checks the quadrant is by comparing how much is drawn with that quadrant is covering the drawing with how much with the quadrant not covering the drawing. It does this for each quadrant.
> This is the myblock that does the comparison:

```
define test coverage of backdrop # (backdrop)
switch costume to (backdrop::custom)
set [ghost v] effect to (0)::looks
show
broadcast [check DRAWN v] and wait
set [OUTSIDE OF SEGMENT v] to (RESULT)
hide
broadcast [check DRAWN v] and wait

```

> This is the stack that uses this for each quadrant:
```
when I receive [check current backdrop v]
hide
wait (0) seconds
if <(is clone) = [0]> then
    switch backdrop to [blank v]
this hides the background and makes the quadrants visible:    
    set [brightness v] effect to (0)::looks
    hide
We do this 4 times, once for each quadrant:
    set [is clone v] to [top left no bg]
    test coverage of backdrop # (is clone)::custom
    set [QUAD1 v] to ((((RESULT) - (OUTSIDE OF SEGMENT)) / (QUAD1 FULL)) * (100))
    show variable [QUAD1 v]
    if <(QUAD1) > [80]> then
        create clone of [myself v]
    end
number 2
    set [is clone v] to [top right no bg]
    test coverage of backdrop # (is clone)::custom
    set [QUAD2 v] to ((((RESULT) - (OUTSIDE OF SEGMENT)) / (QUAD2 FULL)) * (100))
    if <(QUAD2) > [80]> then
        create clone of [myself v]
    end
    show variable [QUAD2 v]
number 3
    set [is clone v] to [bottom left no bg]
    test coverage of backdrop # (is clone)::custom
    set [QUAD3 v] to ((((RESULT) - (OUTSIDE OF SEGMENT)) / (QUAD3 FULL)) * (100))
    if <(QUAD3) > [80]> then
        create clone of [myself v]
    end
    show variable [QUAD3 v]
number 4
    set [is clone v] to [bottom right no bg]
    test coverage of backdrop # (is clone)::custom
    set [QUAD4 v] to ((((RESULT) - (OUTSIDE OF SEGMENT)) / (QUAD4 FULL)) * (100))
    if <(QUAD4) > [80]> then
        create clone of [myself v]
    end
    show variable [QUAD4 v]
make sure background is blank, reset is clone, and show the variables
    switch backdrop to [blank v]
    set [is clone v] to [0]
    broadcast [show variables v]
end

```


> This can be used to check coverage at any moment
```
when [space v] key pressed
broadcast [hide variables v]
broadcast [check current backdrop v] and wait
```

> This formats the covering clones so they hide the earth a bit
```
when I start as a clone
set [is clone v] to [1]
set [ghost v] effect to (75)::looks
change [whirl v] effect by (100)::looks
set [brightness v] effect to (-50)::looks
show
say (is clone)

when I start as a clone
go to [back v] layer

```


> Go to the costume editor and move the sword so the point of the sword is at the very center of the sprite.

Now we are done with the sword. Move to the 1 sprite 
### 1  Sprite
 
 
> Initialize Sprite 1
```
when I receive [initialize v]
 hide variable [TIME REMAINING v]
 hide
 
when I receive [show initial game screen v]
 show

```


> When this sprite is clicked, if it is not current, then start this button
```
 when this sprite clicked
 if <not <(CURRENT BUTTON) = [1]>> then
 hide variables, set current, and start the coundown
     broadcast [hide variables v]
     set [CURRENT BUTTON v] to [1]
     show variable [CURRENT BUTTON v]
     broadcast [show timer v]
 end
 
 ```

> This is the timer
```
when I receive [show timer v]
 reset timer
 set [TIME REMAINING v] to [30]
 show variable [TIME REMAINING v]
It stops either if the timer runs out or we press another button
 repeat until <<(timer) > [30]> or <not <(CURRENT BUTTON) = [1]>>>
 this complicated function is used to make the display of the time look nice
     set [TIME REMAINING v] to (join ([floor v] of ((30) - (timer))::operators) (join [.] (letter (length of ([floor v] of ((10) * ((30) - (timer)))::operators)::operators) of ([floor v] of ((10) * ((30) - (timer)))::operators))))
 end
 when we are done, if we finished because we ran out of time, then we calculate the time and reset
 if <(CURRENT BUTTON) = [1]> then
     broadcast [check current backdrop v] and wait
     set [CURRENT BUTTON v] to [0]
     hide variable [RESULT v]
     hide variable [CURRENT BUTTON v]
 else
     hide variable [TIME REMAINING v]
 end```
 
```


```
```
```
 create new sprite TESTER and copy all costumes from backdrop to this sprite in same order and with same names
 
 create check current values stack and text coverage of backdrop # myblock
 
 
 
 
 
 copy all the costumes in the backdrop into a new sprite, called TESTER



## 2022 08 13

### Sword



>  Add broadcast and waits for:
> * initialize 
> * get initialize values
> * show initial game screen
> * start game


```
when @greenFlag clicked
broadcast [initialize v] and wait
broadcast [get initial values v] and wait
broadcast [show initial game screen v] and wait
broadcast [start game v] and wait
```


> create a new draw routine
> This replaces the old one because
> Using if mouse down is better than if not mouse down
> also, make it draw only on left part of screen

```
when I receive [start game v]
set pen size to (10)
forever
    if <(CURRENT BUTTON) = [1]> then
        if <<mouse down?> and <(mouse x) < [120]>> then
            go to [mouse-pointer v]
            pen down
            repeat until <not <<mouse down?> and <(mouse x) < [120]>>>
                go to [mouse-pointer v]
            end
            pen up
        end
    end
end
```
> 2.create show variable and hide variables:
> 
> 
> 
> Set the starting value of the variables when the game starts. Do this in the in the receive initialize stack.
> 
> CURRENT BUTTON is which button we are using.
> DRAWN is how much of the screen we have drawn on.
> 
> The screen is covered by 4 sections. Each of these takes up a certain amount of the screen.
> 
> QUAD FULL are how much of the screen each section uses by itself.
> QUAD is how much of that QUAD is covered by drawing.
> 


### Sword

```
when I receive [initialize v]
hide variable [CURRENT BUTTON v]
set [CURRENT BUTTON v] to [0]
set [DRAWN v] to [0]
set [QUAD1 v] to [0]
set [QUAD1 FULL v] to [0]
set [QUAD2 v] to [0]
set [QUAD2 FULL v] to [0]
set [QUAD3 v] to [0]
set [QUAD3 FULL v] to [0]
set [QUAD4 v] to [0]
set [QUAD4 FULL v] to [0]
set [RESULT v] to [0]
```

</div>

