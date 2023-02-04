---
{"dg-publish":true,"permalink":"/digital-garden/monday-class/2022-monday-student-h/"}
---


## 2022 09 09
 
The main goal today is to make the platforms cycle. We need to fix a few things as well (platforms sticking at edge and x in the last platform).

Let's start with Sprite 1. In this stack:
```ad-scratch
~~~scratchblock
when [right arrow v] key pressed
~~~
```
you have:
```ad-scratch
~~~scratchblock
set x to ((x) - (scroll x))
~~~
```
(x) - (scroll x) tells us how far this platform's position (called `x`) is from the current position in the game  (called `scroll x`). This is the same thing as where the sprite is relative to the center of the screen, and that's really our standard, blue x position (relative to our screen).

In order to: 
*  avoid long lines of code
* make our code a little easier to read
* help debug the code
* be able to show it on the screen
* help teach you how the code works,
we are going to put this in a new variable called `x offset from game position` (still too long, but to help you remember what it is, I suggest using this name). This isn't changing the game (yet), just giving it a name. So go ahead and create the variable after reading this:
> [!important] Important, READ THIS
This has to be a "for this sprite only" variable, since each platform sprite will have **its own position**. That is why I wrote it in small (lowercase) letters, not BIG (CAPITAL, UPPER CASE) LETTERS. There is a convention that many scratchers use which says: small letter variables are local ("*for this sprite only*") variables. I follow that rule, which means, when you create a variable, be sure to check for that. 

Now we can put this first thing in the right arrow stack. 
```ad-scratch
~~~scratchblock
when [right arrow v] key pressed
set [x offset from game position v] to ((x) - (scroll x))
...
~~~
```

However, it is a good rule to **initialize every variable** in the beginning of the game. If you don't, strange things happen. For example, when we start the game and before we press right arrow, the value will be wrong. We don't want that.

In the "green flag stack", this is the code you already have:
```ad-scratch
~~~scratchblock
when flag clicked
point in direction (90)
go to x\: (0) y\: (0)
go to [back v] layer
set [x v] to [0]
~~~
```

Initialize our variable by putting this right after that:
```ad-scratch
~~~scratchblock
set [x offset from game position v] to ((x) - (scroll x))
~~~
```

>[!Note] And another thing...
> 1. `scroll x` is global. To make that clear, and to follow the convention, I suggest renaming it to `SCROLL X`
> >```scratchblock
>> set [x offset from game position v] to ((x) - (SCROLL X))
> >```
> 3. Notice that `SCROLL X` is initialized in your sonic sprite and (I know that) it runs **before this block** runs.  Therefore, at this point, `x offset from game position` should have a value of zero. If this wasn't true you could get strange values here. That is why we **initialize** variables.

We use the number `480` a lot because it is the size of the screen, so let's make another variable `SCREEN SIZE` for it. (Note, this so-called "variable" will stay the same throughout the game, so technically I should call it a 'named constant'.)
```ad-scratch
~~~scratchblock
set [SCREEN SIZE v] to [480]
~~~
```

Lastly we make another 'named constant', `FRAME SIZE`, to tell us how big the game frame is, and since there are six platforms:
```ad-scratch
~~~scratchblock
set [FRAME SIZE v] to ((6) * (SCREEN SIZE))
~~~
```

Now we are getting to the heart of it: making the platforms scroll. 

### Clock Math
Have you ever noticed that usually `11 + 2 = 13`, but on a clock, `11 + 2` is `1`? That's **clock math**. If you understand a clock, you can understand what is happening. 

The 2 points you need to get are:
* Take `12` away until you get a number less than `12`.
- There is no 12 o'clock, we use `0` instead

* Take `12` away until you get a number less than `12`.
 Clock math is also called `Mod` or “modular math" or "modulo math". `Mod` is just the name for the same kind of thing we do when we add time on a 12-hour clock. On a **non-digital, 12-hour** clock if it is 11 o'clock and I wait 2 hours, it doesn't show 13 o'clock, it shows 1 o'clock. In clock math can say we are "taking the time *mod 12*". In terms of the numbers, it means if a number is larger than or equal to `12`, we keep taking away `12` until we get a number *less than* `12`. For example, `13 mod 12` is `13 - 12 = 1`. For this reason, `25 mod 12` is also `1`, and `36 mod 12 = 1`, too. Take `12` away until you get a small number.

- There is no 12 o'clock
Actually, there is one small, but important, difference between modular math and the usual clock math. In modular math, **there is no *12 o'clock***. That's right, there is no noon. Math says *0 o'clock* instead. In clock math, *11 + 1 = 12 noon*. In modular math, *11 + 1 mod 12 = 0*. *0* and *12* are the same in modular math, and we don't use *12*. 



### Mod in the game

Let's say, in our game, we have 3 platforms, so our clock only goes up to 3 o'clock. No problem, instead of *mod 12* we do *mod 3*.

Platform 1 is at position *0*, platform 2 is at position *1*, and platform 3 is at position *2*. Let's write this "frame", as a list, like this: 
  
 *0, 1, 2*
  
These are the **positions**, not the platform numbers. 
 
Also, in this example, they represent a section that 1 screen wide, starting at that position. So the first platform starts at *0*, and goes to just under *1*, which is written \[*0, 1*). Notice the square `[` and round `)` brackets. The round bracket means not the number 1.
  
The important thing to understand is that in Scratch, **our screen always shows only the parts of the frame that are in \[*0, 1*)**.  If the number is bigger than *1* it is offscreen. In this case, only platform 1 is visible, since it is the only one living in the range \[*0, 1*).
  
If at this point we take the positions in the list *mod 3*, the numbers don't change.

 *0, 1, 2* becomes  *0, 1, 2* 

But, let's say we move the platforms *right* half a screen (because, for example, our character has moved *left*). Mathematically, moving right means adding *½* to each position. So platform 1 is now at *½*, platform 2 is at *1½*, etc.:
 *½, 1½, 2½

**Notice that there is no platform covering the part of the screen between 0 and ½,  \[*0, ½*)**. Yikes, the screen will be blank there! Platform 1 got moved to place *½*, and left a blank in  \[*0, ½*). 

We have to fill that spot, and we are going to bring platform 3 to fill it. Here's how. 


### **ADD, MOD, SUBTRACT**

1. First we **ADD 1** to every number:

*½, 1½, 2½*  becomes *1½, 2½, 3½ 

2. Then we **MOD** *3*:

*1½, 2½, 3½* becomes *1½, 2½, ½*

Notice how the last number becomes *½* because it was bigger than our mod base, 3. This means it is now showing on the screen, but too far right, covering \[*½, 1*). We have to move it to the left side.

3. So, we **SUBTRACT** the *1* we added:

*1½, 2½, ½* becomes *½, 1½, -½

The *-½* at the end, which you remember covers the range \[*-½, ½*) is now covering the gap between \[*0, ½*). HOORAY!

Here it is in code. Notice how we **ADD** the `SCREEN SIZE`, then **MOD** the `FRAME SIZE`, then **SUBTRACT** the `SCREEN SIZE` again :

```ad-scratch
~~~scratchblock
when [right arrow v] key pressed::event
set [x offset from game position v] to ((x) - (scroll x))
set [SCREEN 1 POSITION v] to ((((x offset from game position) + (SCREEN SIZE)) mod (FRAME SIZE)) - (SCREEN SIZE))
set x to (SCREEN 1 POSITION)
~~~
```

> [!note]
> I won't explain it, but turns out this works no matter how many platforms there are, and also no matter where we are in the frame, and also whichever direction we go. To understand this you need to know one more fact:
> - negative numbers get "pushed over to the other side"
> 
> What happens with negative numbers, like *-1*? What is *-1 mod 12*? Well, one hour before *12* is *11*. But *12* is the same as *0*, and *0 - 1 = -1*. In other words, one hour before *0* is *11*, so *-1 mod 12 = 11*. It gets "pushed to the other side".
> When we are at the other end of the frame, and going in the other direction, for example, the first platform gets pushed over to cover the gap at *that* end.
> 

Two more fixes we should do now, before they become problems.

### Platform costume sticking
You might notice that sometimes the sprites stick at the side of the screen. You can see this in your project if you  hit right arrow a few times. 

This can happen for two reasons, and we will fix both. First, scratch can't really pull a costume beyond the edge. We have to trick it, by making the costume just a little bit bigger than the screen.

Here goes:
1. Duplicate the costume.
2. Convert it to vector
3. With the pen tool draw a small dot below and to the left of the costume you have.
4. Do the same with another dot below and to the right.
5. Name this costume "with dots"

Now, right after the
```ad-scratch
~~~scratchblock
when flag clicked
~~~
```
Put this
```ad-scratch
~~~scratchblock
switch costume to [with dots v]
~~~
```
This makes sure we are using this costume during the game, and we put it first so we see it right away.

The second related thing is that, because costumes are overlapping each other in the wrong way, they sometimes show up in front of others. For example, in your project, if you click right arrow once or twice at the start, you can see the overlap. Specifically, platform 3 is covering platform 2, and platform 3 is still stuck at the edge. The layers are not in the right order.

In the beginning of the game, all the platforrms are sent to the back one by one. We want to be sure the first one is always in front of the others when the game starts. 

It turns out that Sprite 1 is the first one that is run (I think the reason is that it was the first one you created, but I am not sure). That means, if at the start we put it 6 layers ahead, the others will then be behind it when they are sent back. Add this at the end of the green flag stack.
```ad-scratch
~~~scratchblock
go [forward v] (6) layers
~~~
```

### Fix Platform 6
I also noticed that there is a mistake in the x value of Platform 6 in your code. See if you can find it, and while you are at it, get rid of the extra blocks.

## 2022 09 02 NEXT STEP CHALLENGE:

0. I suggest renaming the variables `hello` and `hi` to more useful values, like `background1 x`, `background2 x`. 

**Better yet**, now that you have made them unique, you can:  
* convert them to **local/this sprite only variables** (since they are only used in one sprite), 
* delete the **global/all sprites** `my x`, and 
* call the  `hi/hello` **local/this sprite only** variables both just `my x`, as I should have made you do in the first place.

To do this:
a. make sure the Scratch Addons has '*Switch variables between "For all sprites" and "For this sprite only"*' selected (orange). 
![screenshot](https://i.imgur.com/2VqS36W.png)
(It think I did that in class, but just make sure). 
b. Go to **each** background sprite **individually** and **in the block pallette** (*not the code area*),  right click on the hi/hello variable  to make it local. 
c. Right-clicking the **global**  variable `my x` , you can then delete that. 
d. Then, right click the local `hi/hello` variables again to rename them.

1. The background 2 `my x` value doesn't have to be 480. Change it to bigger and smaller numbers and see what happens.
````ad-tip
title: TIP
To help you see this more clearly, we put a
```ad-scratch
~~~scratchblock
set (color v) effect to (50)
~~~
```
in the green flag stack of bkg 2 (not 1). This should make the second background appear green, instead of red. In the actual game you can take it out.



a. But, here is a question: When the game starts, before you touch the right arrow, why does your background appear green instead of red? 

<details><summary><u>Hint</u></summary>
Try <b>hiding the second background</b> and see what happens.
<details>
<summary> <u>Another Hint</u>
</summary>
When the game starts, what <b>x-position</b> are the two backgrounds at?
<details>
<summary> 
<u>Another Hint</u>
</summary>
* You should see they are both at zero. But <b>we wanted the second one to be at 480</b>! To fix this, you will need to copy one block (already in your project) and make sure it runs when the game starts. Which block?
</details>
</details>
</details>
````
2. If you explore you may find that a (my x) value of **600** is special. Can you figure out what it is?

<details><summary><u>Hint</u></summary>
Be sure the size of the background is 200. <b>Change the size of background</b> and see how it changes. Again, try different values of (my x)
<details>
<summary> 
<u>Another Hint</u>
</summary>
<b>Showing</b> the variable `scroll x` will also help.
</details>
</details>

3. Make Sonic be able to move left as well. This is mostly copy and paste, but there are a few changes you need to make.

---


## Old Stuff

### 2022 08 22


1. rename sprites (standing sonic, running sonic, bkg 1, bkg 2)

### Standing Sonic sprite
#### * green flag stack

initialize scroll x 
```ad-scratch
~~~scratchblock
set (scroll x v) to (0)
~~~
``` 

add this so he is animated at beginning
```ad-scratch
~~~scratchblock
go to [front v] layer
repeat until <<key [left arrow v] pressed?> or <key [right arrow v] pressed?>>
    next costume
end
~~~
``` 

#### * right arrow pressed stack

```ad-scratch
~~~scratchblock
when [right arrow v] key pressed
point in direction (90)
~~~
``` 
#### * message 1 stack
Move this part of your right arrow stack into this stack:
```ad-scratch
~~~scratchblock
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
~~~scratchblock
set (my x v) to (0)
~~~
``` 

### bkg 2 stack
#### * green flag stack
add  in bkg 2

```ad-scratch
~~~scratchblock
set (my x v) to (480)
~~~
``` 
this is 480 because the second background is 480 off

#### * right arrow key pressed stack

replace move 10, and replace it with:

```ad-scratch
~~~scratchblock
set (my x v) to ((x)-(scroll x))
~~~
```


### running sonic sprite

#### right arrow stack:

* remove first next costume, not needed. replace it with the show block from the other right arrow stack. 
* add 
```ad-scratch
~~~scratchblock
change (scroll x v) by (10) 
~~~
``` 

this will replace the move 10 you have in the bkgs.

