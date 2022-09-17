---
{"dg-publish":true,"permalink":"/prep-notes/saturday-class/2022-sat-student-n/","dgHomeLink":true,"dgPassFrontmatter":false}
---


# `= this.file.name`

## 2022 09 17

### Small Fixes
When game is over, let's delete the old pipes by adding this in the pipe sprite:
```ad-scratch
~~~scratchblock
When I receive [Game Over v]
delete this clone
~~~
```

In F, add this before you `broadcast start` to restart the game (*can you figure out where this is?*):
```ad-scratch
~~~scratchblock
wait until <<mouse down?> or <key [any v] pressed?>>
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




