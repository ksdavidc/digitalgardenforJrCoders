---
{"dg-publish":true,"permalink":"/prep-notes/friday-class/2022-student-k-flappy-bird/","dgHomeLink":true,"dgPassFrontmatter":false}
---


## Step 1 Gravity
First we just create gravity.
Create your  **Bird Sprite**, and add this code.


```ad-scratch
~~~scratchblock
when @greenFlag clicked
forever
    change y by (-2)
    wait (.1) seconds
end

when [space v] key pressed::event
change y by (35)
~~~
```



## Step 2a Walls

Create one set of walls, and add this code in the wall sprite


```ad-scratch
~~~scratchblock
when @greenFlag clicked
go to x: (575) y: (0)
forever
    change x by (((-4) * <(x position) \> [-300]>) + ((640) * <not <(x position) \> [-300]>>))
end
~~~
```


## Step 2b Use broadcast
This has 5 parts.

1. In the Bird sprite, we have 

```ad-scratch
~~~scratchblock
when @greenFlag clicked
forever
    change y by (-2)
    wait (.1) seconds
end

~~~
```

We 
1. **Break** the green flag and forever apart 
2. **Insert** a message/receive pair (`Main Loop`).

This creates the **Gravity Main Loop**.

```ad-scratch
~~~scratchblock
when @greenFlag clicked
broadcast [Main Loop v]


when I receive [Main Loop v]
forever
    change y by (-2)
end

~~~
```

2. Now we **break and insert** again. This time we insert a `Game Start` message. We take the green flag stack:

```ad-scratch
~~~scratchblock
when @greenFlag clicked
broadcast [Main Loop v]
~~~
```

We break it apart and insert to create the **Game Start Stack**.

```ad-scratch
~~~scratchblock
when @greenFlag clicked
broadcast [Game start v]

This is the Game Start Stack
when I receive [Game start v]
broadcast [Main Loop v]

~~~
```


3. Next, initialize your bird in the **Game Start Stack**. Here I set the size. You can also set the position, direction, and so on.

```ad-scratch
~~~scratchblock
when I receive [Game start v]
set size to (40) %
broadcast [Main Loop v]
~~~
```


4. The bird begins falling in the **Gravity Main Loop**. He should start from  the left middle of the screen. To put him there, add a glide to the Gravity Main Loop.

```ad-scratch
~~~scratchblock
when I receive [Main Loop v]
glide (1) secs to x: (-156) y: (13)
forever
    change y by (-2)
end
~~~
```


5. If you want to make your costume change, add ANOTHER second different Main loop to change the costume. This is the **Costume Main Loop**. Why two Main Loops? Since they start at the same time. Remember, a single broadcasts can go be received in many places.

```ad-scratch
~~~scratchblock
this is a SECOND different receive main loop stack!!!
when I receive [Main Loop v]
forever
    next costume
    wait (.1) seconds
end
~~~
```

## Step 3a Repeat Until Touching Wall

We don't really want the bird to fly forever. We want him to stop flying when he hits a wall. So we will change the `forever` loops to `repeat until touching wall` loops.


```ad-scratch
~~~scratchblock
when I receive [Main Loop v]
show
glide (1) secs to x: (-156) y: (13)
repeat until <touching [wall v]?>
    change y by (-2)
end


when I receive [Main Loop v]
repeat until <touching [wall v]?>
    next costume
    wait (.1) seconds
end
~~~
```

## Step 3b Game Start Game Over

To start the game, you have to click the Bird. Here's how.

In the **Game Start Stack**:

```ad-scratch
~~~scratchblock
when I receive [Game start v]
set size to (40) %
go to x: (-118) y: (-127)
We show the bird and the bird tells the user to click.
show
say [Click Me To Play]
We wait until the mouse is down and touching the bird. This is the same as a click.
wait until <<touching [mouse-pointer v]?> and <mouse down?>>
We clear the text bubble.
say []
broadcast [Main Loop v]

~~~
```

When we have touched a wall, the game is over, so we broadcast the game over message. We also stop the bird from moving any more and we want him to disappear.

```ad-scratch
~~~scratchblock
when I receive [Main Loop v]
show
glide (1) secs to x: (-156) y: (13)
repeat until <touching [wall v]?>
    change y by (-2)
end
add these blocks
say [Game over!]
broadcast [Game Over v]
stop [this script v]


when I receive [Game Over v]
hide
~~~
```

Create a **Game Over Sprite** to show your game over message. Mine is a beachball. In that sprite we can put a simple game over message. 

```ad-scratch
~~~scratchblock
when I receive [Game Over v]
switch costume to [beachball v]
show
say [Game Over]
broadcast [Game start v]

~~~
```

Notice that we also restart the game. This is why we created a **Game Start Stack**. That stack will restart (reset) the game and wait for us to click the bird again. But in our **Game Over Sprite** we will need to hide the Game over message once the main loop starts:


```ad-scratch
~~~scratchblock
when I receive [Main Loop v]
hide
~~~
```

We also need to tell the walls that the game is over. Go to the **Wall Sprite** and add this:

```ad-scratch
~~~scratchblock
when I receive [Game Over v]
stop [other scripts in sprite v]
hide
~~~
```

## Step 4 (optional) Add music

This is optional, and I will not explain it completely.

If you want to add music, this is the way to do it. Pick 2 songs and put them somewhere. The bird is okay, or a dedicated sound sprite. One is for playing during the main loop (track 1), and the other is for the end of the game (track 2). 

```ad-scratch
~~~scratchblock


define Play Track (n)
This is the Music Player. It knows when to stop and which track to play and how to repeat itself.
It is possible to add more tracks but I haven't done it.
repeat until <(music is stopped?) = [1]>
    play sound ((music is stopped?) + (n::custom)) until done
end


define stop/restart music
this stops any music that is playing
stop all sounds
this turn off the Music Player
set [music is stopped? v] to [1]
It needs a moment to do it.
wait (0) seconds
This turns the Music Player on again, so it can play again.
set [music is stopped? v] to [0]

This is how we stop and start the music

when I receive [Main Loop v]
stop/restart music::custom
Play Track [1]::custom


when I receive [Game Over v]
stop/restart music::custom
Play Track [2]::custom


~~~
```


## Step 5a Add Flames

When we jump, we broadcast `jump`. `Jump` will tell the flames to move.

```ad-scratch
~~~scratchblock
when [space v] key pressed::event
broadcast [jump v]
change y by (35)

~~~
```

Now make the Flame Sprite. You can use 1 flame sprite with two fires, or two flame sprites, one on each leg, each with one fire. 

Make sure the flames are centered in costume editor. THen

The way this works is we go to the hero (`Hero` is the name of my bird ), and then move a little down and a little left of right so the flames are just at his feet. Doing this every time makes the flames "follow" the bird. Also, we can cycle the costumes here.

```ad-scratch
~~~scratchblock
when I receive [jump v]
You have to choose the right direction. 
Mine is 52 because my bird's legs are bent.
point in direction (52)
'hero' is the name of my bird
go to [hero v]
show
repeat (2)
    You have to change these numbers to get the position right.
    THey will be different on the right and left flame.
    go to x: (([x position v] of [hero v]::sensing) + (24)) y: (([y position v] of [hero v]::sensing) - (35))
    next costume
end
hide
~~~
```

Be sure to hide them when the game starts and stop them when the game is over.

```ad-scratch
~~~scratchblock
when I receive [Game start v]
hide


when I receive [GameOver v]
stop [other scripts in sprite v]


~~~
```



## Step 5b Use Mouse to Jump

It turns out we want to jump by using the mouse as well as the space. **In the Bird Sprite:**

1. We add an if statement to detect the mouse or space.
2. We put the blcks that make the jump (`broadcast` and `change y`) inside this.
3. If we put the next costume step inside it, the character will only flap its wings when it is jumping.
4. if we add an else, we can make sure it has the same costume when it is not flying.

```ad-scratch
~~~scratchblock
when I receive [Main Loop v]
repeat until <touching [wall v]?>
    if <<mouse down?> or <key [space v] pressed?>> then
        broadcast [jump v]
        change y by (8)
        next costume
    else
        switch costume to [not flying v]
    end
end
~~~
```

Because we are doing this we don't need this anymore.

```ad-scratch
~~~scratchblock
Delete this whole stack from step 5a
when [space v] key pressed::event
broadcast [jump v]
change y by (35)

~~~
```


## Step 6 (Optional) Make a Game Over Effect 

Create your own special Game over effect. This is the one I use, but you can make a simpler one.

```ad-scratch
~~~scratchblock
when I receive [Game Over v]
erase all

switch costume to [beachball v]
show
go to x: (-240) y: (-50)
this is the game over routine:
set [spacing v] to [8]
set [n v] to [1]
jump [4] times::custom
go to x: (-240) y: (-200)
jump [4] times::custom
end of routine
hide
broadcast [Game start v]

define iterate (n ) times
repeat (n ::custom)
    change [T v] by (-1)
    change y by ((T) * (5))
    change x by (spacing)
end

define one jump
set [T v] to [8]
change [n v] by (1)
iterate [8] times::custom
stamp with costume (n)::custom
iterate [7] times::custom

define stamp with costume (n)
switch costume to (n::custom)
pen down
stamp
pen up
switch costume to [beachball v]

define jump (n ) times
repeat (n ::custom)
    one jump::custom
end

when I receive [Main Loop v]
erase all
hide
~~~
```


## Step 7 add more walls

In the wall sprite, add your costumes then add one block in the forever loop:

```ad-scratch
~~~scratchblock
when I receive [Main Loop v]
show
go to x: (575) y: (0)
forever
    add this
    switch costume to ((costume [number v]) + <not <(x position) \> [-300]>>)
    change x by (((-5) * <(x position) \> [-300]>) + ((640) * <not <(x position) \> [-300]>>))
end
~~~
```

This will loop through the costumes forever, in the order you put them. 

