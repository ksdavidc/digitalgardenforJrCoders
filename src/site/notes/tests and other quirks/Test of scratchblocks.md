---
{"dg-publish":true,"permalink":"/tests-and-other-quirks/test-of-scratchblocks/"}
---


## Inline Using .hasInlineScratch and Code

uses the custom classes plugin
and detects `.hasInlineScratch code`

This is set inline: `set [test v] to (0)`  
{ .hasInlineScratch .scratcblocks ad-scratch}

- in a list `set [test v] to (0)` { .hasInlineScratch }

## Admonition with Code Block

works well for multiline:


```ad-scratch
title: admonition with code block

This is an admonition.
~~~scratchblock
set [test v] to (0)
~~~
``` 

## Simple Callout

not working

> [!hint]- wow  
> set [test v] to (0)

## Simple Scratch Callout with .callout-scratch

using detection:  `.callout-scratch`. Works on site not here, but converts all text. not collapsing. 

> [!scratch]- as plain text  
>set [test1 v] to (0)

> [!scratch]+ as codeblock  
> this is regular text  
>`set [test2 v] to (0)`

Works on site and here, regular text gets converted.

> [!scratch]+ this has code.scratchblock
>this has a scratchblock codeblock.
>```scratchblock
>set [test3 v] to (0)
>```
>

### trying to capture just the subcodeblocks
using detection:  `.callout-scratch2`. Works on site not here, but can get it to convert the scratchblock!?

> [!scratch2]+ this is a scratch2 callout
>below is a scratchblock codeblock.
>```scratchblock
>set [test3 v] to (0)
>```
>

# Simple Code Block

works here, but not on site

```scratchblock
set [test v] to (0)
```

```scratchblocks
set [test4 v] to (0)
```

# Code Block Within Collapsible Callout Block

works with `div[class*=callout-] ` but this converts all text. The problem is getting it to convert only the code blocks or language-scratchblock  blocks  


> [!hint]- title
> `scratchblock`
>
> ```scratchblock
> set [Am I finished? v] to [No]
> broadcast [keep doing stuff v] and wait
> wait until <(Am I finished?) = [yes]>
> hide
> ```
>
> &nbsp;
> 
> backticks
> ~~~scratchblock
> set [number of cats v] to [0]
> set [number of dogs v] to [0]
> broadcast [catch animals v] and wait
> wait until <((number of cats) + (number of dogs)) > [5]>
> hide
> ~~~

> [!hint]- another
> callout-scratch
>
> ```callout-scratch
> set [Am I finished? v] to [No]
> broadcast [keep doing stuff v] and wait
> wait until <(Am I finished?) = [yes]>
> hide
> ```
>
> &nbsp;
> 
> this uses ~ ~ ~
> ~~~callout-scratch
> set [number of cats v] to [0]
> set [number of dogs v] to [0]
> broadcast [catch animals v] and wait
> wait until <((number of cats) + (number of dogs)) > [5]>
> hide
> 
> ~~~
> { .hasInlineScratch }
> this uses backticks
> 
>```callout-scratch
> set [number of cats v] to [0]
> set [number of dogs v] to [0]
> broadcast [catch animals v] and wait
> wait until <((number of cats) + (number of dogs)) > [5]>
> hide
>```
{ .hasInlineScratch }


