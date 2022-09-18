---
{"dg-publish":true,"permalink":"/prep-notes/halloween/simple-halloween-storytelling-project/","dgHomeLink":true,"dgPassFrontmatter":false}
---


## Simple Halloween Storytelling Project

### Overview
We are going to tell a Halloween story using a simple **transition system** for moving from one screen to the next. The purpose is to practice *making one costume disappear and another appear*. This is used for things like **Introduction screens**, and most good projects have one. It is a basic building block of many projects, especially ones that tell stories. We are going to make a pretty simple one, and then later perhaps we will add some effects. 

For the Halloween story itself, the focus will be on how we tell the story, not the story itself, but the two are related.

### Getting an Idea
First, you need an idea. Often, that means choosing: 
* a theme: Halloween 
* a setting: An evening walk
* some characters: me, a ghost
* a premise (basic situation): I meet a ghost and something happens. 
* a challenge for the main character: the ghost scares me
* a twist or surprise: I am not scared
* a resolution: I eat him

### Game
Telling someone else what you are doing is a good way to get new ideas, see what you need to code it, see what works and doesn't, and other things.

To make this easier, we will play a game where we will, as a group, come up with a story. We will go around the room and each person adds one item to the story. This is a warmup only though. 

For the real project, you will work in pairs, and do the same thing. Using the storytelling checklist as a guide write the story. You can make one story between the two of you. Or two stories, one for each of you. This is an act of cooperation and communication. 

Write down what you have. You can come up with the ideas in Japanese, but you have to write them down in English. I will help. 

What you write down will be the basis for the summary in your project poster. Yes, there will be project posters!!

### Map Out Your Project
Now that you have a story, the next step is to tell the story **in images only**. This means a sequence of image **frames** one after the other, like a comic strip.  You can often do that in your head, but **in this class**, in order to:
* make it easier for me to help you
* prevent possible problems later
* be sure your idea will work in this situation
I need you to **map our your project on paper**. A rough drawing of each **frame** in order is enough. Each person should do their own, even if they are doing the same project.

For this project, at this stage, there is no motion. The challenge here is to tell the story just with **still** images going by one at a time, like a flipbook. Characters can change position from frame to frame. The frame can move closer of change position. You can do speech bubbles and text, but no actual motion or sound, yet.

### Coding the transitions
Once you have that, we can begin coding. First we will create a sprite (*I called mine "Frames"*) to hold the frames. This is the series of images we are going to cycle through, one at a time.

Then, draw each frame (as a costume in your sprite). If you want, you can do just a few to start, and add more once the code is working. This can help you preview your work as you go along.

Once you have a few costumes, let's make our **transition system**. First, **as always**, initialize the sprite.

```ad-scratch
~~~scratchblock
when @greenFlag clicked
go to x\: (0) y\: (0)
switch costume to [costume1 v]
show
~~~
```

We could move through the screen using the right arrow key and next costume. 

```ad-scratch
~~~scratchblock
{example, don't do:}
when [right arrow v] key pressed::event
next costume
~~~
```

But, we are going to be smarter than that. We want to be able to go forwards and backwards. Instead of `next costume`, let's use `costume + 1`, where the `1` tells us we are going forward.
  ```ad-scratch
 ~~~scratchblock
Example, next frame:
((costume [number v]) + (1))
 ~~~
 ```
 To go back, we would use `-1` instead.
 ```ad-scratch
~~~scratchblock
Example, previous frame:
((costume [number v]) + (-1))
~~~
```

So, now that we have a plan for that, we can create a **myblock** to do it. I am calling it **transition** and it has one input. The input is called `1 or -1`. If it is `1`, we will go to the next costume. If it is `-1` we go to the previous costume:
```ad-scratch
~~~scratchblock
define transition (1 or -1)
switch costume to ((costume [number v]) + (1 or -1::custom))
~~~
```

Now we tell right arrow to transition forward:

```ad-scratch
~~~scratchblock
when [right arrow v] key pressed::event
transition [1]::custom 
~~~
```

And, we use the left arrow to transition backward:

```ad-scratch
~~~scratchblock
when [left arrow v] key pressed::event
transition [-1]::custom
~~~
```

We can make the space key go forward as well:

```ad-scratch
~~~scratchblock
when [space v] key pressed::event
transition [1]::custom 
~~~
```

Or even clicking the sprite itself:

```ad-scratch
~~~scratchblock
when this sprite clicked
transition [1]::custom
~~~
```

Or even use a **message** to make it change:
```ad-scratch
~~~scratchblock
when I receive [next v]
transition [1]::custom


when I receive [previous v]
transition [-1]::custom
~~~
```

We can use these in different ways. For example, using a message, we can make a button transition. First make a button. In my case I used a big rectangle at the edge, with a small triangle. I made the triangle/arrow like this:
1. Make a square. Two sides of the square will be the front part of the arrow.
2. Use the <?xml version="1.0" encoding="UTF-8" standalone="no"?>
<svg width="20px" height="20px" viewBox="0 0 20 20" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
    <!-- Generator: Sketch 43.2 (39069) - http://www.bohemiancoding.com/sketch -->
    <title>reshape</title>
    <desc>Created with Sketch.</desc>
    <defs></defs>
    <g id="Page-1" stroke="none" stroke-width="1" fill="none" fill-rule="evenodd">
        <g id="reshape">
            <g id="reshape-icon" transform="translate(3.000000, 2.000000)">
                <path d="M6.3718,4e-05 C6.3718,1.20298846 6.03840639,2.32811001 5.45898306,3.28804076 C5.31876362,3.52034235 4.30079812,3.15107034 3.82818604,3.61859131 C3.35557395,4.08611228 3.47873759,5.34529147 3.26181884,5.47482181 C2.30759304,6.04462589 1.19191205,6.37204 -0.0002,6.37204" id="Stroke-1" stroke="#575E75" stroke-width="0.75"></path>
                <path d="M4,6.94999094 C2.85887984,6.71835578 2,5.70947896 2,4.5 C2,3.11928813 3.11928813,2 4.5,2 C5.88071187,2 7,3.11928813 7,4.5 C7,4.56854233 6.99724162,4.63644042 6.99182982,4.70358929 L6.68137747,4.42017327 C5.65792772,3.48493325 4,4.20484091 4,5.595932 L4,6.94999094 Z" id="Combined-Shape" fill="#575E75"></path>
                <path d="M4,7.96455557 C2.30385293,7.72194074 1,6.26323595 1,4.5 C1,2.56700338 2.56700338,1 4.5,1 C6.43299662,1 8,2.56700338 8,4.5 C8,4.84508345 7.95005914,5.1785026 7.85701065,5.4934242 L6.68137747,4.42017327 C5.65792772,3.48493325 4,4.20484091 4,5.595932 L4,7.96455557 Z" id="Oval-2" fill-opacity="0.15" fill="#575E75"></path>
                <path d="M7.87915329,13.1684522 L8.98467414,15.6316703 C9.20235954,16.1186581 9.76980913,16.3337238 10.2516521,16.1137141 C10.7334951,15.8924683 10.9462887,15.3189598 10.7286032,14.833208 L9.63583183,12.3973461 L12.3974628,12.3973461 C12.945512,12.3973461 13.207518,11.7313818 12.8048941,11.3644462 L6.00716065,5.15870674 C5.6225647,4.80725864 5,5.07769498 5,5.595932 L5,14.8026807 C5,15.3507015 5.68145595,15.608033 6.04802397,15.1994001 L7.87915329,13.1684522 Z" id="select-icon" fill="#575E75"></path>
            </g>
        </g>
    </g>
</svg>tool to show the dots, and double click one corner dot to delete it. (It takes a little practice.) Now you have a triangle with a long side, but it is pointing the wrong way.
3. Hold shift and use the rotation handle 
![|300x300](https://i.imgur.com/Kf3OXV8.png)
to turn it to face right or left.

In the button, we can add the following code:
```ad-scratch
~~~scratchblock
when this sprite clicked
broadcast [next v]
~~~
```

This will send a message to the frames, where the code we put there:
```ad-scratch
~~~scratchblock
when I receive [next v]
transition [1]::custom
~~~
```
will make the transition.

### Challenge
Make another button, that moves the frame backwards.

### Quick Trick

Here is a cool trick to make your buttons...cool and more user-friendly! It shows the button when our mouse is over it, and hides it when it isn't. This makes the screen less cluttered. The player can see the whole screen while the project is running, and the buttons only show up when they need them.

It uses the fact that:
* *If the ghost effect is 100, we can't see the sprite, but* 
* *Scratch can still detect that our mouse is touching it (It can't do that if the sprite is hidden)*.

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

