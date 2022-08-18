---
{"dg-publish":true,"permalink":"/prep-notes/friday-class/2022-student-m/","dgHomeLink":true,"dgPassFrontmatter":false}
---


# 2022 Student M

- [[Prep Notes/Friday Class/2022 Student M#08 19|08 19]]
	- [[Prep Notes/Friday Class/2022 Student M#08 19|ART GALLERY COVER SPRITE]]
	- [[Prep Notes/Friday Class/2022 Student M#08 19|ART GALLERY SPRITE]]
- [[Prep Notes/Friday Class/2022 Student M#08 05|08 05]]
	- [[Prep Notes/Friday Class/2022 Student M#08 05|CAT]]


<div class="blocks">

## 08 19

### ART GALLERY COVER SPRITE

> this should look like this: (some small changes)

```
when this sprite clicked
if <(MONEY) > [10]> then
    set [art gallerly v] to [1]
    hide variable [art gallerly v]
    change [MONEY v] by (-10)
    hide
end
```

> add this

```
when I receive [initialize v]
go to x: (-34) y: (-20)
show
go to [front v] layer
set [art gallerly v] to [0]
show variable [art gallerly v]
```

### ART GALLERY SPRITE

> In art gallery sprite:
> add:

``` 
when I receive [initialize v]
go to x: (-45) y: (-20)
go to [front v] layer
go [backward v] (2) layers
```

## Old Stuff
<details>Old stuff

## Old Stuff

<summary>

## 08 05

### CAT


>fix the no room available go back at the bottom,
it belongs in the classroom open else area.

>add a delete this clone on the end of 
``` 
define no room available go back
/* ... {stuff, then}
delete this clone
```


> WRITE the get money, go to and leave art gallery code
while changing the variable names

>INITIALIZE all the MAX and OCCUPANTS VARIABLES
for example

``` 
set (OCCUPANTS ART GALLERY) to (0)
```

> Change 

``` 
set (which room to go to) to (pick random (1) to (2))
```
> to
``` 
set (which room to go to) to (pick random (1) to (3))
```
...




```

### CLASSROOM COVER > ART GALLERY COVER

```
we have to finish setting this up
AFTER
if <(MONEY) > 10> then
ADD
set (CLASSROOM OPEN) to (1)


After than, COPY all the code to the art gallery cover, 
but CHANGE the variables and positions
```

### CLASSROOM > ART GALLERY

```
COPY the classroom code to the Art Gallery, 
but CHANGE variables and positions
```

</summary>
</details>
</div>