---
{"dg-publish":true,"permalink":"/prep-notes/saturday-class/student-m/","dgHomeLink":true,"dgPassFrontmatter":false}
---


## 2022 08 13 Student M

### Sword

<div class="blocks">


Add broadcast and waits for:
* initialize 
* get initialize values
* show initial game screen
* start game

```
when @greenFlag clicked
broadcast [initialize v] and wait
broadcast [get initial values v] and wait
broadcast [show initial game screen v] and wait
broadcast [start game v] and wait

```


create a new draw routine 

```
when I receive [start game v]
set pen size to (10)
forever
    if <(CURRENT BUTTON) = [1]> then
        if <<mouse down?> and <(mouse x) < [120]>> then
            go to [mouse-pointer v]
            pen down
            repeat until <not <<mouse down?> and <(mouse x) < [120]>>>
                go to [mouse-pointer v]
            end
            pen up
        end
    end
end
```




when I receive [initialize v]
hide variable [CURRENT BUTTON v]
set [CURRENT BUTTON v] to [0]
set [DRAWN v] to [0]
set [QUAD1 v] to [0]
set [QUAD1 FULL v] to [0]
set [QUAD2 v] to [0]
set [QUAD2 FULL v] to [0]
set [QUAD3 v] to [0]
set [QUAD3 FULL v] to [0]
set [QUAD4 v] to [0]
set [QUAD4 FULL v] to [0]
set [RESULT v] to [0]


 
 
 fix pen routine:
 when drawing goes to mouse, puts pen down, and keeps drawing until mouse is not longer down.
 
 change color detected to 000FF
 
 note that it is different than the color of the numbers
 
 move the sword so it draws at the end.
 
 Create variable CURRENT BUTTON. 
 When I click button set the variable. Make it only draw on CURRENT BUTTON = 1
 
 create new sprite TESTER and copy all costumes from backdrop to this sprite in same order and with same names
 
 create check current values stack and text coverage of backdrop # myblock
 
 
 
 
 
 
 
```


```


</div>


