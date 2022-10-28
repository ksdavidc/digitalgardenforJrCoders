---
{"dg-publish":true,"permalink":"/prep-notes/halloween/broadcast-game/"}
---


### Broadcast Game
Remix the template project. It has 5 broadcast and receive pairs. It includes one broadcast and wait. It also has 2 myblocks.

```ad-scratch
~~~scratchblock
broadcast [msg1 v]
when I receive [msg1 v]

broadcast [msg2 v] and wait
when I receive [msg2 v]

...

define mb1

define mb2
~~~
```


Now, you can then add other blocks and sprites
* not less 10  blocks
* not more than 20 blocks
* No more than 5 sprites 
* Only 2 myblocks
* At least one when this sprite is clicked block with a broadcast in it.

```ad-scratch
~~~scratchblock
when this sprite clicked
...
broadcast [msg1 v]
...
~~~
```

* every receive block must have at least one other block under it.
* Every broadcast block must get used at least once either via the green flag or clicking on a sprite. 

