---
{"dg-publish":true,"permalink":"/prep-notes/monday-class/monday-student-h/","dgHomeLink":true,"dgPassFrontmatter":false}
---

## NEXT STEP CHALLENGE:

0. I suggest renaming the variables `hello` and `hi` to more useful values, like `background1 x`, `background2 x`. 

Better yet, now that you have made them unique, you can:  
* convert them to **local/this sprite only variables** (since they are only used in one sprite), 
* delete the **global/all sprites** `my x`, and 
* call the  `hi/hello` **this sprite only** variables both just `my x`, as I should have made you do in the first place.

To do this:
1. make sure the Scratch Addons has '*Switch variables between "For all sprites" and "For this sprite only"*' selected (orange). ![screenshot](https://i.imgur.com/2VqS36W.png)(It think I did that in class, but just make sure). 
2. Then you can right click on the hi/hello variable <u>while in its sprite</u> to make it local. 
3. Right-clicking the **global**  variable `my x` , you can then delete that. 
4. Then, right click the local `hi/hello` variables again to rename them.

1. The bkg 2 `my x` value doesn't have to be 480. Change it to bigger and smaller numbers and see what happens.
````ad-tip
title: TIP
To help you see this more clearly, we put a
```ad-scratch
~~~
set (color v) effect to (50)
~~~
```
in the green flag stack of bkg 2 (not 1). This should make the second background appear green, instead of red. In the actual game you can take it out.

````

2. But, here is a question: When the game starts, before you touch the right arrow, why does your background appear green instead of red? 

<details><summary><u>Hint</u></summary>
Try hiding the second background and see what happens.
<details>
<summary> <u>Another Hint</u>
</summary>
When the game starts, what x-position are the two backgrounds at?
<details>
<summary> 
<u>Another Hint</u>
</summary>
You should see they are both at zero. But we wanted the second one to be at 480! To fix this, you will need to copy one block (already in your project) and make sure it runs when the game starts. Which block?
</details>
</details>
</details>

3. If you explore you may find that a (my x) value of **600** is special. Can you figure out what it is?

<details><summary><u>Hint</u></summary>
Be sure the size of the background is 200. Change the size of background and see how it changes. Again, try different values of (my x)
<details>
<summary> 
<u>Another Hint</u>
</summary>
Showing the variable (scroll x) will also help.
</details>
</details>

4. Make Sonic be able to move left as well. This is mostly copy and paste, but there are a few changes you need to make.
---
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

