---
{"dg-publish":true,"permalink":"/prep-notes/halloween/simple-halloween-storytelling-project/","dgHomeLink":true,"dgPassFrontmatter":false}
---


## Simple Halloween Storytelling Project

### Overview
* **Project**: Halloween story 
* **Transition**: one costume disappears and another appears
* **Purpose**: To teach the **TRANSITION TRICK**
* **Useful**: Introduction screens, scene changes, etc.
* **Practice** basic idea: [[Prep Notes/Halloween/Broadcast Game|Broadcast Game]]

## Halloween Game

### Checklist
Choose: 
- [x] **theme**: Halloween 
* [ ] **setting**: *An evening walk*
* [ ] **characters**: *me, a ghost*
* [ ] **premise** (basic situation): *I meet a ghost and something happens* 
* [ ] **challenge** for the main character: *the ghost scares me*
* [ ] **twist** or surprise: *I am not scared*
* [ ] **resolution**: *I eat him*

### Warmup Game

We play a game where we go around the room and each person adds one item to the story. This is a warmup only though. 

### Make your Summary/Storyboard
* Option 1: Work in pairs
* Option 2: Work on your own story.

You can come up with the ideas in Japanese, but you have to write them down in English. I will help if needed. 

Using the storytelling checklist to start. then add details

* Be neat. It will be used in project poster. Yes, there will be project posters!!

### Storyboard (on paper)

1. Tell the story **in images only**, as a sequence of image **frames** one after the other, like a comic strip or flipbook.  
2. Write **description of action** for each image. 
3. If you are working in pairs make a copy for each of you, even if you are doing the same project

## Draw each image in Scratch
- Create a "Frames" sprie for the images.
- Code will cycle through the images, one at a time.
- Can be rough, just a guide.
- Characters can change position from frame to frame.
- Frame can move or change setting or position.
- Speech bubbles and text OK
- No actual motion or sound, yet.

### Coding the transitions
* Always initialize sprites.

```ad-scratch
~~~scratchblock
when @greenFlag clicked
go to x\: (0) y\: (0)
switch costume to [costume1 v]
show
~~~
```


> WE COULD: transition with the  right arrow key and next costume:
> 
> ```ad-scratch
> ~~~scratchblock
> {example, don't do:}
> when [right arrow v] key pressed::event
> next costume
> ~~~
> ```
> 
> But, we are going to be smarter than that.
> 
> * Want to go forwards and backwards.
> * Instead of `next costume`, use `costume [number v]`
> * `+1` forward,  `-1` backward.
> ```ad-scratch
> ~~~scratchblock
> Example, next frame:
> ((costume [number v]) + (1))
> 
> Example, previous frame:
> ((costume [number v]) + (-1))
> ~~~
 
* Define a **myblock** called **transition** 
* one input, called  `1 or -1`. 
```ad-scratch
~~~scratchblock
define transition (1 or -1)
switch costume to ((costume [number v]) + (1 or -1::custom))
~~~
```

* Right arrow forward, Left arrow backward:
```ad-scratch
~~~scratchblock
when [right arrow v] key pressed::event
transition [1]::custom 

when [left arrow v] key pressed::event
transition [-1]::custom
~~~
```

````ad-note 
title: Variations

* Space key
```ad-scratch
~~~scratchblock
when [space v] key pressed::event
transition [1]::custom
~~~
```
* Clicking the sprite:
```ad-scratch
~~~scratchblock
when this sprite clicked
transition [1]::custom
~~~
```
````

* We will use: **receive message**
```ad-scratch
~~~scratchblock
when I receive [next v]
transition [1]::custom


when I receive [previous v]
transition [-1]::custom
~~~
```

### BUTTON transition
* New sprite called BUTTON
* Add arrow (triangle): 
> [!info] How to make a triangle in Scratch:
>1. Make a square. Two sides of the square will be the front part of the arrow.
> 2. Spline tool shows dots:
> ![spline.png|200x200](data:image/png;base64,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)
> 
> 3. Double click corner dot to delete it. (takes practice.)
> 4. Triangle with long side, but pointing wrong way.
> 5. So, hold shift and use the rotation handle to turn:
| ![](https://i.imgur.com/Kf3OXV8.png) |
|:--:|
|rotation handle|


| ![](https://i.imgur.com/Kf3OXV8.png) |
|:--:|
|rotation handle|


## THE TRANSITION TRICK

**MAIN IDEA FOR THIS PROJECT!**

In FRAMES we **already have**:
```ad-scratch
~~~scratchblock
when I receive [next v]
transition [1]::custom

define transition (1 or -1)
switch costume to ((costume [number v]) + (1 or -1::custom))

~~~
```

In BUTTON, **add**:
```ad-scratch
~~~scratchblock
when this sprite clicked
broadcast [next v]
~~~
```

Together, I call this the **TRANSITION TRICK**. Learn it.

### Challenge
Make another button to move backwards.

### Ghost Effect Trick
>[!info] Fact
> * *If the ghost effect is 100, we can't see the sprite, but* 
> * *Scratch can still detect that our mouse is touching it (It can't do that if the sprite is hidden)*.

* Makes your buttons cool and user-friendly!
* Shows the button when our mouse is over it
* Hides it when it isn't. 
* Screen is less cluttered. 
* Player sees the whole screen while the project is running
* Buttons show only when needed.

```ad-scratch
~~~scratchblock

when @greenFlag clicked
forever
    if <touching [mouse-pointer v]?> then
    set [ghost v] effect to (0)::looks
    else
        set [ghost v] effect to (100)::looks
    end
end
~~~
```

To make it slowly appear, change it like this:

```ad-scratch
~~~scratchblock

when @greenFlag clicked
forever
    if <touching [mouse-pointer v]?> then
        repeat (5)
            change [ghost v] effect by (-20)::looks
        end
        set [ghost v] effect to (0)::looks
    else
        set [ghost v] effect to (100)::looks
    end
end
~~~
```

