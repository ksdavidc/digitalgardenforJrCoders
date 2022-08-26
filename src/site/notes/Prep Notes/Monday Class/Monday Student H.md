---
{"dg-publish":true,"permalink":"/prep-notes/monday-class/monday-student-h/","dgHomeLink":true,"dgPassFrontmatter":false}
---

## NEXT STEP CHALLENGE:

1. I lied. The bkg 2 my x value doesn't have to be 480. Change it to bigger and smaller numbers and see what happens.
````ad-tip
title: TIP
To help you see this more clearly, we put a
```ad-scratch
~~~
set (color v) effect to (50)
~~~
```
in the green flag stack of bkg 2 (not 1). This should make the second background appear green, in stead of red. In the actual game you can take it out.

````

2. But, here is a question: Why does your background appear green when the game starts?

<details><summary>Hint</summary>
Try hiding the second background and see what happens.
<details>
<summary> 
Another Hint
</summary>
You will need to copy one block in your project and run it when the game starts.
</details>
</details>

3. If you explore you may find that a (my x) value of **600** is special. Can you figure out what it is?

<details><summary>Hint</summary>
Be sure the size of the background is 200. Change the size of background and see how it changes. Again, try different values of (my x)
<details>
<summary> 
Another Hint
</summary>
Showing the variable (scroll x) will also help.
</details>
</details>

4. Make Sonic be able to move left as well. This is mostly copy and paste, but there are a few changes you need to make.





### 2022 08 22


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

