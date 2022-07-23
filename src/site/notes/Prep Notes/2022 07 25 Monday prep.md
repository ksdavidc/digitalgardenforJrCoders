---
{"dg-publish":true,"permalink":"/prep-notes/2022-07-25-monday-prep/","dgHomeLink":true,"dgPassFrontmatter":false}
---


## July 25th

### PREP

1. 
FIRST WE ARE GOING TO CREAT A GAME LOOP. THEN WE CAN REPLAY THE GAME AT THE END. TO DO THAT WE WILL DIVIDE THIS MAIN GAME STACK INTO TWO STACKS. FIRST FIND THIS BLOCK, and AFTER IT...
broadcast [initialize v] and wait

PUT THIS BLOCK.
broadcast [Game Loop v]

THEN MAKE A NEW STACK, WHICH WILL BE THE GAME LOOP> THIS IS WHERE WE RESTART THE GAME FROM:

when I receive [Game Loop v]

AND MOVE ALL 5 OF THESE BLOCKS,(from the green flag above) ...

broadcast [add music v]
broadcast [choose difficulty v] and wait
wait until <(DIFFICULTY) > [0]>
broadcast [Countdown v] and wait
broadcast [Start v] and wait

ONTO THE GAME LOOP (broadcast [Game Loop v])

THEN ADD THESE TWO BLOCKS ON THE END:

THIS WILL MAKE A LANDING EFFECT, AND REPLAY IF YOU TELL IT TO
broadcast [Landed v] and wait

IF YOU DON'T REPLAY, THEN THE GAME IS REALLY OVER:
broadcast [Game Over v]


YOU CAN SEE here to see what it will look like:
https://apple502j.github.io/parse-sb3-blocks/demo.html


THEN GO TO UPDRAFT SPRITE FOR MORE DIRECTIONS