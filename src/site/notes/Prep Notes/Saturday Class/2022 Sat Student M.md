---
{"dg-publish":true,"permalink":"/prep-notes/saturday-class/2022-sat-student-m/","dgHomeLink":true,"dgPassFrontmatter":false}
---


# Student M
- [[Prep Notes/Saturday Class/2022 Sat Student M#2022 09 02|2022 09 02]]
	- [[Prep Notes/Saturday Class/2022 Sat Student M#2022 09 02|1 Button Sprite]]
	- [[Prep Notes/Saturday Class/2022 Sat Student M#2022 09 02|Button 2  Sprite]]
	- [[Prep Notes/Saturday Class/2022 Sat Student M#2022 09 02|Button 3]]
	- [[Prep Notes/Saturday Class/2022 Sat Student M#2022 09 02|Control Area Sprite]]
- [[Prep Notes/Saturday Class/2022 Sat Student M#Old stuff|Old stuff]]
- [[Prep Notes/Saturday Class/2022 Sat Student M#2022 08 20|2022 08 20]]
	- [[Prep Notes/Saturday Class/2022 Sat Student M#2022 08 20|TESTER Sprite]]
	- [[Prep Notes/Saturday Class/2022 Sat Student M#2022 08 20|SWORD]]
	- [[Prep Notes/Saturday Class/2022 Sat Student M#2022 08 20|1  Sprite]]
- [[Prep Notes/Saturday Class/2022 Sat Student M#2022 08 13|2022 08 13]]
	- [[Prep Notes/Saturday Class/2022 Sat Student M#2022 08 13|Sword]]



## 2022 09 02

You are almost done with the first part. After this code, we can start customizing it and making it look nice. We can also prepare for the Showcase. 

If we have time, we can work on buttons 2 and 3.


### 1 Button Sprite


```ad-scratch
~~~scratchblock
when this sprite clicked
only if we are using button 1
if <not <(CURRENT BUTTON) = [1]>> then

    broadcast [hide variables v]
    set [CURRENT BUTTON v] to [1]
    show variable [CURRENT BUTTON v]
    start the timer
    broadcast [show timer v]
end
~~~
```

Hide the button when the game starts (for the game intro)

```ad-scratch
~~~scratchblock
when I receive [initialize v]
hide variable [TIME REMAINING v]
hide
~~~
```

This is when the game starts
```ad-scratch
~~~scratchblock
when I receive [show initial game screen v]
show
~~~
```

This is the timer function
```ad-scratch
~~~scratchblock
when I receive [show timer v]
reset timer
set [TIME REMAINING v] to [30]
show variable [TIME REMAINING v]
This will stop timer if time runs out 
or we touch another button
or if we are only checking the current
repeat until <<(timer) > [30]> or <<not <(CURRENT BUTTON) = [1]>> or <not <(CHECKING CURRENT) = [0]>>>>
complicated function shows time easily
    set [TIME REMAINING v] to (join ([floor v] of ((30) - (timer))::operators) (join [.] (letter (length of ([floor v] of ((10) * ((30) - (timer)))::operators)::operators) of ([floor v] of ((10) * ((30) - (timer)))::operators))))
end
When timer is done, check
if <(timer) > [30]> then
    set [CURRENT BUTTON v] to [0]
    broadcast [check current backdrop v] and wait
end
else we don'T check, but hide/stop timer
set [CURRENT BUTTON v] to [0]
hide variable [TIME REMAINING v]

~~~
```

### Button 2  Sprite
Change current button
```ad-scratch
~~~scratchblock
when this sprite clicked
broadcast [hide variables v]
set [CURRENT BUTTON v] to [2]
~~~
```

Hides for opening, shows during game
```ad-scratch
~~~scratchblock
when I receive [initialize v]
hide
~~~
```


```ad-scratch
~~~scratchblock
when I receive [show initial game screen v]
show

~~~
```

### Button 3 
Similar to 2, some things can be copied


```ad-scratch
~~~scratchblock
when this sprite clicked
broadcast [hide variables v]
set [CURRENT BUTTON v] to [3]
~~~
```


```ad-scratch
~~~scratchblock
when I receive [initialize v]
hide
~~~
```


```ad-scratch
~~~scratchblock
when I receive [show initial game screen v]
show
~~~
```
### Control Area Sprite
Hides for opening, shows during game
```ad-scratch
~~~scratchblock
when I receive [initialize v]
hide
go to [back v] layer
~~~
```


```ad-scratch
~~~scratchblock
when I receive [show initial game screen v]
show
~~~
```



---

## Old stuff

## 2022 08 20


> I have added a CHECK COVERAGE sprite that does the checking to see how much of each section is covered. You don't need to code this, but the two key blocks are:  

This checks for how much is drawn:

```ad-scratch
~~~scratchblock
When I receive [check DRAWN v]
~~~
``` 

This checks for how much is not white.
It is used in the begininng to get the initial size of the quadrants.
If you call these, the result goes into the global variable RESULT. 

```ad-scratch
~~~scratchblock
When I receive [check not white v]
~~~
```




### TESTER Sprite

>Create a new sprite called TESTER.
>The Tester Sprite calls the coverage stacks to find out how much each quadrant is covered.
>
>* When the game starts, it gets the initial coverage:
```ad-scratch
~~~scratchblock

when I receive [get initial values v]
clear graphic effects
erase all
set [is clone v] to [0]
switch backdrop to [blank v]
switch costume to [**name of your top left quadrant** v]
show
~~~
```


> * Then, on the same stack, we will:  
>   * show the quadrant and see how much is showing.  
>   * store the RESULT   
> It is important that your 4 quadrant costumes are in the right order in your TESTER sprite.  
  
costume top left:  
```ad-scratch
~~~scratchblock
broadcast [check not white v] and wait
set [QUAD1 FULL v] to (RESULT)
~~~
```

then next is top right:  
```ad-scratch
~~~scratchblock
next costume
broadcast [check not white v] and wait
set [QUAD2 FULL v] to (RESULT)
~~~
```

bottom left:  
```ad-scratch
~~~scratchblock
next costume
broadcast [check not white v] and wait
set [QUAD3 FULL v] to (RESULT)
~~~
```

lastly bottom right:  
```ad-scratch
~~~scratchblock
next costume
broadcast [check not white v] and wait
set [QUAD4 FULL v] to (RESULT)
~~~
```

clear the screen and run the stamp all costumes myblock  
```ad-scratch
~~~scratchblock
erase all
stamp full costumes::custom
~~~
```


> The *stamp full costumes myblock* stamps each quadrant onto the background when the game starts:
```ad-scratch
~~~scratchblock
define stamp full costumes
~~~
```

it clears the screen
```ad-scratch
~~~scratchblock
erase all
switch backdrop to [blank v]
go to x: (0) y: (0)
~~~
```

set up first quadrant
```ad-scratch
~~~scratchblock
switch costume to [top left2 v]
~~~
```

then (4 times) stamps each quadrant costumes
```ad-scratch
~~~scratchblock
repeat (4)
    stamp
    next costume
end

~~~
```


> The way the program works is like this:
> 
> It checks each quadrant to see how much is covered. If more than 80% is covered, it creates a clone that **covers** that quadrant to make it look like it is being eaten. 
> 
> The way it checks the quadrant is by comparing 
> a) how much is drawn when that quadrant is **covering** the drawing 
> b) how much is drawn when that quadrant **not covering** the drawing.
> 
> It does this for each quadrant. This is the myblock that does the comparison:
```ad-scratch
~~~scratchblock
define test coverage of backdrop # (backdrop)
switch costume to (backdrop::custom)
set [ghost v] effect to (0)::looks
show
checks with covering:
broadcast [check DRAWN v] and wait
puts the result into (OUTSIDE OF SEGMENT)
set [OUTSIDE OF SEGMENT v] to (RESULT)
hide
checks without covering.
broadcast [check DRAWN v] and wait


If I subtract `(OUTSIDE OF SEGMENT)` from `(RESULT)` 
I get how much is covering that quadrant, `(QUAD 1)`

~~~
```




> This is the stack that uses this for each quadrant:
```ad-scratch
~~~scratchblock
when I receive [check current backdrop v]
hide
wait (0) seconds
only does this stack for the main sprite, not its clones:
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

~~~
```



> This is the stack that calls that, and is used to check coverage at any moment
```ad-scratch
~~~scratchblock
when [space v] key pressed
broadcast [hide variables v]
~~~
```

this is used to stop the timer if the space is pressed:
```ad-scratch
~~~scratchblock
set [CHECKING CURRENT v] to (1)
~~~
```

this calls the checking stack, which is above:
```ad-scratch
~~~scratchblock
broadcast [check current backdrop v] and wait
reset this variable:
set [CHECKING CURRENT v] to (0)
~~~
```



> This formats the covering clones so they hide the earth a bit
```ad-scratch
~~~scratchblock
when I start as a clone
set [is clone v] to [1]
set [ghost v] effect to (75)::looks
change [whirl v] effect by (100)::looks
set [brightness v] effect to (-50)::looks
show
say (is clone)

when I start as a clone
go to [back v] layer

~~~
```


> All done with the TESTER sprite. 
> 

### SWORD 

> Now, go to the costume editor and move the sword 
> so the point of the sword is at the very center of the sprite.

> Now we are done with the sword, and move on to the 1 sprite 

### 1  Sprite
 
 
> Initialize Sprite 1
```ad-scratch
~~~scratchblock
when I receive [initialize v]
 hide variable [TIME REMAINING v]
 hide
 
when I receive [show initial game screen v]
 show
~~~
```



> When this sprite is clicked, if it is not current, then start this button
```ad-scratch
~~~scratchblock
 when this sprite clicked
 if <not <(CURRENT BUTTON) = [1]>> then
 hide variables, set current, and start the coundown
     broadcast [hide variables v]
     set [CURRENT BUTTON v] to [1]
     show variable [CURRENT BUTTON v]
     broadcast [show timer v]
 end
~~~
```


> This runs the timer
```ad-scratch
~~~scratchblock
when I receive [show timer v]
 reset timer
 set [TIME REMAINING v] to [30]
 show variable [TIME REMAINING v]
We will stop the timer for one of 3 reasons: 
1. the timer runs out 
2. we press another button or 
3. start a check {for example with the space bar}
 repeat until <<(timer) > [30]> or <<not <(CURRENT BUTTON) = [1]>> or <not <(CHECKING CURRENT) = (0)>>
This complicated function is used to make the display of the time look nice:
     set [TIME REMAINING v] to (join ([floor v] of ((30) - (timer))::operators) (join [.] (letter (length of ([floor v] of ((10) * ((30) - (timer)))::operators)::operators) of ([floor v] of ((10) * ((30) - (timer)))::operators))))
 end
If we stopped because of the timer, then calculate the coverage and reset everything
 if <(timer) > [30]> then
     broadcast [check current backdrop v] and wait
     set [CURRENT BUTTON v] to [0]
 end
 once we are done, we do this
 set [CURRENT BUTTON v] to [0]
 hide variable [TIME REMAINING v]
  
~~~
```




## 2022 08 13

### Sword



>  1. Add broadcast and waits for:
> * initialize 
> * get initialize values
> * show initial game screen
> * start game


```ad-scratch
~~~scratchblock
when @greenFlag clicked
broadcast [initialize v] and wait
broadcast [get initial values v] and wait
broadcast [show initial game screen v] and wait
broadcast [start game v] and wait
~~~
```



> 2. Create a new draw routine
> This replaces the old one because
> Using if mouse down is better than if not mouse down
> also, make it draw only on left part of screen

```ad-scratch
~~~scratchblock
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
~~~
```



> 
> 3. Now we set the starting value of the variables when the game starts. 
> 
> Do this in the in the receive initialize stack.
> 
> CURRENT BUTTON is which button we are using.
> DRAWN is how much of the screen we have drawn on.
> 
> The screen is covered by 4 sections. Each of these takes up a certain amount of the screen.
> 
> QUAD FULL are how much of the screen each section uses by itself.
> QUAD is how much of that QUAD is covered by drawing.
> 

```ad-scratch
~~~scratchblock
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
~~~
```





