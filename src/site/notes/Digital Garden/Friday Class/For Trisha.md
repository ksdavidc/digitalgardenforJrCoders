---
{"dg-publish":true,"permalink":"/digital-garden/friday-class/for-trisha/"}
---


# For Trisha

I am going ot start off with an explanation of a point I think many of the friday kids (other than Saki) have not grasped:
The idea of this project is you make FRAMES that show the action like a flipbook. Maybe we will even make a flipbook???

This is an example of the kind code that kids can use for their halloween projects to move from costume or background to background. 

For Miki the code uses backdrop number, but for other kids it will be costume number, instead.
(Miki should have put his frames in a sprite, not the backdrop. Using a sprite makes certain blocks available (motion  blacks, say blocks, etc.) that are not available for backdrops.)

The main idea is nested if statement. 
if A then B else if C then D else if E then F...


```ad-scratch
~~~scratchblock


when @greenFlag clicked
clear graphic effects
this is used to get the number of the last costume. 
We use this to know when to stop.
It works because the last costume is always costume 0. 
switch backdrop to (join [0] [])
But when we actually switch to the last costume, 
the number of the costume is not 0, but the number of costumes.
set [last costume v] to (backdrop [number v])
switch backdrop to [backdrop1 v]

This is a series of nested loops.
For each costume I ask: what do I want to do 
 after pressing space  when I am at this costume. 
IF I want to move to the next costume that is fine, 
but sometimes I want to scroll through several costumes 
to create the idea of motion. Then I use a repeat until.

when [space v] key pressed::event
if <(backdrop [number v]) = [1]> then
    next backdrop
else
    if <(backdrop [number v]) = [2]> then
        next backdrop
    else
        if <(backdrop [number v]) = [3]> then
        this basically says automatically move from costume
        3 to costume 70. 
            repeat until <(backdrop [number v]) = [70]>
                next backdrop
                wait (.2) seconds
            end
        else
            if <(backdrop [number v]) \> [69]> then
            here we use the last costume to know 
            when to stop being able to scroll
                if <(backdrop [number v]) \< (last costume)> then
                    next backdrop
                else
                    this is makes it black, 
                    but replace this with game over
                    set [brightness v] effect to (-100)::looks
                end
            end
        end
    end
end

~~~
```

## **Saki**

Her project is a model of what we are trying to do. She just needs to keep adding frames and then add the scrolling code as well.


## **Daifuku**
He is actually not following the template for this project. I have fixed his project at:
[https://scratch.mit.edu/projects/759559263/](https://scratch.mit.edu/projects/759559263/)
There are comments that explain what I changed and why. The idea would be to walk through these with him.

BUT,  THen we should have him follow the template:
1. Make a storyboard. (he's done this)
2. Make frames for each image in his storyboard. 1 frame per image.
3. Add  in-between frames between each frame in the storyboard to make the action/movement natural and clearer.
4. Then use the code above to move through it.


https://scratch.mit.edu/projects/759559263/

<iframe src="https://forkphorus.github.io/embed.html?id=759559263&auto-start=false&light-content=false" width="482" height="393" allowfullscreen="true" allowtransparency="true" style="border:none;"></iframe>

#### **Miki**
He will use nested if statements to automate the control of his character.

[https://scratch.mit.edu/projects/759528097](https://scratch.mit.edu/projects/759528097)


<iframe src="https://forkphorus.github.io/embed.html?id=759528097&auto-start=false&light-content=false" width="482" height="393" allowfullscreen="true" allowtransparency="true" style="border:none;"></iframe>


## Keigo

He needs to 
* fix the flames (NOT FRAMES, but flames) under the main character's feet (so they are in the correct position)
* change the balls to 232 so they cycle through. 

## Taiga
He is jsut starting to get his sprites. He will need to draw his frames.

## Kina
Needs to make frames.