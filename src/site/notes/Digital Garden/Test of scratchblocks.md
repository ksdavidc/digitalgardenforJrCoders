---
{"dg-publish":true,"permalink":"/digital-garden/test-of-scratchblocks/"}
---


## simple callout

> [!hint]- wow
> you betcha

# simple code block


```scratchblock
set [test v] to (0)

```

# collapsible code block

> [!hint]- The <u><B>Set</b> Then <b>Wait</b></u> Trick
> Notice how I **set** a variable, and then **waited** until that variable changed to continue?
> 
> &nbsp;
> 
> That is a cool trick for making sure a step finishes before you continue.
> 
> &nbsp;
> 
> The values can be any two different values, like yes and no:
> 
> ```scratchblock
> set [Am I finished? v] to [No]
> broadcast [keep doing stuff v] and wait
> wait until <(Am I finished?) = [yes]>
> hide
> ```
> 
> &nbsp;
> 
> And the test can be any kind of test. Here we have to catch at least 5 animals:
> ~~~scratchblock
> set [number of cats v] to [0]
> set [number of dogs v] to [0]
> broadcast [catch animals v] and wait
> wait until <((number of cats) + (number of dogs)) > [5]>
> hide
> ~~~



