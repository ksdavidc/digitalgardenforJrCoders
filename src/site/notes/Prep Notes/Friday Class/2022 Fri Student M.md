---
{"dg-publish":true,"permalink":"/prep-notes/friday-class/2022-fri-student-m/","dgHomeLink":true,"dgPassFrontmatter":false}
---




# 2022 Student M

- [[Prep Notes/Friday Class/2022 Fri Student M#08 19|08 19]]
	- [[Prep Notes/Friday Class/2022 Fri Student M#08 19|ART GALLERY COVER SPRITE]]
	- [[Prep Notes/Friday Class/2022 Fri Student M#08 19|ART GALLERY SPRITE]]
- [[Prep Notes/Friday Class/2022 Fri Student M#OLD STUFF|OLD STUFF]]
- [[Prep Notes/Friday Class/2022 Fri Student M#08 05|08 05]]
	- [[Prep Notes/Friday Class/2022 Fri Student M#08 05|CAT SPRITE]]
	- [[Prep Notes/Friday Class/2022 Fri Student M#08 05|CLASSROOM COVER > ART GALLERY COVER]]
	- [[Prep Notes/Friday Class/2022 Fri Student M#08 05|CLASSROOM > ART GALLERY]]



## 08 19

### ART GALLERY COVER SPRITE

> this should look like this: (some small changes)

```ad-scratch
~~~scratchblock
when this sprite clicked
if <(MONEY) > [10]> then
    set [art gallerly v] to [1]
    hide variable [art gallerly v]
    change [MONEY v] by (-10)
    hide
end
~~~
```

> add this

```ad-scratch
~~~scratchblock
when I receive [initialize v]
go to x: (-34) y: (-20)
show
go to [front v] layer
set [art gallerly v] to [0]
show variable [art gallerly v]
~~~
```

### ART GALLERY SPRITE

> In art gallery sprite:
> add:


```ad-scratch
~~~scratchblock
when I receive [initialize v]
go to x: (-45) y: (-20)
go to [front v] layer
go [backward v] (2) layers
~~~
```


## OLD STUFF
## 08 05

### CAT SPRITE

>fix the no room available go back at the bottom,
it belongs in the classroom open else area.

>add a delete this clone on the end of
```ad-scratch
~~~scratchblock
define no room available go back
/* ... {stuff, then}
delete this clone
~~~
```


WRITE the get money, go to and leave art gallery code
while changing the variable names

>INITIALIZE all the MAX and OCCUPANTS VARIABLES
for example

```ad-scratch
~~~scratchblock
set (OCCUPANTS ART GALLERY) to (0)
~~~
```

Change 

```ad-scratch
~~~scratchblock
set (which room to go to) to (pick random (1) to (2))
~~~
```
to
```ad-scratch
~~~scratchblock
set (which room to go to) to (pick random (1) to (3))
~~~
```







### CLASSROOM COVER > ART GALLERY COVER

we have to finish setting this up
AFTER
```ad-scratch
~~~scratchblock
if <(MONEY) > (10) > then
~~~
```
ADD
```ad-scratch
~~~scratchblock
set (CLASSROOM OPEN) to (1)
~~~
```

After than, COPY all the code to the art gallery cover,
but CHANGE the variables and positions


### CLASSROOM > ART GALLERY


COPY the classroom code to the Art Gallery,
but CHANGE variables and positions

