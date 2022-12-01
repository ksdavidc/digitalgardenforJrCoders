---
{"dg-publish":true,"permalink":"/digital-garden/torchlight-platformer-part-2/"}
---

I assume you have made [[Digital Garden/Torchlight Platformer Part 1, First Class|Torchlight Platformer Part 1, First Class]].

In that we had a jump routine, but it was a temporary solution. 

Here are some problems to notice:

* If you jump below a platform, the sprite is pushed up through the platform. Instead, it is more realistic for the sprite to bounce.
* And, while you are inside that platform you can move left to right. That is also unrealistic.
* The when up arrow stack lets you jump in mid-air. We used this to fix that:
```ad-scratch
title: 
~~~scratchblock
wait until < ([abs v] of (y speed)) < (8)>
~~~
```
* Still, the jump is "wobbly". 
* Right now we fall in steps, but our jump routine makes a big step up when we jump. We are going to jump in steps as well, so that we can detect platforms. 

## Organize your Code Area

It really helps to keep your code area neat. 
For example, I suggest arranging your code area in two columns:
COLUMN 1 (stacked in roughly the order they are executed):
Green Flag
Initialize
move left/right
fall
up arrow

COLUMN 2 myblocks in roughly the order they are executed
set speed
keep speed below max
change y by y speed...
pull out if touching ...


When we add new stack, we will try to fit them into the two columns.


## Distance to the ground
The first step we will take is to keep track of our distance to the ground. 
1. create a variable `distance to ground`
2. initialize it in the initialize routine:

```ad-scratch
title: hitbox, initialize stack 
~~~scratchblock
when I receive [initialize v]
...
set [distance to ground v] to [0]
...
~~~
```

Next we change `distance to ground` inside the `change y by xspeed...` stack. Note that we duplicate the condition in the `change y block`, so the two change the same way.

```ad-scratch
title: hitbox, define change y by (yspeed)
~~~scratchblock
define change y by (yspeed) by single steps
repeat ([abs v] of (yspeed::custom)::operators)
    change [distance to ground v] by ((-1) * <not <touching [walls v]?>>)
    change y by ((-1) * <not <touching [walls v]?>>)
end
~~~
```

we also change  `pull out if touching...` but in a slightlly different way. 

If we are touching the wall and falling, then we want to seet `Distance to the ground` will to zero.  One way to do is

```ad-scratch
~~~scratchblock

  
if <(<falling?::custom> * <touching [walls v]?>) = (1)> then
    set [distance to ground v] to (0)
end

~~~
```

It runs a little faster if we don't use an `if`, but put it all on one line. We can do this with a change block. If I have 10, and I change it by -10, I get zero. This is true for any number. We multiply `distance to ground` by **-1** and then multiply by the condition.

```ad-scratch
title: 
~~~scratchblock
change [distance to ground v] by (((distance to ground) * (-1)) * (<falling?::custom> * <touching [walls v]?>))
~~~
```

We put all this in our pull up stack:
```ad-scratch
title: hitbox, define pull up
~~~scratchblock
define pull up or down if touching walls and <falling?> or not
change [y speed v] by (<touching [walls v]?> * ((-1) * (y speed)))
change [distance to ground v] by (((distance to ground) * (-1)) * (<falling?::custom> * <touching [walls v]?>))
change y by (<touching [walls v]?> * (falling?::custom)
~~~
```

Notice that:
## Change jump routine
Now we can change the jump routine so that we only jump when we are close to the ground.

First, to make sure we are only jumping at the right time, let's change from a `when up arrow pressed` to `receive jump`. Delete **this entire stack**:

```ad-scratch
title: hitbox, when up arrow stack
~~~scratchblock
when [up arrow v] key pressed
...
~~~
```

and replace it with:

```ad-scratch
title: hitbox, jump stack
~~~scratchblock
when I receive [jump v]
if <key [up arrow v] pressed?>  then
    change [y speed v] by ((20) * <(distance to ground) \< [5]>)
    change [distance to ground v] by ((20) * <(distance to ground) \< [5]>)
end
broadcast [move left / right v]
~~~
```
This changes the speed by 20 only if we are close to the ground.

Then change the `broadcast` at the bottom of fall like this:

```ad-scratch
title: hitbox, fall stack
~~~scratchblock
not
broadcast [move left / right v]

instead
broadcast [jump v]

~~~
```
Run it to test it. Is it working yet? 

No, it shouldn't be. We have one more thing to do. The problem is that, as I wrote above:

* Right now we fall in steps, but our jump routine makes a big step up when we jump. We are going to jump in steps as well, so that we can detect platforms. 

So, how do we do that? We keep track of whether we are falling by making a new variable to keep track of the sign:

```ad-scratch
title: 
~~~scratchblock
set [sign of y speed v] to (<(y speed) \> [0]> - <(y speed) \< [0]>)
~~~
```
This will be **1** if we are jumping and **-1** if we are falling. Then we put this is in the change y by stack, and change **-1** to `sign of y speed`. 


```ad-scratch
title: hitbox, define change y by (yspeed)
~~~scratchblock
define change y by (yspeed) by single steps
set [sign of y speed v] to (<(y speed) \> [0]> - <(y speed) \< [0]>)
repeat ([abs v] of (yspeed::custom)::operators)
    change [distance to ground v] by ((sign of y speed) * <not <touching [walls v]?>>)
    change y by ((sign of y speed) * <not <touching [walls v]?>>)
end
~~~
```

That should work. You might have to change the numbers in the **jump stack** for the  `change y speed` and `distance to ground` block to make it work. Things like the size of your hitbox and what your platform looks like can make a difference.

## Climbing walls
If you make a slope in your wall, you will find that you pass right through it. We haven't taught the x direction to recognize walls yes.

Here's what we do if we find ourselves in a wall. 
1. Try 3 times to go up and get out. 
	1. If we fail, go back and undo the step that got us there.
		1. The undo is tricky because we could have been going right or left. 
			1. So we take **1 step left**. If that works, ok.
			2. If it doesn't, we take **2 steps right.** that should work.
			3. We know one of them has to work.
	2. If we succeed, stay.
<style>
.container {font-family: sans-serif; text-align: center;}
.button-wrapper button {z-index: 1;height: 40px; width: 100px; margin: 10px;padding: 5px;}
.excalidraw .App-menu_top .buttonList { display: flex;}
.excalidraw-wrapper { height: 800px; margin: 50px; position: relative;}
:root[dir="ltr"] .excalidraw .layer-ui__wrapper .zen-mode-transition.App-menu_bottom--transition-left {transform: none;}
</style><script src="https://unpkg.com/react@17/umd/react.production.min.js"></script><script src="https://unpkg.com/react-dom@17/umd/react-dom.production.min.js"></script><script type="text/javascript" src="https://unpkg.com/@excalidraw/excalidraw@0.12.0/dist/excalidraw.production.min.js"></script><div id="HatlinkClimbexcalidraw.md1"></div><script>(function(){const InitialData={"type":"excalidraw","version":2,"source":"https://excalidraw.com","elements":[{"type":"rectangle","version":785,"versionNonce":933004649,"isDeleted":false,"id":"HITczZ2WnSgBNgqwybQtk","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-671.3791207785852,"y":-92.08530328351763,"strokeColor":"#000000","backgroundColor":"#15aabf","width":580.8837890625,"height":391.697998046875,"seed":1137687143,"groupIds":[],"strokeSharpness":"sharp","boundElements":[],"updated":1669398506952,"link":null,"locked":false},{"type":"rectangle","version":754,"versionNonce":98808839,"isDeleted":false,"id":"QwlCzrxJb6gmmsNx83g1N","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":5.4980536612531115,"x":-624.7237390742927,"y":52.424326195082145,"strokeColor":"#000000","backgroundColor":"#fa5252","width":110.97502255032714,"height":70.5779453048153,"seed":3881479,"groupIds":[],"strokeSharpness":"sharp","boundElements":[{"id":"77_3WgWoV124rznVtUSWu","type":"arrow"}],"updated":1669398503577,"link":null,"locked":false},{"type":"rectangle","version":637,"versionNonce":40285161,"isDeleted":false,"id":"0O1qXktXwk04dqnjbqOwC","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-672.1895121259449,"y":102.46848821189565,"strokeColor":"#000000","backgroundColor":"#fa5252","width":141.7652202405428,"height":52.170654296875,"seed":1844233097,"groupIds":[],"strokeSharpness":"round","boundElements":[{"id":"77_3WgWoV124rznVtUSWu","type":"arrow"}],"updated":1669398503577,"link":null,"locked":false},{"type":"rectangle","version":795,"versionNonce":1132305191,"isDeleted":false,"id":"1Q6kG176Q1p-Fz0YFNiRr","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-616.2092453850149,"y":49.412257032350496,"strokeColor":"#000000","backgroundColor":"#4c6ef5","width":57.265625,"height":54.74920654296875,"seed":1188681095,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1669398503577,"link":null,"locked":false},{"type":"rectangle","version":769,"versionNonce":1897549513,"isDeleted":false,"id":"GKs6z3LqMjc2hPk32BCSL","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":5.4980536612531115,"x":-468.8632966959966,"y":-19.69742159987547,"strokeColor":"#000000","backgroundColor":"#fa5252","width":110.86530381551387,"height":70.57794530481532,"seed":970127975,"groupIds":[],"strokeSharpness":"sharp","boundElements":[{"id":"kFVRM3-_zUgiCwV_k7KD7","type":"arrow"}],"updated":1669398503577,"link":null,"locked":false},{"type":"rectangle","version":907,"versionNonce":2139987527,"isDeleted":false,"id":"C0iNKnFlVGz8IhriqdCVF","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-494.4249171206827,"y":31.3441089601976,"strokeColor":"#000000","backgroundColor":"#fa5252","width":141.7652202405428,"height":52.170654296875,"seed":1341642345,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1669398503577,"link":null,"locked":false},{"type":"text","version":577,"versionNonce":1079479721,"isDeleted":false,"id":"0Dkahe6U","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-465.7727243523846,"y":37.87620060287857,"strokeColor":"#000000","backgroundColor":"transparent","width":87,"height":38,"seed":1025743337,"groupIds":[],"strokeSharpness":"sharp","boundElements":[{"id":"kFVRM3-_zUgiCwV_k7KD7","type":"arrow"}],"updated":1669398503577,"link":null,"locked":false,"fontSize":15.08601053930055,"fontFamily":1,"text":"try 3 times\nto get out","rawText":"try 3 times\nto get out","baseline":33,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"try 3 times\nto get out"},{"type":"freedraw","version":41,"versionNonce":1022377319,"isDeleted":false,"id":"1Lay8SOcx7QnOL7OHQfLE","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-697.5963905736019,"y":190.70445409794428,"strokeColor":"#000000","backgroundColor":"transparent","width":0.21416915090458133,"height":0.10710063733552033,"seed":1108635273,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1669398503577,"link":null,"locked":false,"points":[[0,0],[0,-0.10710063733552033],[-0.10710063733540665,-0.10710063733552033],[-0.21416915090458133,-0.10710063733552033],[0,0]],"lastCommittedPoint":null,"simulatePressure":true,"pressures":[]},{"type":"rectangle","version":1168,"versionNonce":2001334409,"isDeleted":false,"id":"hUN9Mqir3nDZ_A2RDwsqh","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":5.697900419059218,"x":-452.6714532579249,"y":184.34520628119435,"strokeColor":"#000000","backgroundColor":"#fa5252","width":110.86530381551387,"height":70.57794530481532,"seed":1138638375,"groupIds":[],"strokeSharpness":"sharp","boundElements":[],"updated":1669398503577,"link":null,"locked":false},{"type":"rectangle","version":1113,"versionNonce":1861351559,"isDeleted":false,"id":"6-qeHxUvLhYDa0SEwOFuf","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-461.31599189141707,"y":108.53728237435794,"strokeColor":"#000000","backgroundColor":"#4c6ef5","width":57.265625,"height":54.74920654296875,"seed":516512713,"groupIds":[],"strokeSharpness":"round","boundElements":[{"id":"ca0Kxu526HZvwVmwJaIzP","type":"arrow"}],"updated":1669398503577,"link":null,"locked":false},{"type":"arrow","version":977,"versionNonce":732755817,"isDeleted":false,"id":"ca0Kxu526HZvwVmwJaIzP","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-402.7686671609739,"y":184.10602009579057,"strokeColor":"#5c940d","backgroundColor":"transparent","width":25.75433028371708,"height":19.0004368832237,"seed":300015943,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1669398503577,"link":null,"locked":false,"startBinding":null,"endBinding":{"elementId":"6-qeHxUvLhYDa0SEwOFuf","focus":0.5722513877772222,"gap":1.819094295240177},"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[23.845150596217138,-11.151492470189112],[-1.9091796874999432,-19.0004368832237]]},{"type":"rectangle","version":1028,"versionNonce":1800359847,"isDeleted":false,"id":"X3alj4MXodew3LxFIn2U1","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-494.0749733536636,"y":221.1217928651161,"strokeColor":"#000000","backgroundColor":"#fa5252","width":141.7652202405428,"height":52.170654296875,"seed":1587346089,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1669398503577,"link":null,"locked":false},{"type":"text","version":699,"versionNonce":801907273,"isDeleted":false,"id":"DODmyuJJ","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-465.3156799480299,"y":227.6538845077971,"strokeColor":"#000000","backgroundColor":"transparent","width":87,"height":38,"seed":566501479,"groupIds":[],"strokeSharpness":"sharp","boundElements":[{"id":"DUumFiWLmBjLGs_EetedM","type":"arrow"}],"updated":1669398503577,"link":null,"locked":false,"fontSize":15.08601053930055,"fontFamily":1,"text":"try 3 times\nto get out","rawText":"try 3 times\nto get out","baseline":33,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"try 3 times\nto get out"},{"type":"arrow","version":1234,"versionNonce":473219783,"isDeleted":false,"id":"DUumFiWLmBjLGs_EetedM","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-402.650788224154,"y":219.9125193762183,"strokeColor":"#5c940d","backgroundColor":"transparent","width":25.75433028371708,"height":19.573267886513236,"seed":1683602825,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1669398503577,"link":null,"locked":false,"startBinding":{"elementId":"DODmyuJJ","focus":-0.44746274891167764,"gap":7.741365131578789},"endBinding":null,"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[24.83089959353032,-11.724323473478648],[-0.9234306901867626,-19.573267886513236]]},{"type":"arrow","version":982,"versionNonce":8581417,"isDeleted":false,"id":"Xw8N_1OUhSri1r5ND0nMp","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-402.7423741774338,"y":201.71454124513974,"strokeColor":"#5c940d","backgroundColor":"transparent","width":23.845150596217138,"height":17.512576434273342,"seed":1968274311,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1669398503577,"link":null,"locked":false,"startBinding":null,"endBinding":null,"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[23.845150596217138,-11.151492470189112],[1.555677305452548,-17.512576434273342]]},{"type":"rectangle","version":1262,"versionNonce":1916719591,"isDeleted":false,"id":"Cs-BTQ3pG6YJ6XuU_pqCK","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":5.697900419059218,"x":-254.46277467670393,"y":189.37326942618475,"strokeColor":"#000000","backgroundColor":"#fa5252","width":110.86530381551387,"height":70.57794530481532,"seed":691888905,"groupIds":[],"strokeSharpness":"sharp","boundElements":[],"updated":1669398503577,"link":null,"locked":false},{"type":"rectangle","version":1219,"versionNonce":1933370377,"isDeleted":false,"id":"NoZg0bqhLaX6phTdAEFvq","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-262.89311203552506,"y":133.45824488201274,"strokeColor":"#000000","backgroundColor":"#4c6ef5","width":57.265625,"height":54.74920654296875,"seed":503639559,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1669398503577,"link":null,"locked":false},{"type":"rectangle","version":1126,"versionNonce":1936896775,"isDeleted":false,"id":"uHziZka7EVr3PdR_8IFpk","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-295.6463042741318,"y":226.14985601010656,"strokeColor":"#000000","backgroundColor":"#fa5252","width":141.7652202405428,"height":52.170654296875,"seed":2003277095,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1669398522075,"link":null,"locked":false},{"type":"text","version":1285,"versionNonce":603290345,"isDeleted":false,"id":"D17GKRMs","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-665.249087337749,"y":-20.962651781642563,"strokeColor":"#000000","backgroundColor":"transparent","width":129,"height":38,"seed":739071079,"groupIds":[],"strokeSharpness":"sharp","boundElements":[{"id":"DUumFiWLmBjLGs_EetedM","type":"arrow"}],"updated":1669398503577,"link":null,"locked":false,"fontSize":15.08601053930055,"fontFamily":1,"text":"Oops, we stepped\ninto the slope!","rawText":"Oops, we stepped\ninto the slope!","baseline":33,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"Oops, we stepped\ninto the slope!"},{"type":"rectangle","version":950,"versionNonce":1549976615,"isDeleted":false,"id":"TjHHvGDF3puKSutmdm99r","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":5.4980536612531115,"x":-248.7945950870605,"y":-24.304925587870244,"strokeColor":"#000000","backgroundColor":"#fa5252","width":114.5488716286079,"height":72.92294088676715,"seed":1573399719,"groupIds":[],"strokeSharpness":"sharp","boundElements":[{"id":"eB4dWzTwXrh_9401X3NUZ","type":"arrow"}],"updated":1669398503577,"link":null,"locked":false},{"type":"rectangle","version":1136,"versionNonce":73858857,"isDeleted":false,"id":"JhdIrqCZPfOAC4rH36ShT","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-297.41047124505013,"y":27.0319455814657,"strokeColor":"#000000","backgroundColor":"#fa5252","width":182.39276566615874,"height":57.377672204712006,"seed":1671140681,"groupIds":[],"strokeSharpness":"round","boundElements":[{"id":"eB4dWzTwXrh_9401X3NUZ","type":"arrow"}],"updated":1669398508389,"link":null,"locked":false},{"type":"rectangle","version":1209,"versionNonce":1944430407,"isDeleted":false,"id":"UyITH7jDsGrlI4cW_mVtW","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-314.8880936062184,"y":-27.7950675147503,"strokeColor":"#000000","backgroundColor":"#4c6ef5","width":59.168310563354716,"height":56.56828255749635,"seed":1703542727,"groupIds":[],"strokeSharpness":"round","boundElements":[{"id":"eB4dWzTwXrh_9401X3NUZ","type":"arrow"}],"updated":1669398503577,"link":null,"locked":false},{"type":"rectangle","version":1259,"versionNonce":1679856809,"isDeleted":false,"id":"_QZdLO2RrvqGKoTSyDMpT","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-465.1768927323195,"y":-76.94890315688733,"strokeColor":"#000000","backgroundColor":"#4c6ef5","width":57.265625,"height":54.74920654296875,"seed":349887753,"groupIds":[],"strokeSharpness":"round","boundElements":[{"id":"ca0Kxu526HZvwVmwJaIzP","type":"arrow"},{"id":"uAr-oTCL8XF69DZW1W7tG","type":"arrow"}],"updated":1669398503577,"link":null,"locked":false},{"type":"arrow","version":1260,"versionNonce":1532962407,"isDeleted":false,"id":"uAr-oTCL8XF69DZW1W7tG","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-407.593427094123,"y":-5.003891014103708,"strokeColor":"#5c940d","backgroundColor":"transparent","width":23.845150596217138,"height":16.23491226253948,"seed":197255145,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1669398503577,"link":null,"locked":false,"startBinding":null,"endBinding":{"elementId":"_QZdLO2RrvqGKoTSyDMpT","focus":0.6138975051088584,"gap":2.630323852904212},"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[23.845150596217138,-11.151492470189112],[2.3124832147076972,-16.23491226253948]]},{"type":"arrow","version":1475,"versionNonce":1784289161,"isDeleted":false,"id":"kFVRM3-_zUgiCwV_k7KD7","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-407.4755481573031,"y":30.80260826632407,"strokeColor":"#5c940d","backgroundColor":"transparent","width":25.75433028371708,"height":19.573267886513236,"seed":1908092711,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1669398503577,"link":null,"locked":false,"startBinding":{"elementId":"0Dkahe6U","focus":-0.482731929049218,"gap":7.073592336554498},"endBinding":null,"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[24.83089959353032,-11.724323473478648],[-0.9234306901867626,-19.573267886513236]]},{"type":"arrow","version":1225,"versionNonce":295420295,"isDeleted":false,"id":"D9VsZblOLojJvzMHwcir6","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-407.4600334732474,"y":12.6046301352455,"strokeColor":"#5c940d","backgroundColor":"transparent","width":23.845150596217138,"height":17.512576434273342,"seed":2117073609,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1669398503577,"link":null,"locked":false,"startBinding":null,"endBinding":null,"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[23.845150596217138,-11.151492470189112],[1.555677305452548,-17.512576434273342]]},{"type":"text","version":1021,"versionNonce":941637225,"isDeleted":false,"id":"EB4lLJcT","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-551.9714572707868,"y":57.84916289805699,"strokeColor":"#000000","backgroundColor":"transparent","width":38,"height":19,"seed":452264457,"groupIds":[],"strokeSharpness":"sharp","boundElements":[{"id":"DUumFiWLmBjLGs_EetedM","type":"arrow"}],"updated":1669398503577,"link":null,"locked":false,"fontSize":15.08601053930055,"fontFamily":1,"text":"slope","rawText":"slope","baseline":14,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"slope"},{"type":"arrow","version":2125,"versionNonce":131594407,"isDeleted":false,"id":"eB4dWzTwXrh_9401X3NUZ","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-190.49652885069844,"y":-31.365941530419676,"strokeColor":"#5c940d","backgroundColor":"transparent","width":70.44470087085082,"height":53.11504594275629,"seed":1972338023,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1669398503577,"link":null,"locked":false,"startBinding":null,"endBinding":{"elementId":"UyITH7jDsGrlI4cW_mVtW","focus":0.8329123881653764,"gap":1.6383360410465428},"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[6.859782719732119,28.516532041266895],[-63.5849181511187,53.11504594275629]]},{"type":"text","version":1125,"versionNonce":1268128231,"isDeleted":false,"id":"SGhpAOig","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-242.60614230724366,"y":238.46981893884654,"strokeColor":"#000000","backgroundColor":"transparent","width":48.63991827713817,"height":24.97725533150339,"seed":152515753,"groupIds":[],"strokeSharpness":"sharp","boundElements":[{"id":"DUumFiWLmBjLGs_EetedM","type":"arrow"}],"updated":1669398526606,"link":null,"locked":false,"fontSize":19.831954588097943,"fontFamily":1,"text":"Stay","rawText":"Stay","baseline":17.97725533150339,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"Stay"},{"type":"text","version":1265,"versionNonce":1405111239,"isDeleted":false,"id":"ybxu1UgZ","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-357.2880261609201,"y":-64.42743977026785,"strokeColor":"#000000","backgroundColor":"transparent","width":52,"height":24,"seed":1430392999,"groupIds":[],"strokeSharpness":"sharp","boundElements":[{"id":"DUumFiWLmBjLGs_EetedM","type":"arrow"}],"updated":1669398503577,"link":null,"locked":false,"fontSize":18.634518511062545,"fontFamily":1,"text":"FAIL!","rawText":"FAIL!","baseline":17,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"FAIL!"},{"type":"text","version":1371,"versionNonce":3322727,"isDeleted":false,"id":"Pn3tp5qQ","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-252.29303906356563,"y":31.800196592044337,"strokeColor":"#000000","backgroundColor":"transparent","width":82,"height":25,"seed":1140146825,"groupIds":[],"strokeSharpness":"sharp","boundElements":[{"id":"DUumFiWLmBjLGs_EetedM","type":"arrow"},{"id":"eB4dWzTwXrh_9401X3NUZ","type":"arrow"}],"updated":1669398512900,"link":null,"locked":false,"fontSize":19.994068729120446,"fontFamily":1,"text":"Go back","rawText":"Go back","baseline":18,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"Go back"},{"type":"arrow","version":1610,"versionNonce":561068775,"isDeleted":false,"id":"77_3WgWoV124rznVtUSWu","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-650.7975333939639,"y":102.60835988898037,"strokeColor":"#5c940d","backgroundColor":"transparent","width":37.217743626219544,"height":21.204761705900523,"seed":758348329,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1669398503577,"link":null,"locked":false,"startBinding":{"elementId":"QwlCzrxJb6gmmsNx83g1N","focus":-1.3228029876831593,"gap":12.730000914015818},"endBinding":{"elementId":"0O1qXktXwk04dqnjbqOwC","focus":0.13607954566585798,"gap":1},"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[17.883786556421,-21.204761705900523],[37.217743626219544,-0.7703504060444857]]},{"type":"text","version":1360,"versionNonce":1434553097,"isDeleted":false,"id":"UAA9IS5w","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-392.3520692059641,"y":112.94017992521594,"strokeColor":"#000000","backgroundColor":"transparent","width":121,"height":31,"seed":1877338119,"groupIds":[],"strokeSharpness":"sharp","boundElements":[{"id":"DUumFiWLmBjLGs_EetedM","type":"arrow"}],"updated":1669398503577,"link":null,"locked":false,"fontSize":24.713242332584898,"fontFamily":1,"text":"SUCCESS!","rawText":"SUCCESS!","baseline":22,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"SUCCESS!"},{"type":"text","version":1422,"versionNonce":1028449991,"isDeleted":false,"id":"klQLOv3C","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-282.84690554926544,"y":55.155297302419875,"strokeColor":"#000000","backgroundColor":"transparent","width":155,"height":25,"seed":600807465,"groupIds":[],"strokeSharpness":"sharp","boundElements":[{"id":"DUumFiWLmBjLGs_EetedM","type":"arrow"},{"id":"eB4dWzTwXrh_9401X3NUZ","type":"arrow"}],"updated":1669398511033,"link":null,"locked":false,"fontSize":19.994068729120446,"fontFamily":1,"text":"set speed to 0","rawText":"set speed to 0","baseline":18,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"set speed to 0"},{"id":"kgVdRNpq","type":"text","x":-230.7636941538604,"y":239.73518315854406,"width":12,"height":25,"angle":0,"strokeColor":"#000000","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"groupIds":[],"strokeSharpness":"sharp","seed":62901769,"version":2,"versionNonce":948643049,"isDeleted":true,"boundElements":null,"updated":1669398522077,"link":null,"locked":false,"text":"","rawText":"","fontSize":20,"fontFamily":1,"textAlign":"center","verticalAlign":"middle","baseline":18,"containerId":"uHziZka7EVr3PdR_8IFpk","originalText":""}],"appState":{"theme":"dark","viewBackgroundColor":"transparent","currentItemStrokeColor":"#000000","currentItemBackgroundColor":"transparent","currentItemFillStyle":"solid","currentItemStrokeWidth":1,"currentItemStrokeStyle":"solid","currentItemRoughness":1,"currentItemOpacity":100,"currentItemFontFamily":1,"currentItemFontSize":20,"currentItemTextAlign":"left","currentItemStrokeSharpness":"sharp","currentItemStartArrowhead":null,"currentItemEndArrowhead":"arrow","currentItemLinearStrokeSharpness":"round","gridSize":null,"colorPalette":{}},"files":{}};InitialData.scrollToContent=true;App=()=>{const e=React.useRef(null),t=React.useRef(null),[n,i]=React.useState({width:void 0,height:void 0});return React.useEffect(()=>{i({width:t.current.getBoundingClientRect().width,height:t.current.getBoundingClientRect().height});const e=()=>{i({width:t.current.getBoundingClientRect().width,height:t.current.getBoundingClientRect().height})};return window.addEventListener("resize",e),()=>window.removeEventListener("resize",e)},[t]),React.createElement(React.Fragment,null,React.createElement("div",{className:"excalidraw-wrapper",ref:t},React.createElement(ExcalidrawLib.Excalidraw,{ref:e,width:n.width,height:n.height,initialData:InitialData,viewModeEnabled:!0,zenModeEnabled:!0,gridModeEnabled:!1})))},excalidrawWrapper=document.getElementById("HatlinkClimbexcalidraw.md1");ReactDOM.render(React.createElement(App),excalidrawWrapper);})();</script>




```ad-scratch
title: 
~~~scratchblock
when I receive [climb v]
if <touching [walls v]?> then
    change y by (1)
    if <touching [walls v]?> then
        change y by (1)
        if <touching [walls v]?> then
            change y by (1)
            if <touching [walls v]?> then
                /: [reset x and y] \:: pen reporter stack #1234FF::custom
                change x by ((x speed) * (-1))
                change y by (-3)
                set [x speed v] to [0]
            end
        end
    end
end
broadcast [fall v]
~~~
```

### Wrapping


```ad-scratch
title: 
~~~scratchblock

when I receive [wrap v]
if <(x position) \> [238]> then
    begin scene ((screen) + (1)) in direction [-1]::custom
else
    if <<(x position) \< [-238]> and <(screen) \> [1]>> then
        begin scene ((screen) + (-1)) in direction [1]::custom
    end
end
broadcast [climb v]

~~~
```



```ad-scratch
title: 
~~~scratchblock
define begin scene (scene) in direction (x)
set x to ((x::custom) * (233))
set [screen v] to (scene::custom)
broadcast [new screen v]
stop [other scripts in sprite v]
wait (0) seconds
Fix collisions in [0]::custom

~~~
```


```ad-scratch
title: 
~~~scratchblock
define Fix collisions in (direction)
set [distance v] to [1]
point in direction (direction::custom)
repeat (64)
    if <not <touching [walls v]?>> then
        stop [this script v]
    end
    move (distance::variables) steps
    turn @turnRight (180) degrees::motion
    change [distance v] by (1)
end
~~~
```


```ad-scratch
title: Walls, switch costume stacks
~~~scratchblock
when gf clicked
switch costume to (screen)

when I receive (new screen v)
switch costume to (screen)


~~~
```


### Make visual effects

Torchlight
Use gradient


LEYERS

from the front: 
	costume
	hitbox
	tails
	walls
	lava
	torch
	background

Overlay
Walls
Lava

	game start
	change to game start






when @greenFlag clicked
set [mode v] to [0]
broadcast [initialize v]

when I receive [move left / right v]
set xspeed::custom
change x by (x speed)
broadcast [wrap v]

when I receive [wrap v]
if <(x position) \> [238]> then
    begin scene ((screen) + (1)) goto x [-1]::custom
else
    if <<(x position) \< [-238]> and <(screen) \> [1]>> then
        begin scene ((screen) + (-1)) goto x [1]::custom
    end
end
broadcast [climb v]

when I receive [climb v]
set [lifted up v] to [0]
climb::custom
broadcast [fall v]

when I receive [fall v]
change [y speed v] by (-1)
change y  by (y speed) by single steps::custom
pull up or down if touching walls and <(y speed) \< [0]> or not::custom
broadcast [check lava v]

when I receive [jump v]
if <<<key [up arrow v] pressed?> or <key [space v] pressed?>> or <key [z v] pressed?>> then
    /: [only jump if near the ground]::custom
    change [y speed v] by ((4) * <(distance to ground) \< [5]>)
end
start sound [jump v]
broadcast [move left / right v]

define anothe ray to set the xspeed and facing
change [x speed2 v] by ((<(x speed2) \< [0]> - <(x speed2) \> [0]>) * <<not <key [left arrow v] pressed?>> and <not <key [right arrow v] pressed?>>>)
change [x speed2 v] by (<key [right arrow v] pressed?> - <key [left arrow v] pressed?>)
change [x speed2 v] by (((4) - (x speed2)) * <(x speed2) \> [4]>)
change [x speed2 v] by (((-4) - (x speed2)) * <(x speed2) \< [-4]>)
change [facing2 v] by (((1) - (facing2)) * <key [left arrow v] pressed?>)
change [facing2 v] by (((2) - (facing2)) * <key [right arrow v] pressed?>)

define pull up or down if touching walls and <falling?> or not
if <touching [Lava v]?> then
    change y by (1)
    broadcast [touching lava v]
end
change [distance to ground v] by (1)
/: [if touching a wall and falling, set distance to 0, else keep the same]::custom
change [distance to ground v] by (<touching [walls v]?> * (<falling?::custom> * ((distance to ground) * (-1))))
/: [if touching a wall, set y speed to zero, else keep the same]::custom
change [y speed v] by (<touching [walls v]?> * ((-1) * (y speed)))
/: [if touching a wall, go up if falling, down if jumping]::custom
change y by (<touching [walls v]?> * (<falling?::custom> - <not <falling?::custom>>))



define set xspeed
if <<not <key [left arrow v] pressed?>> and <not <key [right arrow v] pressed?>>> then
    change [x speed v] by (<(x speed) \< [0]> - <(x speed) \> [0]>)
else
    change [x speed v] by (<key [right arrow v] pressed?> - <key [left arrow v] pressed?>)
end
set [sign of x v] to (<(x speed) \> [0]> - <(x speed) \< [0]>)
if <(x speed) \> [4]> then
    set [x speed v] to [4]
end
if <(x speed) \< [-4]> then
    set [x speed v] to [-4]
end

when I receive [initialize v]
say []
switch costume to [costume1 v]
set size to (((64) / (44)) * (50)) %
set [ghost v] effect to (90)::looks
set [color v] effect to (25)::looks
go to x: (-205) y: (65)
set [x speed v] to [0]
set [x speed2 v] to [0]
set [y speed v] to [0]
set [grounded v] to [0]
set [screen v] to [0]
set [distance to ground v] to [0]
set [touched lava v] to [0]
broadcast [move left / right v]

define change costume 2
if <([abs v] of (x speed)::operators) \> [0]> then
    point in direction ((sign of x) * (90))
    next costume
else
    switch costume to [costume1 v]
end

when I receive [touching lava v]
if <(mode) = [0]> then
    set [touched lava v] to [1]
end

when I receive [check lava v]
if <(touched lava) = [1]> then
    set y to (65)
    broadcast [set scene v]
end
broadcast [jump v]

when [e v] key pressed::event
change [mode v] by (<(mode) = [0]> - <(mode) = [1]>)

define begin scene (scene) goto x (x)
/: [simplified from griffpatch e2]::custom
set x to ((x::custom) * (233))
set [screen v] to (scene::custom)
broadcast [new screen v]
stop [other scripts in sprite v]
wait (0) seconds
Fix collisions in [0]::custom

define Fix collisions in (direction)
set [distance v] to [1]
point in direction (direction::custom)
repeat (64)
    if <not <touching [walls v]?>> then
        stop [this script v]
    end
    move (distance::variables) steps
    turn @turnRight (180) degrees::motion
    change [distance v] by (1)
end

when I receive [set scene v]
set x to (-233)
set [touched lava v] to [0]
broadcast [move left / right v]

define climb
repeat (4)
    if <touching [walls v]?> then
        change y by (.5)
        change [lifted up v] by (-.5)
    end
end
point in direction (last angle)
if <touching [walls v]?> then
    change x by ((x speed) * (-1))
    change y by (lifted up)
    if <touching [walls v]?> then
        change x by (-3)
        if <touching [walls v]?> then
            change x by (6)
        end
    end
    set [x speed v] to [0]
    set [x speed2 v] to [0]
end

```ad-scratch
title: 
~~~scratchblock
define change y  by (yspeed) by single steps
1 for going up, -1 for going down, 0 if still
set [sign of y speed v] to (<(y speed) \> [0]> - <(y speed) \< [0]>)
repeat ([abs v] of (yspeed::custom)::operators)
    change y by ((sign of y speed) * <not <<touching [walls v]?> or <<touching [Lava v]?> and <(mode) = [1]>>>>)
end
at this point we are either mid air or just touching wall

~~~
```