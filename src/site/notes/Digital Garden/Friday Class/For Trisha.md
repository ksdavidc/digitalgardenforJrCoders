---
{"dg-publish":true,"permalink":"/digital-garden/friday-class/for-trisha/"}
---


# For Trisha



This is an example of the kind code that kids can use for their halloween projects to move from costume or background to background. 

For Miki it will be backdrop number, but for other kids it will be costume number, instead.
The main idea is nested if statement. 
```ad-scratch
~~~scratchblock


when @greenFlag clicked
clear graphic effects
this is used to get the number of the last costume. We use this to know when to stop.
It works because the last costume is always costume 0. 
switch backdrop to (join [0] [])
But when we actually switch to the last costume, the number of the costume is not 0, but the number of costumes.
set [last costume v] to (backdrop [number v])
switch backdrop to [backdrop1 v]

This is a series of nested loops.
For each costume I ask: what do I want to do 
(after pressing space) when I am at this costume. 
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
                if <(backdrop [number v]) \< (last costume)> then
                    next backdrop
                else
                    set [brightness v] effect to (-100)::looks
                end
            end
        end
    end
end

~~~
```



#### **Daifuku**
He is actually not following the template for this project. I have fixed his project at:
https://scratch.mit.edu/projects/755406245/

I think we should first fix his project. 
THen we should have him follow the template:
1. Make a storyboard.
2. Make frames for each image in his storyboard.
3. Make the in-between frames between each frame in the storyboard.
4. Then uuse the code above
5. 

<iframe style="width:-webkit-fill-available;" src="https://scratch-viewer.techlit.app/view#project=759559263&showDownload=true" height="500px" />



#### **Saki**

#### **Miki**
He will use nested if statements to automate the control of his character.

<iframe style="width:-webkit-fill-available;" src="https://scratch-viewer.techlit.app/view#project=759601159&showDownload=true" height="500px" />
   
   