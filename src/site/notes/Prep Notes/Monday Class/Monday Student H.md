---
{"dg-publish":true,"permalink":"/prep-notes/monday-class/monday-student-h/","dgHomeLink":true,"dgPassFrontmatter":false}
---


1. rename sprites (standing sonic, running sonic, bkg 1, bkg 2)

### Standing Sonic sprite
#### * green flag stack

initialize scroll x 
```ad-scratch
~~~
set (scroll x v) to (0)
~~~
``` 

add this so he is animated at beginning
```ad-scratch
~~~
go to [front v] layer
repeat until <<key [left arrow v] pressed?> or <key [right arrow v] pressed?>>
    next costume
end
~~~
``` 

#### * right arrow pressed stack

```ad-scratch
~~~
when [right arrow v] key pressed
point in direction (90)
~~~
``` 
#### * message 1 stack
Move this part of your right arrow stack into this stack:
```ad-scratch
~~~
when I receive [message1 v]
go to [running sonic v]
show
repeat until <key [right arrow v] pressed?>
    next costume
end
hide
~~~
``` 
(*in your version, the hide is not at the bottom and the wait until is not needed*)




### bkg 1 sprite
#### * green flag stack
add  in bkg 1

```ad-scratch
~~~
set (my x v) to (0)
~~~
``` 

### bkg 2 stack
#### * green flag stack
add  in bkg 2

```ad-scratch
~~~
set (my x v) to (480)
~~~
``` 
this is 480 because the second background is 480 off

#### * right arrow key pressed stack

replace move 10, and replace it with:

```ad-scratch
~~~
set (my x v) to ((x)-(scroll x))
~~~
```


### running sonic sprite

#### right arrow stack:

* remove first next costume, not needed. replace it with the show block from the other right arrow stack. 
* add 
```ad-scratch
~~~
change (scroll x v) by (10) 
~~~
``` 

this will replace the move 10 you have in the bkgs.

## NEXT STEP CHALLENGE:

1. I lied. 

* The bkg 2 my x value doesn't have to be 480. Change it to bigger and smaller numbers and see what happens.
````ad-tip
title: TIP
To help you see this more clearly, put a 
```ad-scratch
~~~
set (color v) effect to (50)
~~~
```
in the green flag stack of bkg 2 (not 1)

````

* Why is a my x value of **600** special???

2. Make Sonic be able to move left as well.

Be sure that:
* sonic is not upside down
* if you press an arrow key once quickly, sonic doesn't stop
* remove the white background



