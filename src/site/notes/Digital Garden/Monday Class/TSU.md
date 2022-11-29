---
{"dg-publish":true,"permalink":"/digital-garden/monday-class/tsu/"}
---


```ad-scratch
title: 
~~~scratchblock
define set x speed
if <<not <key [left arrow v] pressed?>> and <not <key [right arrow v] pressed?>>> then
    change [x speed v] by (<(x speed) \< [0]> - <(x speed) \> [0]>)
else
remove this and the definition for it. Don't need
    else go in direction of arrow::custom
    change [x speed v] by (<key [right arrow v] pressed?> - <key [left arrow v] pressed?>)
end
if <<<not <key [up arrow v] pressed?>> and <not <key [left arrow v] pressed?>>> and <not <key [right arrow v] pressed?>>> then
    switch costume to [normal v]
end
~~~
```



```ad-scratch
title: 
~~~scratchblock
define change y (y speed) times in steps.Stop at wall.
repeat ([abs v] of (y speed::custom)::operators)
important step. 
the old way we just could fall (-1), 
but now we need to jump, 
so if we are falling we use -1, 
if we are jumping we go up.
    if <(y speed::custom) \< [0]> then
        change y by ((-1) * <not <touching [wall v]?>>)
    else
        change y by ((1) * <not <touching [wall v]?>>)
    end
end

~~~
```



```ad-scratch
title: 
~~~scratchblock
when I receive [touching spikes v]
set [touched spikes v] to [1]
remove the stuff below
if <() = (50)> then
end

~~~
```



```ad-scratch
title: 
~~~scratchblock
when I receive [jump v]
if <key [up arrow v] pressed?> then
Fix like this. This is the easy answer.
It says keep the speed low. 
\(Actually what we really what we want is to only jump 
if we are touching or near the ground. 
That can be done but is a little trickier.) 
    change [y speed v] by ((2) * <(y speed) \< [8]>)
end
broadcast [move left and right v]

~~~
```
