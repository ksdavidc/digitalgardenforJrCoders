---
{"dg-publish":true,"permalink":"/prep-notes/2022-08-01-instructions/","dgHomeLink":true,"dgPassFrontmatter":false}
---


## Instructions for Monday, August 1st


<div class="blocks">

### CLOUD SPRITE:

```
at the end of the New sky stack, add this
to make sure the cloud hides when the round is over:
hide

We want a bit of a see-through effect
so the player is looking through the cloud.
Add this stack:
when I receive [initialize v]
set [ghost v] effect to (25)::looks
hide

add this as a new stack
to make sure the cloud is hidden at the beginning of the game:
when I receive [choose difficulty v]
hide

```

### Ground sprite

```
remove this
change[SKY# v] by (-1)
since we will change the SKY# in the kitty sprite instead

and add this as a new stack
This makes sure the game restarts at the last sky, and that the ground is in back
behind the choose difficulty screen:
when I receive [choose difficulty v]
set [SKY# v] to [8]
go to [back v] layer
hide

```

### KITTY

```
add this as a new stack
we are fixing the transition from one sky to the next:
when I receive [ready for new sky? v]
set [ROUND OVER v] to [0]
change [SKY# v] by (-1)
(we removed this from the cloud, remember?)
broadcast [New sky v]

add this as a new stack

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

define ending dance
*** MAKE THIS YOURSELF ***
*** use blocks like:
		change x by
		change y by
		repeat
		change .... effect
		change size 
		go to
		glide
		or any thing else you like
***


and this new stack:
when I receive [Announce Score v]
hide variable [SCORE v]
set [DIFFICULTY SAY v] to (join [𝚈𝚘𝚞 𝚑𝚊𝚟𝚎 𝚊 𝚝𝚘𝚝𝚊𝚕 𝚘𝚏 ] (join (SCORE) [ 𝚙𝚘𝚒𝚗𝚝𝚜 ]))
show variable [DIFFICULTY SAY v]



and this as a new stack:
when I receive [Game Over v]
say [Bye] for (2) seconds
change [ROUND OVER v] by (1)
set y to (-82)
stop [all v]


```

### difficulty

```

create a new  my block
define position difficulty


take these four blocks from  initialize stack:
go to x: (-200) y: (100)
clear graphic effects
set size to (400) %
hide
and put them on the position difficulty stack

add one of these: 
position difficulty::custom
on the initialize stack and 
as the first block on the 
when I receive [choose difficulty v]
stack.





```