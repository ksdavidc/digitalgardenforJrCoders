---
{"dg-publish":true,"permalink":"/digital-garden/hatlink-part-2/"}
---

I assume you have made [[Digital Garden/Hatlight Platformer Step 1|Hatlight Platformer Step 1]].

In that we had a jump routine, but it was a temporary solution. 

Here are some problems to notice:

* If you jump below a platform, the sprite is pushed up through the platform. Instead, it is more realistic for the sprite to bounce.
* And, while you are inside that platform you can move left to right. That is also unrealistic.
* The when up arrow stack lets you jump in mid-air. We used this to fix that:
```ad-scratch
title: 
~~~scratchblock
wait until < ([abs v] of (y speed)) < (8)>
~~~
```
* Still, the jump is "wobbly". 
* Right now we fall in steps, but our jump routine makes a big step up when we jump. We are going to jump in steps as well, so that we can detect platforms. 

## Distance to the ground
The first step we will take is to keep track of our distance to the ground. 
1. create a variable `distance to ground`
2. initialize it in the initialize routine:

```ad-scratch
title: hitbox, initialize stack 
~~~scratchblock
when I receive [initialize v]
...
set [distance to ground v] to [0]
...
~~~
```

Next we change `distance to ground` inside the `change y by xspeed...` stack. Note that we duplicate the condition in the `change y block`, so the two change the same way.

```ad-scratch
title: hitbox, define change y by (yspeed)
~~~scratchblock
define change y by (yspeed) by single steps
repeat ([abs v] of (yspeed::custom)::operators)
    change [distance to ground v] by ((-1) * <not <touching [walls v]?>>)
    change y by ((-1) * <not <touching [walls v]?>>)
end
~~~
```

we also change  `pull out if touching...` but in a slightlly different way. Here we want to make sure that the distance to the ground will be zero when we are done  pulling out (which means touching the wall and falling). Therefore we multiply the condition by `-1 * distance to ground`. This cancels whatever value is in there.

```ad-scratch
title: hitbox, define pull up
~~~scratchblock
define pull up or down if touching walls and <falling?> or not
change [y speed v] by (<touching [walls v]?> * ((-1) * (y speed)))
change [distance to ground v] by (<touching [walls v]?> * (<falling?::custom> * ((distance to ground) * (-1))))
change y by (<touching [walls v]?> * (falling?::custom)
~~~
```

Notice that:
```ad-scratch
~~~scratchblock
change [distance to ground v] by (<touching [walls v]?> * (<falling?::custom> * ((distance to ground) * (-1))))
~~~
```
is the same as, but all in one line:
```ad-scratch
~~~scratchblock

  
if <(<falling?::custom> * <touching [walls v]?>) = (1)> then
    set [distance to ground v] to (0)
end

~~~
```

## Change jump routine
Now we can change the jump routine so that we only jump when we are close to the ground.

First, to make sure we are only jumping at the right time, let's change from a `when up arrow pressed` to `receive jump`. Delete **this entire stack**:

```ad-scratch
title: hitbox, when up arrow stack
~~~scratchblock
when [up arrow v] key pressed
...
~~~
```

and replace it with:

```ad-scratch
title: hitbox, jump stack
~~~scratchblock
when I receive [jump v]
if <key [up arrow v] pressed?>  then
    change [y speed v] by ((20) * <(distance to ground) \< [5]>)
    change [distance to ground v] by ((20) * <(distance to ground) \< [5]>)
end
broadcast [move left / right v]
~~~
```
This changes the speed by 20 only if we are close to the ground.

Then change the `broadcast` at the bottom of fall like this:

```ad-scratch
title: hitbox, fall stack
~~~scratchblock
not
broadcast [move left / right v]

instead
broadcast [jump v]

~~~
```
Run it to test it. Is it working still? 

No, it shouldn't. We have one more thing to do. The problem is that, as I wrote above,

* Right now we fall in steps, but our jump routine makes a big step up when we jump. We are going to jump in steps as well, so that we can detect platforms. 

So, how do we do that? We keep track of whether we are falling by making a new variable to keep track of the sign:

```ad-scratch
title: 
~~~scratchblock
set [sign of y speed v] to (<(y speed) \> [0]> - <(y speed) \< [0]>)
~~~
```
This will be **1** if we are jumping and **-1** if we are falling. Then we put this is in the change y by stack, and change **-1** to `sign of y speed`. 


```ad-scratch
title: hitbox, define change y by (yspeed)
~~~scratchblock
define change y by (yspeed) by single steps
set [sign of y speed v] to (<(y speed) \> [0]> - <(y speed) \< [0]>)
repeat ([abs v] of (yspeed::custom)::operators)
    change [distance to ground v] by ((sign of y speed) * <not <touching [walls v]?>>)
    change y by ((sign of y speed) * <not <touching [walls v]?>>)
end
~~~
```

That should work. You might have to change the numbers in the **jump stack** for the  `change y speed` and `distance to ground` block to make it work. Things like the size of your hitbox and what your platform looks like can make a difference.

```ad-scratch
title: 
~~~scratchblock
define begin scene (scene) in direction (x)
if <> then
simplified from griffpatch e2 :: custom #002c3d
set x to ((x::custom) * (233))
end
set [screen v] to (scene::custom)
broadcast [new screen v]
stop [other scripts in sprite v]
wait (0) seconds
Fix collisions in [0]::custom
run ({create clone :: control} @addInput :: grey ring) :: control
<() @addInput :: grey ring>
say (http:// [snap.berkeley.edu] :: sensing)
((6) × (7) :: operators)
(join [hello ] [world] @delInput @addInput :: operators)
script variables ((foo) :: grey) ((bar) :: grey) @delInput @addInput :: grey
(all but first of @list :: list)
warp {
move (10) steps
} :: grey
report [Done!] :: control cap
(<> @addInput) // without even the :: grey ring
~~~
```




```ad-scratch
title: 
~~~scratchblock
@stopSign ghi :: pen reporter #1234FF
~~~
```


when @greenFlag clicked
set [mode v] to [0]
broadcast [initialize v]

when I receive [move left / right v]
set xspeed::custom
change x by (x speed)
broadcast [wrap v]

when I receive [wrap v]
if <(x position) \> [238]> then
    begin scene ((screen) + (1)) goto x [-1]::custom
else
    if <<(x position) \< [-238]> and <(screen) \> [1]>> then
        begin scene ((screen) + (-1)) goto x [1]::custom
    end
end
broadcast [climb v]

when I receive [climb v]
set [lifted up v] to [0]
climb::custom
broadcast [fall v]

when I receive [fall v]
change [y speed v] by (-1)
change y  by (y speed) by single steps::custom
pull up or down if touching walls and <(y speed) \< [0]> or not::custom
broadcast [check lava v]

when I receive [jump v]
if <<<key [up arrow v] pressed?> or <key [space v] pressed?>> or <key [z v] pressed?>> then
    /: [only jump if near the ground]::custom
    change [y speed v] by ((4) * <(distance to ground) \< [5]>)
end
start sound [jump v]
broadcast [move left / right v]

define anothe ray to set the xspeed and facing
change [x speed2 v] by ((<(x speed2) \< [0]> - <(x speed2) \> [0]>) * <<not <key [left arrow v] pressed?>> and <not <key [right arrow v] pressed?>>>)
change [x speed2 v] by (<key [right arrow v] pressed?> - <key [left arrow v] pressed?>)
change [x speed2 v] by (((4) - (x speed2)) * <(x speed2) \> [4]>)
change [x speed2 v] by (((-4) - (x speed2)) * <(x speed2) \< [-4]>)
change [facing2 v] by (((1) - (facing2)) * <key [left arrow v] pressed?>)
change [facing2 v] by (((2) - (facing2)) * <key [right arrow v] pressed?>)

define pull up or down if touching walls and <falling?> or not
if <touching [Lava v]?> then
    change y by (1)
    broadcast [touching lava v]
end
change [distance to ground v] by (1)
/: [if touching a wall and falling, set distance to 0, else keep the same]::custom
change [distance to ground v] by (<touching [walls v]?> * (<falling?::custom> * ((distance to ground) * (-1))))
/: [if touching a wall, set y speed to zero, else keep the same]::custom
change [y speed v] by (<touching [walls v]?> * ((-1) * (y speed)))
/: [if touching a wall, go up if falling, down if jumping]::custom
change y by (<touching [walls v]?> * (<falling?::custom> - <not <falling?::custom>>))



define set xspeed
if <<not <key [left arrow v] pressed?>> and <not <key [right arrow v] pressed?>>> then
    change [x speed v] by (<(x speed) \< [0]> - <(x speed) \> [0]>)
else
    change [x speed v] by (<key [right arrow v] pressed?> - <key [left arrow v] pressed?>)
end
set [sign of x v] to (<(x speed) \> [0]> - <(x speed) \< [0]>)
if <(x speed) \> [4]> then
    set [x speed v] to [4]
end
if <(x speed) \< [-4]> then
    set [x speed v] to [-4]
end

when I receive [initialize v]
say []
switch costume to [costume1 v]
set size to (((64) / (44)) * (50)) %
set [ghost v] effect to (90)::looks
set [color v] effect to (25)::looks
go to x: (-205) y: (65)
set [x speed v] to [0]
set [x speed2 v] to [0]
set [y speed v] to [0]
set [grounded v] to [0]
set [screen v] to [0]
set [distance to ground v] to [0]
set [touched lava v] to [0]
broadcast [move left / right v]

define change costume 2
if <([abs v] of (x speed)::operators) \> [0]> then
    point in direction ((sign of x) * (90))
    next costume
else
    switch costume to [costume1 v]
end

when I receive [touching lava v]
if <(mode) = [0]> then
    set [touched lava v] to [1]
end

when I receive [check lava v]
if <(touched lava) = [1]> then
    set y to (65)
    broadcast [set scene v]
end
broadcast [jump v]

when [e v] key pressed::event
change [mode v] by (<(mode) = [0]> - <(mode) = [1]>)

define begin scene (scene) goto x (x)
/: [simplified from griffpatch e2]::custom
set x to ((x::custom) * (233))
set [screen v] to (scene::custom)
broadcast [new screen v]
stop [other scripts in sprite v]
wait (0) seconds
Fix collisions in [0]::custom

define Fix collisions in (direction)
set [distance v] to [1]
point in direction (direction::custom)
repeat (64)
    if <not <touching [walls v]?>> then
        stop [this script v]
    end
    move (distance::variables) steps
    turn @turnRight (180) degrees::motion
    change [distance v] by (1)
end

when I receive [set scene v]
set x to (-233)
set [touched lava v] to [0]
broadcast [move left / right v]

define climb
repeat (4)
    if <touching [walls v]?> then
        change y by (.5)
        change [lifted up v] by (-.5)
    end
end
point in direction (last angle)
if <touching [walls v]?> then
    change x by ((x speed) * (-1))
    change y by (lifted up)
    if <touching [walls v]?> then
        change x by (-3)
        if <touching [walls v]?> then
            change x by (6)
        end
    end
    set [x speed v] to [0]
    set [x speed2 v] to [0]
end

```ad-scratch
title: 
~~~scratchblock
define change y  by (yspeed) by single steps
1 for going up, -1 for going down, 0 if still
set [sign of y speed v] to (<(y speed) \> [0]> - <(y speed) \< [0]>)
repeat ([abs v] of (yspeed::custom)::operators)
    change y by ((sign of y speed) * <not <<touching [walls v]?> or <<touching [Lava v]?> and <(mode) = [1]>>>>)
end
at this point we are either mid air or just touching wall

~~~
```