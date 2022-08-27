---
{"dg-publish":true,"permalink":"/prep-notes/monday-class/2022-monday-class-kitten-parachute-game/","dgHomeLink":true,"dgPassFrontmatter":false}
---


# 2022 Kitty Parachute Game
- [[Prep Notes/Monday Class/2022 Monday Class Kitten Parachute Game#2022 08 08|2022 08 08]]
- [[Prep Notes/Monday Class/2022 Monday Class Kitten Parachute Game#2022 08 01|2022 08 01]]
	- [[Prep Notes/Monday Class/2022 Monday Class Kitten Parachute Game#2022 08 01|CLOUD SPRITE]]
	- [[Prep Notes/Monday Class/2022 Monday Class Kitten Parachute Game#2022 08 01|GROUND SPRITE]]
	- [[Prep Notes/Monday Class/2022 Monday Class Kitten Parachute Game#2022 08 01|KITTY]]
	- [[Prep Notes/Monday Class/2022 Monday Class Kitten Parachute Game#2022 08 01|DIFFICULTY SPRITE]]
- [[Prep Notes/Monday Class/2022 Monday Class Kitten Parachute Game#July 25th|July 25th]]
	- [[Prep Notes/Monday Class/2022 Monday Class Kitten Parachute Game#July 25th|KITTY SPRITE]]
	- [[Prep Notes/Monday Class/2022 Monday Class Kitten Parachute Game#July 25th|UPDRAFT SPRITE]]



## 2022 08 08





This week we take blocks like this:

```ad-scratch
~~~scratchblock
set y to (10)
~~~
```

and make them look like
```ad-scratch
~~~scratchblock
set {y position variable} to (10)
change y by (y position variable) 
~~~
```


1. create blank sprite

2. do this:

```ad-scratch
~~~scratchblock
define Change player y by (speed y) and then pull up (fix overlap)
change y by (speed y::custom)
// [is this if necessary?]::custom
// [old version of change player loop]::custom
if <touching [Platform v]?> then
    repeat until <not <touching [Platform v]?>>
        change y by (1)
    end
    set [speed y v] to [0]
end
~~~
```


```ad-scratch
~~~scratchblock
when @greenFlag clicked
broadcast [green flag v] and wait
broadcast [Play Game v]
~~~
```


```ad-scratch
~~~scratchblock
when I receive [Play Game v]
Game on::custom
broadcast [rl4 v]
broadcast [su4 v]
// [** this surround tick to broadcast tick once]::custom
repeat until <>
    tick::custom
    set scroll and position::custom
end
~~~
```


```ad-scratch
~~~scratchblock
define Game on
set [speed y v] to [-1]
go to x: (0) y: (100)
~~~
```


```ad-scratch
~~~scratchblock
define tick
change [speed y v] by (-1)
Change player y by (speed y) and then pull up (fix overlap)::custom
~~~
```


```ad-scratch
~~~scratchblock
define Position (at screen x and y)
// [since the game player x and the game scroll x are the same, this is 0]::custom
go to x: ((player game x) - (SCROLL X)) y: ((player game y) - (SCROLL Y))
// [** goes in change player y by speed y at end of repeat until loop]::custom
set [in air v] to [0]
~~~
```


```ad-scratch
~~~scratchblock
define set scroll and position
// [will have stuff later]::custom
~~~
```


```ad-scratch
~~~scratchblock
define Is touching level?
set [touching level v] to ((1) * <touching [Platform v]?>)
~~~
```


## 2022 08 01 


### CLOUD SPRITE



at the end of the New sky stack, add this
to make sure the cloud hides when the round is over:

```ad-scratch
~~~scratchblock
hide

~~~
```


We want a bit of a see-through effect
so the player is looking through the cloud.
Add this stack:
```ad-scratch
~~~scratchblock
when I receive [initialize v]
set [ghost v] effect to (25)::looks
hide
~~~
```


add this as a new stack
```ad-scratch
~~~scratchblock
to make sure the cloud is hidden at the beginning of the game:
when I receive [choose difficulty v]
hide
~~~
```





### GROUND SPRITE




remove this
```ad-scratch
~~~scratchblock
change[SKY# v] by (-1)
~~~
```

since we will change the SKY# in the kitty sprite instead

and add this as a new stack
This makes sure the game restarts at the last sky, and that the ground is in back
behind the choose difficulty screen:
```ad-scratch
~~~scratchblock
when I receive [choose difficulty v]
set [SKY# v] to [8]
go to [back v] layer
hide
~~~
```





### KITTY

add this as a new stack
we are fixing the transition from one sky to the next:
```ad-scratch
~~~scratchblock
when I receive [ready for new sky? v]
set [ROUND OVER v] to [0]
change [SKY# v] by (-1)
~~~
```

(we removed this from the cloud, remember?)
```ad-scratch
~~~scratchblock
broadcast [New sky v]
~~~
```


add this as a new stack
```ad-scratch
~~~scratchblock
when I receive [Landed v]
wait (0.05) seconds
When we land, we create a little dance:
ending dance::custom
reset timer
wait (0) seconds
repeat until <<mouse down?> or <<key [space v] pressed?> or <(timer) > [8]>>>
    broadcast [Announce Score v]
    say (join [Ending game in ] (join ((8) - (round (timer))) [ seconds. Click or Press space key to restart instead.]))
end
if <<mouse down?> or <key [space v] pressed?>> then
    stop [other scripts in sprite v]
    broadcast [Game Loop v]
    hide variable [DIFFICULTY SAY v]
    say []
end
~~~
```


define ending dance
** MAKE THIS YOURSELF **
*** use blocks like:
```ad-scratch
~~~scratchblock
change x by ()
change y by ()
repeat () times
change .... effect
change size 
go to x: () y: ()
glide
~~~
```

or any thing else you like
***


and this new stack:
```ad-scratch
~~~scratchblock
when I receive [Announce Score v]
hide variable [SCORE v]
set [DIFFICULTY SAY v] to (join [𝚈𝚘𝚞 𝚑𝚊𝚟𝚎 𝚊 𝚝𝚘𝚝𝚊𝚕 𝚘𝚏 ] (join (SCORE) [ 𝚙𝚘𝚒𝚗𝚝𝚜 ]))
show variable [DIFFICULTY SAY v]
~~~
```



and this as a new stack:
```ad-scratch
~~~scratchblock
when I receive [Game Over v]
say [Bye] for (2) seconds
change [ROUND OVER v] by (1)
set y to (-82)
stop [all v]
~~~
```





### DIFFICULTY SPRITE


create a new  my block
define position difficulty


take these four blocks from  initialize stack:
```ad-scratch
~~~scratchblock
go to x: (-200) y: (100)
clear graphic effects
set size to (400) %
hide
~~~
```

and put them on the position difficulty stack

add one of these: 
```ad-scratch
~~~scratchblock
position difficulty::custom
~~~
```

to 
1. the initialize stack and 
2. as the first block on the 
```ad-scratch
~~~scratchblock
when I receive [choose difficulty v]
~~~
```

stack.



## July 25th


### KITTY SPRITE


1. First we are going to creat a game loop. 
then we can replay the game at the end. 

To do that we will divide this main game stack into two stacks. 

first find this block:
```ad-scratch
~~~scratchblock
When green flag clicked
broadcast [initialize v] and wait
~~~
```

and AFTER IT PUT THIS BLOCK:
```ad-scratch
~~~scratchblock
broadcast [Game Loop v]
~~~
```


Then we make a new stack, which will be the game loop. 
This is where we restart the game from. 
Add this block:
```ad-scratch
~~~scratchblock
when I receive [Game Loop v]
~~~
```

And move all 5 of these blocks, 
{**they are from the green flag above**} 
onto the  {when I receive \[Game Loop v\] } 
```ad-scratch
~~~scratchblock
broadcast [add music v]
broadcast [choose difficulty v] and wait
wait until <(DIFFICULTY) > [0]>
broadcast [Countdown v] and wait
broadcast [Start v] and wait
~~~
```

Then we are going to add two blocks on the end...
1. The first will make a landing effect, and replay if you tell it to
```ad-scratch
~~~scratchblock
broadcast [Landed v] and wait
~~~
```

2. Then, if you don't replay,
this block will make the game really over:
```ad-scratch
~~~scratchblock
broadcast [Game Over v]
~~~
```


Now go to the updraft sprite and follow the next set of directions





### UPDRAFT SPRITE



1. After this block:
```ad-scratch
~~~scratchblock
clear graphic effects
~~~
```

we are going to insert some blocks here. 
First, we delete any clones that might be left over 
from the last time the game was played. 
Add this: {note there is NOTHING in the not block}
```ad-scratch
~~~scratchblock
if <not <>> then
    delete this clone
end
~~~
```

Then we make the updraft go to the front:
```ad-scratch
~~~scratchblock

go to [front v] layer
~~~
```

at some random position: 
```ad-scratch
~~~scratchblock
go to [random position v]
~~~
```

When it is there, create a clone. This "shadow-clone" is the updraft's shadow.
```ad-scratch
~~~scratchblock
create clone of [myself v]
~~~
```

Keep this block that was there before:
```ad-scratch
~~~scratchblock

show
~~~
```

We also want the updraft to move around the screen, 
so add this onto the show block:
```ad-scratch
~~~scratchblock

broadcast [move updraft v]
~~~
```


Why a broadcast, instead of just putting the code here?
Because then it will act on both 
the updraft AND the clone at the same time. 
This stack is only working on the mother 
{because we deleted the leftover clones at the top...}


2. Before we do the code to move the updraft and its shadow,
let's make the shadow clone look right.  
To control the shadow-clone one of these blocks: 
```ad-scratch
~~~scratchblock
when I start as a clone
~~~
```

We want the clones to look like shadows, so we do a couple of things:
1. put the clone behind the mother updraft
```ad-scratch
~~~scratchblock
go [backward v] (1) layers
~~~
```

2. Make it black like a shadow:
```ad-scratch
~~~scratchblock
set [brightness v] effect to (-100)::looks
~~~
```

3. but add a little transparency:
```ad-scratch
~~~scratchblock
set [ghost v] effect to (75)::looks
~~~
```

we offset it a little bit, so it looks like a shadow
```ad-scratch
~~~scratchblock
change x by (2)
change y by (-2)
~~~
```

and then finally, we make sure it is showing:
```ad-scratch
~~~scratchblock
show
~~~
```


Now, at last we can make the updraft and its shadow move. 
Remember this stack is working on both of them, 
so they will always both move together.
First we create the partner to the broadcast above, that is the receive block:
```ad-scratch
~~~scratchblock
when I receive [move updraft v]
~~~
```

We want to keep them moving up until either:
a) they they the top OR
b) the round is over
```ad-scratch
~~~scratchblock
repeat until <<(y position) > [186]> or <(ROUND OVER) = [1]>>
~~~
```

You might have to adjust the "186" depending on the size of your updraft. Inside this loop:
We move up:
```ad-scratch
~~~scratchblock
change y by (.5)
~~~
```

If they are touching the kitty
```ad-scratch
~~~scratchblock
if <touching [KItty v]?> then
~~~
```

we make them fade out : 
```ad-scratch
~~~scratchblock
broadcast [fade out updraft v]
~~~
```

And then we are done with this round, so we stop the code.
```ad-scratch
~~~scratchblock
stop [this script v]
~~~
```

The {repeat loop} ends
```ad-scratch
~~~scratchblock
end
~~~
```


The {when I receive} loop ends
```ad-scratch
~~~scratchblock
end
~~~
```

Lastly, we hide the updraft. This may not be necessary here...
```ad-scratch
~~~scratchblock
hide
~~~
```



This is the stack that does the fadeout:
```ad-scratch
~~~scratchblock
when I receive [fade out updraft v]
repeat (10)
    change [ghost v] effect by (10)::looks
    wait (0) seconds
end
hide
delete this clone
~~~
```


