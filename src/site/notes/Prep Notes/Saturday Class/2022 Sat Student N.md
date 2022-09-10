---
{"dg-publish":true,"permalink":"/prep-notes/saturday-class/2022-sat-student-n/","dgHomeLink":true,"dgPassFrontmatter":false}
---


# Student N

## 2022 09 17

Add
When game is over, let's delete the old pipes

```ad-scratch
~~~scratchblock
When I receive [Game Over v]
delete this clone
~~~
```


## Old Stuff
## 2022 08 20




```ad-scratch
~~~scratchblock

when I receive [GameOver v]
stop all sounds
stop [other scripts in sprite v]

~~~
```


### in the when I start as a clone stack
change play sound to:

```ad-scratch
~~~scratchblock
        start sound [Dance Around]
~~~
```

Add this:

```ad-scratch
~~~scratchblock

when I receive [AboutToDie v]
repeat (3)
    show
    wait (0.05) seconds
    hide
    wait (0.05) seconds
end
Broadcast [Game over v]
delete this clone
~~~
```


### In Abu
add to when I receive start stack
```ad-scratch
~~~scratchblock
switch backdrop to [Blue Sky v]
~~~
```




