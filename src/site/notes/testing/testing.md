---
{"dg-publish":true,"permalink":"/testing/testing/","dgHomeLink":true,"dgPassFrontmatter":false}
---


This works correctly in obsidian but not on site. Probably because it needs a div to latch on to:

```scratchblock  
move (40) steps  
go to x: (0) y: (0)  
```

This works on both site and obsidian

```ad-scratch  
~~~scratchblock
move (40) steps
go to x: (0) y: (0)
~~~
```


broken text

```scratchblock  
move (40) steps  
go to x: (0) y: (0)  
magilicutty
```

This works on both site and obsidian

```ad-scratch  
~~~scratchblock  
move (40) steps
go to x: (0) y: (0)
brewster's millions
~~~
```
