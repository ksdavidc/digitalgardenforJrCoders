---
{"dg-publish":true,"permalink":"/prep-notes/monday-class/monday-student-h/","dgHomeLink":true,"dgPassFrontmatter":false}
---


1. rename sprites (standing sonic, running sonic, bkg 1, bkg 2)

### Standing Sonic
initialize scroll x in green flag stack
```ad-scratch
~~~
set (scroll x v) to (0)
~~~
``` 



### bkgs 1 & 2

#### green flag stack
add  bkg 1

```ad-scratch
~~~
set (my x v) to (0)
~~~
``` 
add  bkg 2

```ad-scratch
~~~
set (my x v) to (480)
~~~
``` 


#### right arrow key pressed:

replace move 10, and replace it with:

```ad-scratch
~~~
set (my x v) to ((x)-(scroll x))
~~~
```




### running sonic 

#### right arrow stack:

* remove first next costume, not needed. replace it with the show block from the other right arrow stack. 
* add 
```ad-scratch
~~~
change (scroll x v) by (10) 
~~~
``` 

this will replace the move 10 you have in the bkgs.



