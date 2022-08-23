---
{"dg-publish":true,"permalink":"/prep-notes/monday-class/monday-student-h/","dgHomeLink":true,"dgPassFrontmatter":false}
---


1. rename sprites (standing sonic, running sonic, bkg 1, bkg 2)

### Standing Sonic sprite
initialize scroll x in green flag stack
```ad-scratch
~~~
set (scroll x v) to (0)
~~~
``` 



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

the bkg 2 my x value doesn't have to be 480. Change it to bigger and smaller numbers and see what happens.
Why is 600 special???

> [!hint]
> 
> To help you see this, put a
> 
> ````ad-scratch
> ```
> set (color v) effect to (50)
> ```
> ````
> in the green flag stack
> 


2. Make Sonic be able to move left as well.

Be sure that:
* sonic is not upside down
* if you press an arrow key once quickly, sonic doesn't stop
* remove the white background



