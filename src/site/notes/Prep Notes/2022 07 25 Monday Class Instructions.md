---
{"dg-publish":true,"permalink":"/prep-notes/2022-07-25-monday-class-instructions/","dgHomeLink":true,"dgPassFrontmatter":false}
---



<style>

text.sb3-label {
    color: darkred;
    fill: white;
    font-family: Times New Roman;
    font-size: medium;
}

.sb3-obsolete {
    fill: transparent;
    stroke: transparent;
}

:is(.markdown-preview-view,.markdown-rendered) pre {
    background-color: black; 
}
</style>


## July 25th

## PREP

### KITTY BLOCK

<div class="blocks">

```
1. FIRST WE ARE GOING TO CREAT A GAME LOOP. 
THEN WE CAN REPLAY THE GAME AT THE END. 

TO DO THAT WE WILL DIVIDE THIS MAIN GAME STACK INTO TWO STACKS. 

FIRST FIND THIS BLOCK:
When green flag clicked
broadcast [initialize v] and wait
and AFTER IT PUT THIS BLOCK:
broadcast [Game Loop v]

THEN WE MAKE A NEW STACK, WHICH WILL BE THE GAME LOOP. 
THIS IS WHERE WE RESTART THE GAME FROM. 
USE THIS BLOCK:
when I receive [Game Loop v]
AND MOVE ALL 5 OF THESE BLOCKS, 
{they are from the green flag above} 
ONTO THE  {when I receive \[Game Loop v\] } 
broadcast [add music v]
broadcast [choose difficulty v] and wait
wait until <(DIFFICULTY) > [0]>
broadcast [Countdown v] and wait
broadcast [Start v] and wait
THEN WE ARE GOING TO ADD TWO BLOCKS ON THE END...
1. THE FIRST WILL MAKE A LANDING EFFECT, AND REPLAY IF YOU TELL IT TO
broadcast [Landed v] and wait
2. THEN, IF YOU DON'T REPLAY,
THIS BLOCK WILL MAKE THE GAME REALLY OVER:
broadcast [Game Over v]


YOU CAN SEE HERE WHAT THIS WILL LOOK LIKE
{YOU HAVE TO SCROLL AT THE RIGHT TO LOOK FOR THE GREEN FLAG AND GAME LOOP STACKS}

[at this link:](https://apple502j.github.io/parse-sb3-blocks/demo?pid=711622549&locale=en&sprite=KItty)

THEN GO TO UPDRAFT SPRITE FOR MORE DIRECTIONS

```

### UPDRAFT block


```
1. AFTER THIS BLOCK
clear graphic effects
FIRST WE DELETE ALL CLONES. ADD THIS: 
{note there is NOTHING in the not block}
if <not <>> then
    delete this clone
end
THEN WE GO TO THE FRONT AND CHOOSE A RANDOM POSITION AND CREATE A CLONE. THE CLONE IS A SHADOW.
go to [front v] layer
go to [random position v]
create clone of [myself v]
KEEP THIS BLOCK:
show
WE ALSO WANT THE UPDRAFT TO MOVE AROUND THE SCREEN, 
SO ADD THIS ONTO THE END:
broadcast [move updraft v] 
WHY BROADCAST? BECAUSE THEN IT WILL ACT ON THE CLONE ALSO.

USE THIS LINK TO SEE THE RESULT 
{AGAIN, LOOK FOR THE RIGHT BLOCKS.}
[this link](https://apple502j.github.io/parse-sb3-blocks/demo?pid=711622549&locale=en&sprite=Updraft)


2. NOW WE WANT THE CLONES TO LOOK LIKE SHADOWS.
ADD THIS
when I start as a clone
PUT THE CLONE BEHIND THE MOTHER UPDRAFT
go [backward v] (1) layers
MAKE IT BLACK
set [brightness v] effect to (-100)::looks
BUT A LITTLE TRANSPARENT
set [ghost v] effect to (75)::looks
OFFSET IT A LITTLE
change x by (2)
change y by (-2)
MAKE SURE IT SHOWS
show


NOW WE CAN MAKE IT MOVE. START A NEW STACK:
when I receive [move updraft v]
KEEP MOVING UP UNTIL IT HITS THE TOP OR THE ROUND IS OVER
INSIDE THE WHEN LOOP:
repeat until <<(y position) > [186]> or <(ROUND OVER) = [1]>>
MOVE IT UP
    change y by (.5)

IF IT IS TOUCHING THE KITTY
    if <touching [KItty v]?> then

LETS MAKE IT FADE OUT 
        broadcast [fade out updraft v]

WE ARE DONE WITH THIS ROUND
        stop [this script v]

{REPEAT LOOP} ENDS
    end

{WHEN I RECEIVE} LOOP ENDS
end
HIDE THE UPDRAFT 
hide


HERE WE DO THE FADEOUT:
when I receive [fade out updraft v]
repeat (10)
    change [ghost v] effect by (10)::looks
    wait (0) seconds
end
hide
delete this clone

what is this?
if <(USEMETHOD) = [2]> then
            Method2::custom
        else
            if <(USEMETHOD) = [3]> then
                // []::custom
                Method3::custom
            else

```

</div>

[[scratchblocks.min.js]]
