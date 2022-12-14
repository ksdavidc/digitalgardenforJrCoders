---
{"dg-publish":true,"permalink":"/digital-garden/torchlight-platformer-part-2/"}
---


# Torchlight Platformer Part 2

Please complete [[Digital Garden/Torchlight Platformer Part 1, First Class\|Torchlight Platformer Part 1, First Class]] before starting here.

In that we had a jump routine, but it was a temporary solution. 

Here are some problems to notice:

- If you jump below a platform, the sprite is pushed up through the platform. Instead, it is more realistic for the sprite to bounce.
- And, while you are inside that platform you can move left to right. That is also unrealistic.
- The when up arrow stack lets you jump in mid-air. We used this to fix that:

```ad-scratch
title: 
~~~scratchblock
wait until < ([abs v] of (y speed)) < (8)>
~~~
```

- Still, the jump is "wobbly". 
- Right now we fall in steps, but our jump routine makes a big step up when we jump. We are going to jump in steps as well, so that we can detect platforms. 

## Organize Your Code Area

It really helps to keep your code area neat. For example, I suggest arranging your code area in two columns:  
\  
COLUMN 1 (stacked in roughly the order they are executed): 
1) Green Flag
2) Initialize
3) move left/right
4) fall
5) up arrow

COLUMN 2 (myblocks in roughly the order they are executed):
1) set speed
2) keep speed below max
3) change y by y speed…
4) pull out if touching …


When we add new stack, we will try to fit them into the two columns.

## Distance to the Ground

### Initialize Distance

The first step we will take is to keep track of our distance to the ground. 
1) create a variable `distance to ground`
2) initialize it in the initialize routine:

```ad-scratch
title: hitbox, initialize stack 
~~~scratchblock
when I receive [initialize v]
...
set [distance to ground v] to [0]
...
~~~
```

### Add Distance to Change Y Stack

Next we change `distance to ground` inside the `change y by xspeed…` stack. Note that we duplicate the condition in the `change y block`, so the two change the same way.

```ad-scratch
title: hitbox, define change y by (yspeed)
~~~scratchblock
define change y by (yspeed) by single steps
repeat ([abs v] of (yspeed::custom)::operators)
    if <not <touching [walls v]?>> then
        change [distance to ground v] by (-1)
        change y by (-1)
    end
end
~~~
```

### Add Distance to Pull Out Stack

We also change `pull out if touching…` stack, which looks like this:

```ad-scratch
title: hitbox, pull up definition
~~~scratchblock
define pull out if touching walls and <falling?> or not
if <touching [walls v]> then
set [y speed v] to (0)
change y by <falling?::custom>
end
~~~
```

We will do this in a slightlly different way. If we are touching the wall and falling, then we want to set `Distance to the ground` to zero. One way to do is:

```ad-scratch
~~~scratchblock

  
if <falling?::custom> then
    set [distance to ground v] to (0)
end

~~~
```

One liner [^1]

We put all this in our pull up stack:

```ad-scratch
title: hitbox, pull up definition
~~~scratchblock
define pull out if touching walls and <falling?> or not
if <touching [walls v]> then
set [y speed v] to (0)
change y by <falling?::custom>
if <falling?::custom> then
    set [distance to ground v] to (0)
end
end
~~~
```

One line version is here.[^2]

### Change Jump Routine

Finally, now we can change the jump routine so that we only jump when we are close to the ground.

First, to make sure we are only jumping at the right time, let's change from a `when up arrow pressed` to `receive jump`. Delete __this entire stack__:

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
if <<key [up arrow v] pressed?> and <(distance to ground) \< [5]>> then
    change [y speed v] by (20)
end
broadcast [move left / right v]
~~~
```

This changes the speed by 20 only if we are close to the ground.

Don't forget to change the `broadcast` at the bottom of fall like this:

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

- Right now we fall in steps, but our jump routine makes a big step up when we jump. We are going to jump in steps as well, so that we can detect platforms. 

So, how do we do that? We keep track of whether we are falling by making a new variable to keep track of the sign:

```ad-scratch
title: 
~~~scratchblock
set [sign of y speed v] to (<(y speed) \> [0]> - <(y speed) \< [0]>)
~~~
```

This will be __1__ if we are jumping and __-1__ if we are falling. Then we put this is in the change y by stack, and change __-1__ to `sign of y speed`. 

```ad-scratch
title: hitbox, define change y by (yspeed)
~~~scratchblock
define change y by (yspeed) by single steps
set [sign of y speed v] to (<(y speed) \> [0]> - <(y speed) \< [0]>)
repeat ([abs v] of (yspeed::custom)::operators)
    if <not <touching [walls v]?>> then
        instead of -1, we use sign of y speed
        change [distance to ground v] by (sign of y speed)
        change y by (sign of y speed)
    end
end
~~~
```

That should work. You might have to change the numbers in the __jump stack__ for the `change y speed` and `distance to ground` block to make it work. Things like the size of your hitbox and what your platform looks like can make a difference.

## Climbing Walls

If you make a slope in your wall, you will find that you pass right through it. We haven't taught the x direction to recognize walls yes.

Here's what we do if we find ourselves in a wall. 
1) Try 3 times to go up and get out. 
	1) If we fail, go back and undo the step that got us there.
	2) If we succeed, stay.  
<style>
.container {font-family: sans-serif; text-align: center;}
.button-wrapper button {z-index: 1;height: 40px; width: 100px; margin: 10px;padding: 5px;}
.excalidraw .App-menu_top .buttonList { display: flex;}
.excalidraw-wrapper { height: 800px; margin: 50px; position: relative;}
:root[dir="ltr"] .excalidraw .layer-ui__wrapper .zen-mode-transition.App-menu_bottom--transition-left {transform: none;}
</style><script src="https://unpkg.com/react@17/umd/react.production.min.js"></script><script src="https://unpkg.com/react-dom@17/umd/react-dom.production.min.js"></script><script type="text/javascript" src="https://unpkg.com/@excalidraw/excalidraw@0.12.0/dist/excalidraw.production.min.js"></script><div id="HatlinkClimbexcalidraw.md1"></div><script>(function(){const InitialData={"type":"excalidraw","version":2,"source":"https://excalidraw.com","elements":[{"type":"rectangle","version":787,"versionNonce":586883061,"isDeleted":false,"id":"HITczZ2WnSgBNgqwybQtk","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-671.0252912584959,"y":-92.1737170669998,"strokeColor":"#000000","backgroundColor":"#15aabf","width":580.8837890625,"height":391.697998046875,"seed":1137687143,"groupIds":[],"strokeSharpness":"sharp","boundElements":[],"updated":1669914326974,"link":null,"locked":false},{"type":"rectangle","version":754,"versionNonce":98808839,"isDeleted":false,"id":"QwlCzrxJb6gmmsNx83g1N","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":5.4980536612531115,"x":-624.7237390742927,"y":52.424326195082145,"strokeColor":"#000000","backgroundColor":"#fa5252","width":110.97502255032714,"height":70.5779453048153,"seed":3881479,"groupIds":[],"strokeSharpness":"sharp","boundElements":[{"id":"77_3WgWoV124rznVtUSWu","type":"arrow"}],"updated":1669398503577,"link":null,"locked":false},{"type":"rectangle","version":637,"versionNonce":40285161,"isDeleted":false,"id":"0O1qXktXwk04dqnjbqOwC","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-672.1895121259449,"y":102.46848821189565,"strokeColor":"#000000","backgroundColor":"#fa5252","width":141.7652202405428,"height":52.170654296875,"seed":1844233097,"groupIds":[],"strokeSharpness":"round","boundElements":[{"id":"77_3WgWoV124rznVtUSWu","type":"arrow"}],"updated":1669398503577,"link":null,"locked":false},{"type":"rectangle","version":795,"versionNonce":1132305191,"isDeleted":false,"id":"1Q6kG176Q1p-Fz0YFNiRr","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-616.2092453850149,"y":49.412257032350496,"strokeColor":"#000000","backgroundColor":"#4c6ef5","width":57.265625,"height":54.74920654296875,"seed":1188681095,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1669398503577,"link":null,"locked":false},{"type":"rectangle","version":769,"versionNonce":1897549513,"isDeleted":false,"id":"GKs6z3LqMjc2hPk32BCSL","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":5.4980536612531115,"x":-468.8632966959966,"y":-19.69742159987547,"strokeColor":"#000000","backgroundColor":"#fa5252","width":110.86530381551387,"height":70.57794530481532,"seed":970127975,"groupIds":[],"strokeSharpness":"sharp","boundElements":[{"id":"kFVRM3-_zUgiCwV_k7KD7","type":"arrow"}],"updated":1669398503577,"link":null,"locked":false},{"type":"rectangle","version":907,"versionNonce":2139987527,"isDeleted":false,"id":"C0iNKnFlVGz8IhriqdCVF","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-494.4249171206827,"y":31.3441089601976,"strokeColor":"#000000","backgroundColor":"#fa5252","width":141.7652202405428,"height":52.170654296875,"seed":1341642345,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1669398503577,"link":null,"locked":false},{"type":"text","version":577,"versionNonce":1079479721,"isDeleted":false,"id":"0Dkahe6U","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-465.7727243523846,"y":37.87620060287857,"strokeColor":"#000000","backgroundColor":"transparent","width":86,"height":38,"seed":1025743337,"groupIds":[],"strokeSharpness":"sharp","boundElements":[{"id":"kFVRM3-_zUgiCwV_k7KD7","type":"arrow"}],"updated":1669398503577,"link":null,"locked":false,"fontSize":15.08601053930055,"fontFamily":1,"text":"try 3 times\nto get out","rawText":"try 3 times\nto get out","baseline":32,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"try 3 times\nto get out"},{"type":"freedraw","version":41,"versionNonce":1022377319,"isDeleted":false,"id":"1Lay8SOcx7QnOL7OHQfLE","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-697.5963905736019,"y":190.70445409794428,"strokeColor":"#000000","backgroundColor":"transparent","width":0.21416915090458133,"height":0.10710063733552033,"seed":1108635273,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1669398503577,"link":null,"locked":false,"points":[[0,0],[0,-0.10710063733552033],[-0.10710063733540665,-0.10710063733552033],[-0.21416915090458133,-0.10710063733552033],[0,0]],"lastCommittedPoint":null,"simulatePressure":true,"pressures":[]},{"type":"rectangle","version":1168,"versionNonce":2001334409,"isDeleted":false,"id":"hUN9Mqir3nDZ_A2RDwsqh","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":5.697900419059218,"x":-452.6714532579249,"y":184.34520628119435,"strokeColor":"#000000","backgroundColor":"#fa5252","width":110.86530381551387,"height":70.57794530481532,"seed":1138638375,"groupIds":[],"strokeSharpness":"sharp","boundElements":[],"updated":1669398503577,"link":null,"locked":false},{"type":"rectangle","version":1113,"versionNonce":1861351559,"isDeleted":false,"id":"6-qeHxUvLhYDa0SEwOFuf","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-461.31599189141707,"y":108.53728237435794,"strokeColor":"#000000","backgroundColor":"#4c6ef5","width":57.265625,"height":54.74920654296875,"seed":516512713,"groupIds":[],"strokeSharpness":"round","boundElements":[{"id":"ca0Kxu526HZvwVmwJaIzP","type":"arrow"}],"updated":1669398503577,"link":null,"locked":false},{"type":"arrow","version":1030,"versionNonce":679719221,"isDeleted":false,"id":"ca0Kxu526HZvwVmwJaIzP","fillStyle":"hachure","strokeWidth":4,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-402.6801487457954,"y":184.19445131788876,"strokeColor":"#5c940d","backgroundColor":"transparent","width":25.75433028371708,"height":19.0004368832237,"seed":62231605,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1669914510249,"link":null,"locked":false,"startBinding":null,"endBinding":{"elementId":"6-qeHxUvLhYDa0SEwOFuf","focus":0.5739536814039634,"gap":1.907525517338371},"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[23.845150596217138,-11.151492470189112],[-1.9091796874999432,-19.0004368832237]]},{"type":"rectangle","version":1028,"versionNonce":1800359847,"isDeleted":false,"id":"X3alj4MXodew3LxFIn2U1","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-494.0749733536636,"y":221.1217928651161,"strokeColor":"#000000","backgroundColor":"#fa5252","width":141.7652202405428,"height":52.170654296875,"seed":1587346089,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1669398503577,"link":null,"locked":false},{"type":"text","version":699,"versionNonce":801907273,"isDeleted":false,"id":"DODmyuJJ","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-465.3156799480299,"y":227.6538845077971,"strokeColor":"#000000","backgroundColor":"transparent","width":86,"height":38,"seed":566501479,"groupIds":[],"strokeSharpness":"sharp","boundElements":[{"id":"DUumFiWLmBjLGs_EetedM","type":"arrow"}],"updated":1669398503577,"link":null,"locked":false,"fontSize":15.08601053930055,"fontFamily":1,"text":"try 3 times\nto get out","rawText":"try 3 times\nto get out","baseline":32,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"try 3 times\nto get out"},{"type":"arrow","version":1281,"versionNonce":1471342747,"isDeleted":false,"id":"DUumFiWLmBjLGs_EetedM","fillStyle":"hachure","strokeWidth":4,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-402.6507533469219,"y":219.73560461617367,"strokeColor":"#5c940d","backgroundColor":"transparent","width":25.75433028371708,"height":19.573267886513236,"seed":1623147925,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1669914510249,"link":null,"locked":false,"startBinding":{"elementId":"DODmyuJJ","focus":-0.4486446753327983,"gap":7.918279891623428},"endBinding":null,"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[24.83089959353032,-11.724323473478648],[-0.9234306901867626,-19.573267886513236]]},{"type":"arrow","version":1030,"versionNonce":1606533781,"isDeleted":false,"id":"Xw8N_1OUhSri1r5ND0nMp","fillStyle":"hachure","strokeWidth":4,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-402.6538557622553,"y":201.80297246723794,"strokeColor":"#5c940d","backgroundColor":"transparent","width":23.845150596217138,"height":17.512576434273342,"seed":1212926709,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1669914510249,"link":null,"locked":false,"startBinding":null,"endBinding":null,"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[23.845150596217138,-11.151492470189112],[1.555677305452548,-17.512576434273342]]},{"type":"rectangle","version":1262,"versionNonce":1916719591,"isDeleted":false,"id":"Cs-BTQ3pG6YJ6XuU_pqCK","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":5.697900419059218,"x":-254.46277467670393,"y":189.37326942618475,"strokeColor":"#000000","backgroundColor":"#fa5252","width":110.86530381551387,"height":70.57794530481532,"seed":691888905,"groupIds":[],"strokeSharpness":"sharp","boundElements":[],"updated":1669398503577,"link":null,"locked":false},{"type":"rectangle","version":1219,"versionNonce":1933370377,"isDeleted":false,"id":"NoZg0bqhLaX6phTdAEFvq","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-262.89311203552506,"y":133.45824488201274,"strokeColor":"#000000","backgroundColor":"#4c6ef5","width":57.265625,"height":54.74920654296875,"seed":503639559,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1669398503577,"link":null,"locked":false},{"type":"rectangle","version":1126,"versionNonce":1936896775,"isDeleted":false,"id":"uHziZka7EVr3PdR_8IFpk","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-295.6463042741318,"y":226.14985601010656,"strokeColor":"#000000","backgroundColor":"#fa5252","width":141.7652202405428,"height":52.170654296875,"seed":2003277095,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1669398522075,"link":null,"locked":false},{"type":"text","version":1285,"versionNonce":603290345,"isDeleted":false,"id":"D17GKRMs","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-665.249087337749,"y":-20.962651781642563,"strokeColor":"#000000","backgroundColor":"transparent","width":129,"height":38,"seed":739071079,"groupIds":[],"strokeSharpness":"sharp","boundElements":[{"id":"DUumFiWLmBjLGs_EetedM","type":"arrow"}],"updated":1669398503577,"link":null,"locked":false,"fontSize":15.08601053930055,"fontFamily":1,"text":"Oops, we stepped\ninto the slope!","rawText":"Oops, we stepped\ninto the slope!","baseline":32,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"Oops, we stepped\ninto the slope!"},{"type":"rectangle","version":950,"versionNonce":1549976615,"isDeleted":false,"id":"TjHHvGDF3puKSutmdm99r","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":5.4980536612531115,"x":-248.7945950870605,"y":-24.304925587870244,"strokeColor":"#000000","backgroundColor":"#fa5252","width":114.5488716286079,"height":72.92294088676715,"seed":1573399719,"groupIds":[],"strokeSharpness":"sharp","boundElements":[{"id":"eB4dWzTwXrh_9401X3NUZ","type":"arrow"}],"updated":1669398503577,"link":null,"locked":false},{"type":"rectangle","version":1136,"versionNonce":73858857,"isDeleted":false,"id":"JhdIrqCZPfOAC4rH36ShT","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-297.41047124505013,"y":27.0319455814657,"strokeColor":"#000000","backgroundColor":"#fa5252","width":182.39276566615874,"height":57.377672204712006,"seed":1671140681,"groupIds":[],"strokeSharpness":"round","boundElements":[{"id":"eB4dWzTwXrh_9401X3NUZ","type":"arrow"}],"updated":1669398508389,"link":null,"locked":false},{"type":"rectangle","version":1209,"versionNonce":1944430407,"isDeleted":false,"id":"UyITH7jDsGrlI4cW_mVtW","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-314.8880936062184,"y":-27.7950675147503,"strokeColor":"#000000","backgroundColor":"#4c6ef5","width":59.168310563354716,"height":56.56828255749635,"seed":1703542727,"groupIds":[],"strokeSharpness":"round","boundElements":[{"id":"eB4dWzTwXrh_9401X3NUZ","type":"arrow"}],"updated":1669398503577,"link":null,"locked":false},{"type":"rectangle","version":1260,"versionNonce":2097336763,"isDeleted":false,"id":"_QZdLO2RrvqGKoTSyDMpT","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-465.1768927323195,"y":-76.94890315688733,"strokeColor":"#000000","backgroundColor":"#4c6ef5","width":57.265625,"height":54.74920654296875,"seed":349887753,"groupIds":[],"strokeSharpness":"round","boundElements":[{"id":"ca0Kxu526HZvwVmwJaIzP","type":"arrow"}],"updated":1669914548712,"link":null,"locked":false},{"type":"arrow","version":1342,"versionNonce":1391986197,"isDeleted":false,"id":"uAr-oTCL8XF69DZW1W7tG","fillStyle":"hachure","strokeWidth":4,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-407.41646001823017,"y":-4.915459792005514,"strokeColor":"#5c940d","backgroundColor":"transparent","width":24.49311660025944,"height":19.632233691110912,"seed":182494293,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1669914548712,"link":null,"locked":false,"startBinding":null,"endBinding":null,"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[23.845150596217138,-11.151492470189112],[-0.6479660040423028,-19.632233691110912]]},{"type":"arrow","version":1526,"versionNonce":469149685,"isDeleted":false,"id":"kFVRM3-_zUgiCwV_k7KD7","fillStyle":"hachure","strokeWidth":4,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-407.29858108141025,"y":30.891039488422265,"strokeColor":"#5c940d","backgroundColor":"transparent","width":25.75433028371708,"height":19.573267886513236,"seed":1280528821,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1669914510249,"link":null,"locked":false,"startBinding":{"elementId":"0Dkahe6U","focus":-0.4752488793729658,"gap":6.985161114456304},"endBinding":null,"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[24.83089959353032,-11.724323473478648],[-0.9234306901867626,-19.573267886513236]]},{"type":"arrow","version":1272,"versionNonce":1109376475,"isDeleted":false,"id":"D9VsZblOLojJvzMHwcir6","fillStyle":"hachure","strokeWidth":4,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-407.28306639735456,"y":12.693061357343694,"strokeColor":"#5c940d","backgroundColor":"transparent","width":23.845150596217138,"height":17.512576434273342,"seed":432624405,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1669914510249,"link":null,"locked":false,"startBinding":null,"endBinding":null,"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[23.845150596217138,-11.151492470189112],[1.555677305452548,-17.512576434273342]]},{"type":"text","version":1021,"versionNonce":941637225,"isDeleted":false,"id":"EB4lLJcT","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-551.9714572707868,"y":57.84916289805699,"strokeColor":"#000000","backgroundColor":"transparent","width":38,"height":19,"seed":452264457,"groupIds":[],"strokeSharpness":"sharp","boundElements":[{"id":"DUumFiWLmBjLGs_EetedM","type":"arrow"}],"updated":1669398503577,"link":null,"locked":false,"fontSize":15.08601053930055,"fontFamily":1,"text":"slope","rawText":"slope","baseline":13,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"slope"},{"type":"arrow","version":2168,"versionNonce":1059578197,"isDeleted":false,"id":"eB4dWzTwXrh_9401X3NUZ","fillStyle":"hachure","strokeWidth":4,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-190.4080801899841,"y":-31.631287512562523,"strokeColor":"#5c940d","backgroundColor":"transparent","width":70.44470087085082,"height":53.11504594275629,"seed":1069033589,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1669914510249,"link":null,"locked":false,"startBinding":null,"endBinding":{"elementId":"Pn3tp5qQ","focus":-1.4068369883947134,"gap":10.31643816185057},"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[6.859782719732119,28.516532041266895],[-63.5849181511187,53.11504594275629]]},{"type":"text","version":1125,"versionNonce":1268128231,"isDeleted":false,"id":"SGhpAOig","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-242.60614230724366,"y":238.46981893884654,"strokeColor":"#000000","backgroundColor":"transparent","width":48,"height":25,"seed":152515753,"groupIds":[],"strokeSharpness":"sharp","boundElements":[{"id":"DUumFiWLmBjLGs_EetedM","type":"arrow"}],"updated":1669398526606,"link":null,"locked":false,"fontSize":19.831954588097943,"fontFamily":1,"text":"Stay","rawText":"Stay","baseline":17,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"Stay"},{"type":"text","version":1265,"versionNonce":1405111239,"isDeleted":false,"id":"ybxu1UgZ","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-357.2880261609201,"y":-64.42743977026785,"strokeColor":"#000000","backgroundColor":"transparent","width":52,"height":23,"seed":1430392999,"groupIds":[],"strokeSharpness":"sharp","boundElements":[{"id":"DUumFiWLmBjLGs_EetedM","type":"arrow"}],"updated":1669398503577,"link":null,"locked":false,"fontSize":18.634518511062545,"fontFamily":1,"text":"FAIL!","rawText":"FAIL!","baseline":16,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"FAIL!"},{"type":"text","version":1371,"versionNonce":3322727,"isDeleted":false,"id":"Pn3tp5qQ","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-252.29303906356563,"y":31.800196592044337,"strokeColor":"#000000","backgroundColor":"transparent","width":82,"height":25,"seed":1140146825,"groupIds":[],"strokeSharpness":"sharp","boundElements":[{"id":"DUumFiWLmBjLGs_EetedM","type":"arrow"},{"id":"eB4dWzTwXrh_9401X3NUZ","type":"arrow"}],"updated":1669398512900,"link":null,"locked":false,"fontSize":19.994068729120446,"fontFamily":1,"text":"Go back","rawText":"Go back","baseline":18,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"Go back"},{"type":"arrow","version":1662,"versionNonce":281102971,"isDeleted":false,"id":"77_3WgWoV124rznVtUSWu","fillStyle":"hachure","strokeWidth":4,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-650.7975333939639,"y":102.60835988898037,"strokeColor":"#5c940d","backgroundColor":"transparent","width":37.217743626219544,"height":21.204761705900523,"seed":1608864213,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1669914510249,"link":null,"locked":false,"startBinding":{"elementId":"QwlCzrxJb6gmmsNx83g1N","focus":-1.3228029876831593,"gap":12.730000914015818},"endBinding":{"elementId":"0O1qXktXwk04dqnjbqOwC","focus":0.13607954566585798,"gap":1},"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[17.883786556421,-21.204761705900523],[37.217743626219544,-0.7703504060444857]]},{"type":"text","version":1360,"versionNonce":1434553097,"isDeleted":false,"id":"UAA9IS5w","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-392.3520692059641,"y":112.94017992521594,"strokeColor":"#000000","backgroundColor":"transparent","width":120,"height":31,"seed":1877338119,"groupIds":[],"strokeSharpness":"sharp","boundElements":[{"id":"DUumFiWLmBjLGs_EetedM","type":"arrow"}],"updated":1669398503577,"link":null,"locked":false,"fontSize":24.713242332584898,"fontFamily":1,"text":"SUCCESS!","rawText":"SUCCESS!","baseline":22,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"SUCCESS!"},{"type":"text","version":1422,"versionNonce":1028449991,"isDeleted":false,"id":"klQLOv3C","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-282.84690554926544,"y":55.155297302419875,"strokeColor":"#000000","backgroundColor":"transparent","width":155,"height":25,"seed":600807465,"groupIds":[],"strokeSharpness":"sharp","boundElements":[{"id":"DUumFiWLmBjLGs_EetedM","type":"arrow"},{"id":"eB4dWzTwXrh_9401X3NUZ","type":"arrow"}],"updated":1669398511033,"link":null,"locked":false,"fontSize":19.994068729120446,"fontFamily":1,"text":"set speed to 0","rawText":"set speed to 0","baseline":18,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"set speed to 0"}],"appState":{"theme":"dark","viewBackgroundColor":"transparent","currentItemStrokeColor":"#5c940d","currentItemBackgroundColor":"transparent","currentItemFillStyle":"solid","currentItemStrokeWidth":4,"currentItemStrokeStyle":"solid","currentItemRoughness":0,"currentItemOpacity":100,"currentItemFontFamily":1,"currentItemFontSize":20,"currentItemTextAlign":"left","currentItemStrokeSharpness":"sharp","currentItemStartArrowhead":null,"currentItemEndArrowhead":"arrow","currentItemLinearStrokeSharpness":"round","gridSize":null,"colorPalette":{}},"files":{}};InitialData.scrollToContent=true;App=()=>{const e=React.useRef(null),t=React.useRef(null),[n,i]=React.useState({width:void 0,height:void 0});return React.useEffect(()=>{i({width:t.current.getBoundingClientRect().width,height:t.current.getBoundingClientRect().height});const e=()=>{i({width:t.current.getBoundingClientRect().width,height:t.current.getBoundingClientRect().height})};return window.addEventListener("resize",e),()=>window.removeEventListener("resize",e)},[t]),React.createElement(React.Fragment,null,React.createElement("div",{className:"excalidraw-wrapper",ref:t},React.createElement(ExcalidrawLib.Excalidraw,{ref:e,width:n.width,height:n.height,initialData:InitialData,viewModeEnabled:!0,zenModeEnabled:!0,gridModeEnabled:!1})))},excalidrawWrapper=document.getElementById("HatlinkClimbexcalidraw.md1");ReactDOM.render(React.createElement(App),excalidrawWrapper);})();</script>

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

Test it out by putting a slanted wall in your project and watch the player climb up it.

### Wrapping

When we hit the edge of the screen, we want to wrap around to the other side. 

The basic routing is if we hit an edge, we will 
1) move the character to a new position
2) change the screen number to the new screen
3) tell the walls to change to the new screen
4) stop what we were doing. We don't need to keep moving or falling or jumping, because we are on a new screen.
5) wait one second for all the other sprites (the wall, the lava) to catch up. 

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

At this point, there is one problem. If the two screens don't match up, which can easily happen, we might end up inside a wall when we switch screen. So, we will fix the collision. 

We fix it lie this:  
We turn going up and move 1 pixel.  
If we are out, good.  
If not, we turn the opposite way and go down 2 pixels.  
If we are out, good.  
If not, we turn back going up, and move 3 pixels, and so on, until we are finally out.

Here's a picture:

<div id="Torchlight_Platformer_Part_2_Fix_Collisionexcalidraw.md2"></div><script>(function(){const InitialData={"type":"excalidraw","version":2,"source":"https://excalidraw.com","elements":[{"type":"rectangle","version":1230,"versionNonce":1326460981,"isDeleted":false,"id":"6r8oZzXxjRGtEO5IhP07N","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":4.71238898038469,"x":-127.54069433901702,"y":-489.13844442206175,"strokeColor":"#000000","backgroundColor":"#fa5252","width":295.5058418434516,"height":72.92294088676715,"seed":1349433452,"groupIds":[],"strokeSharpness":"sharp","boundElements":[{"id":"DZRCKaeJC-TAsPsNJaCOc","type":"arrow"}],"updated":1669918440150,"link":null,"locked":false},{"type":"rectangle","version":1767,"versionNonce":415098939,"isDeleted":false,"id":"im284DNI8V8JLk6yWFcMu","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":4.712269451431062,"y":-611.9504128138345,"strokeColor":"#000000","backgroundColor":"#4c6ef5","width":59.168310563354716,"height":56.56828255749635,"seed":1028150356,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1669918484010,"link":null,"locked":false},{"type":"rectangle","version":1163,"versionNonce":1926925787,"isDeleted":false,"id":"qEV3Hn21T2npdRiWS8leo","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":4.71238898038469,"x":-321.9224844644991,"y":-483.8028908060695,"strokeColor":"#000000","backgroundColor":"#fa5252","width":295.5058418434516,"height":72.92294088676715,"seed":1041328084,"groupIds":[],"strokeSharpness":"sharp","boundElements":[],"updated":1669918218367,"link":null,"locked":false},{"type":"rectangle","version":433,"versionNonce":382538651,"isDeleted":false,"id":"0UPvBxTQyQ9KOCtsEDP53","fillStyle":"solid","strokeWidth":2,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-13.610716316723,"y":-602.9928376573877,"strokeColor":"#000000","backgroundColor":"#228be6","width":130.69785563151044,"height":22.71038818359381,"seed":1063623355,"groupIds":[],"strokeSharpness":"round","boundElements":[{"id":"DZRCKaeJC-TAsPsNJaCOc","type":"arrow"}],"updated":1669918479152,"link":null,"locked":false},{"type":"rectangle","version":1512,"versionNonce":1471711547,"isDeleted":false,"id":"SuwEYpyxtkfh-wQKAHC1n","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-174.26969989347313,"y":-555.354458804843,"strokeColor":"#000000","backgroundColor":"#4c6ef5","width":59.168310563354716,"height":56.56828255749635,"seed":1757236564,"groupIds":[],"strokeSharpness":"round","boundElements":[{"id":"XgcU1G7NP16CRhX4da5QD","type":"arrow"},{"id":"QJb82Mopw7i7D3H6u-m3K","type":"arrow"}],"updated":1669918291066,"link":null,"locked":false},{"type":"rectangle","version":2063,"versionNonce":27400827,"isDeleted":false,"id":"IL4SI3rKAcOw9VT3l6fLs","fillStyle":"solid","strokeWidth":0.5,"strokeStyle":"dotted","roughness":1,"opacity":100,"angle":0,"x":-174.2696998934731,"y":-611.9504128138345,"strokeColor":"#000000","backgroundColor":"#228be6","width":59.168310563354716,"height":56.56828255749635,"seed":894585708,"groupIds":[],"strokeSharpness":"round","boundElements":[{"id":"DZRCKaeJC-TAsPsNJaCOc","type":"arrow"}],"updated":1669918218367,"link":null,"locked":false},{"type":"text","version":2000,"versionNonce":66606683,"isDeleted":false,"id":"HXi8s5xC","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-102.58379864168569,"y":-617.0516973614006,"strokeColor":"#000000","backgroundColor":"transparent","width":39,"height":25,"seed":1213272812,"groupIds":[],"strokeSharpness":"sharp","boundElements":[],"updated":1669918529295,"link":null,"locked":false,"fontSize":19.994068729120446,"fontFamily":1,"text":"up 1","rawText":"up 1","baseline":18,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"up 1"},{"type":"rectangle","version":1859,"versionNonce":764671931,"isDeleted":false,"id":"RlFbv5HtP0x_Jhjq3Hamp","fillStyle":"solid","strokeWidth":0.5,"strokeStyle":"dotted","roughness":1,"opacity":100,"angle":0,"x":4.618460265825,"y":-491.25202022392745,"strokeColor":"#000000","backgroundColor":"#228be6","width":59.168310563354716,"height":56.56828255749635,"seed":99134444,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1669918218367,"link":null,"locked":false},{"type":"text","version":2151,"versionNonce":529839477,"isDeleted":false,"id":"zdJGNLOX","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":69.1738660568146,"y":-487.8799467073629,"strokeColor":"#000000","backgroundColor":"transparent","width":70,"height":25,"seed":727886292,"groupIds":[],"strokeSharpness":"sharp","boundElements":[{"id":"DZRCKaeJC-TAsPsNJaCOc","type":"arrow"}],"updated":1669918218367,"link":null,"locked":false,"fontSize":19.994068729120446,"fontFamily":1,"text":"down 2","rawText":"down 2","baseline":18,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"down 2"},{"type":"rectangle","version":1395,"versionNonce":1498630235,"isDeleted":false,"id":"vo9_iJh1XJ_evuXyATswG","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":4.71238898038469,"x":75.30159266678322,"y":-477.9910343471921,"strokeColor":"#000000","backgroundColor":"#fa5252","width":295.5058418434516,"height":72.92294088676715,"seed":477319532,"groupIds":[],"strokeSharpness":"sharp","boundElements":[{"id":"FnxsHGiPfhYKi4EBRkgQx","type":"arrow"}],"updated":1669918218367,"link":null,"locked":false},{"type":"rectangle","version":2044,"versionNonce":883984955,"isDeleted":false,"id":"Ia-tx3iVtldCVr_36TtQV","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":205.8726552451195,"y":-491.54682002861495,"strokeColor":"#000000","backgroundColor":"#4c6ef5","width":59.168310563354716,"height":56.56828255749635,"seed":1440459372,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1669918616051,"link":null,"locked":false},{"type":"text","version":2418,"versionNonce":1606335317,"isDeleted":false,"id":"DWGMYdn3","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":275.58097081322364,"y":-626.8990793792973,"strokeColor":"#000000","backgroundColor":"transparent","width":47,"height":25,"seed":1967580780,"groupIds":[],"strokeSharpness":"sharp","boundElements":[{"id":"FnxsHGiPfhYKi4EBRkgQx","type":"arrow"}],"updated":1669918536080,"link":null,"locked":false,"fontSize":19.994068729120446,"fontFamily":1,"text":"up 3","rawText":"up 3","baseline":18,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"up 3"},{"type":"rectangle","version":2194,"versionNonce":1497603125,"isDeleted":false,"id":"PrYNPL7FfObYSUA_DZuGw","fillStyle":"solid","strokeWidth":0.5,"strokeStyle":"dotted","roughness":1,"opacity":100,"angle":0,"x":205.8726552451195,"y":-648.5627136600156,"strokeColor":"#000000","backgroundColor":"#228be6","width":59.168310563354716,"height":56.56828255749635,"seed":1047236204,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1669918218367,"link":null,"locked":false},{"type":"text","version":2410,"versionNonce":58404251,"isDeleted":false,"id":"jEX4oxLK","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":276.88045263989227,"y":-653.8376485996455,"strokeColor":"#000000","backgroundColor":"transparent","width":109,"height":25,"seed":126818900,"groupIds":[],"strokeSharpness":"sharp","boundElements":[{"id":"FnxsHGiPfhYKi4EBRkgQx","type":"arrow"}],"updated":1669918218367,"link":null,"locked":false,"fontSize":19.994068729120446,"fontFamily":1,"text":"We're free!","rawText":"We're free!","baseline":18,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"We're free!"},{"type":"text","version":2611,"versionNonce":1696031541,"isDeleted":false,"id":"m865Cgdt","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-128.94226348268998,"y":-639.463508904705,"strokeColor":"#000000","backgroundColor":"transparent","width":90,"height":25,"seed":1593345900,"groupIds":[],"strokeSharpness":"sharp","boundElements":[{"id":"FnxsHGiPfhYKi4EBRkgQx","type":"arrow"}],"updated":1669918363748,"link":null,"locked":false,"fontSize":19.994068729120446,"fontFamily":1,"text":"Touching!","rawText":"Touching!","baseline":18,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"Touching!"},{"type":"text","version":2797,"versionNonce":1804456309,"isDeleted":false,"id":"0dZrvjSG","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":64.36221607502455,"y":-467.4472170097506,"strokeColor":"#000000","backgroundColor":"transparent","width":90,"height":25,"seed":162935636,"groupIds":[],"strokeSharpness":"sharp","boundElements":[{"id":"FnxsHGiPfhYKi4EBRkgQx","type":"arrow"}],"updated":1669918526561,"link":null,"locked":false,"fontSize":19.994068729120446,"fontFamily":1,"text":"Touching!","rawText":"Touching!","baseline":18,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"Touching!"},{"type":"arrow","version":2034,"versionNonce":1745712245,"isDeleted":false,"id":"OxjlI-cr2r7d8a6bOusgQ","fillStyle":"hachure","strokeWidth":2,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":35.36607633518362,"y":-583.8587360209059,"strokeColor":"#000000","backgroundColor":"#228be6","width":0,"height":36.57410757882246,"seed":33109941,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1669918463287,"link":null,"locked":false,"startBinding":{"elementId":"hALv1Oe2","focus":0.32196741948446,"gap":1.9575781248267958},"endBinding":null,"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"triangle","points":[[0,0],[0,36.57410757882246]]},{"type":"text","version":3694,"versionNonce":55355675,"isDeleted":false,"id":"hALv1Oe2","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-4.6378459152332425,"y":-599.8163141457327,"strokeColor":"#000000","backgroundColor":"transparent","width":118,"height":14,"seed":522127899,"groupIds":[],"strokeSharpness":"sharp","boundElements":[{"id":"FnxsHGiPfhYKi4EBRkgQx","type":"arrow"},{"id":"XgcU1G7NP16CRhX4da5QD","type":"arrow"},{"id":"OxjlI-cr2r7d8a6bOusgQ","type":"arrow"}],"updated":1669918448935,"link":null,"locked":false,"fontSize":11.282452729288204,"fontFamily":1,"text":"point in direction 180","rawText":"point in direction 180","baseline":10,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"point in direction 180"},{"type":"arrow","version":4100,"versionNonce":540747093,"isDeleted":false,"id":"DZRCKaeJC-TAsPsNJaCOc","fillStyle":"hachure","strokeWidth":4,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":38.38641730164438,"y":-579.2824494737938,"strokeColor":"#5c940d","backgroundColor":"transparent","width":66.94850141131926,"height":114.50569118774433,"seed":1498729196,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1669918432382,"link":null,"locked":false,"startBinding":{"elementId":"0UPvBxTQyQ9KOCtsEDP53","focus":0.3436910526935273,"gap":1},"endBinding":null,"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[58.98078712590863,54.735771964251626],[-7.967714285410629,114.50569118774433]]},{"type":"rectangle","version":643,"versionNonce":241190011,"isDeleted":false,"id":"3g_9kWtlQErJcA-lrebuf","fillStyle":"solid","strokeWidth":2,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":186.0675321011192,"y":-475.07598022283025,"strokeColor":"#000000","backgroundColor":"#228be6","width":116.28605143229159,"height":23.420572916666625,"seed":1131303643,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1669918220166,"link":null,"locked":false},{"type":"arrow","version":3960,"versionNonce":413582875,"isDeleted":false,"id":"FnxsHGiPfhYKi4EBRkgQx","fillStyle":"hachure","strokeWidth":4,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":268.46622990286346,"y":-482.7653446926095,"strokeColor":"#5c940d","backgroundColor":"transparent","width":58.3925902970268,"height":137.4759071179007,"seed":1401503956,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1669918232635,"link":null,"locked":false,"startBinding":{"elementId":"yrEaZrPp","focus":0.27992841772910565,"gap":12.485588428112408},"endBinding":null,"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[22.68107793095149,-57.68559917435465],[-35.71151236607531,-137.4759071179007]]},{"type":"text","version":3825,"versionNonce":501127675,"isDeleted":false,"id":"yrEaZrPp","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":188.35836462065018,"y":-470.2797562644971,"strokeColor":"#000000","backgroundColor":"transparent","width":112,"height":14,"seed":1968575803,"groupIds":[],"strokeSharpness":"sharp","boundElements":[{"id":"FnxsHGiPfhYKi4EBRkgQx","type":"arrow"},{"id":"XgcU1G7NP16CRhX4da5QD","type":"arrow"},{"id":"OxjlI-cr2r7d8a6bOusgQ","type":"arrow"},{"id":"DZRCKaeJC-TAsPsNJaCOc","type":"arrow"},{"id":"C72Om_XO2M3xszHKiHbAJ","type":"arrow"}],"updated":1669918218368,"link":null,"locked":false,"fontSize":11.282452729288204,"fontFamily":1,"text":" point in direction 0","rawText":" point in direction 0","baseline":10,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":" point in direction 0"},{"type":"rectangle","version":820,"versionNonce":1139386843,"isDeleted":false,"id":"6FpWSr7ncMs8iB-UIfEwy","fillStyle":"solid","strokeWidth":2,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-199.74441858247465,"y":-536.1587845848097,"strokeColor":"#000000","backgroundColor":"#228be6","width":116.28605143229159,"height":23.420572916666625,"seed":82195989,"groupIds":[],"strokeSharpness":"round","boundElements":[{"id":"QJb82Mopw7i7D3H6u-m3K","type":"arrow"}],"updated":1669918291066,"link":null,"locked":false},{"type":"text","version":4004,"versionNonce":1297684411,"isDeleted":false,"id":"pvgSQxIm","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-197.45358606294369,"y":-531.3625606264767,"strokeColor":"#000000","backgroundColor":"transparent","width":112,"height":14,"seed":1280287163,"groupIds":[],"strokeSharpness":"sharp","boundElements":[{"id":"FnxsHGiPfhYKi4EBRkgQx","type":"arrow"},{"id":"XgcU1G7NP16CRhX4da5QD","type":"arrow"},{"id":"OxjlI-cr2r7d8a6bOusgQ","type":"arrow"},{"id":"DZRCKaeJC-TAsPsNJaCOc","type":"arrow"},{"id":"C72Om_XO2M3xszHKiHbAJ","type":"arrow"}],"updated":1669918585651,"link":null,"locked":false,"fontSize":11.282452729288204,"fontFamily":1,"text":" point in direction 0","rawText":" point in direction 0","baseline":10,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":" point in direction 0"},{"type":"arrow","version":895,"versionNonce":1928061659,"isDeleted":false,"id":"QJb82Mopw7i7D3H6u-m3K","fillStyle":"hachure","strokeWidth":2,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-146.25173066309156,"y":-528.6547838756392,"strokeColor":"#000000","backgroundColor":"#228be6","width":1.4621233258928044,"height":38.9751408894856,"seed":543097621,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1669918592706,"link":null,"locked":false,"startBinding":null,"endBinding":{"elementId":"SuwEYpyxtkfh-wQKAHC1n","focus":0.053046656422927156,"gap":12.275465960281736},"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"triangle","points":[[0,0],[1.4621233258928044,-38.9751408894856]]},{"type":"arrow","version":4318,"versionNonce":995927637,"isDeleted":false,"id":"XgcU1G7NP16CRhX4da5QD","fillStyle":"hachure","strokeWidth":4,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-140.4805813662682,"y":-527.2837476930234,"strokeColor":"#5c940d","backgroundColor":"transparent","width":52.81868152218121,"height":57.19617554264266,"seed":109568492,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1669918494681,"link":null,"locked":false,"startBinding":null,"endBinding":null,"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[47.26444264915801,-37.06457486979366],[-5.554238873023195,-57.19617554264266]]},{"type":"arrow","version":1366,"versionNonce":337677045,"isDeleted":false,"id":"C72Om_XO2M3xszHKiHbAJ","fillStyle":"hachure","strokeWidth":2,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":233.63413153654392,"y":-469.087170728085,"strokeColor":"#000000","backgroundColor":"#228be6","width":0,"height":50.16330761930152,"seed":796466261,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1669918616051,"link":null,"locked":false,"startBinding":null,"endBinding":null,"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"triangle","points":[[0,0],[0,-50.16330761930152]]}],"appState":{"theme":"dark","viewBackgroundColor":"transparent","currentItemStrokeColor":"#000000","currentItemBackgroundColor":"#228be6","currentItemFillStyle":"solid","currentItemStrokeWidth":2,"currentItemStrokeStyle":"solid","currentItemRoughness":0,"currentItemOpacity":100,"currentItemFontFamily":1,"currentItemFontSize":20,"currentItemTextAlign":"left","currentItemStrokeSharpness":"round","currentItemStartArrowhead":null,"currentItemEndArrowhead":"triangle","currentItemLinearStrokeSharpness":"round","gridSize":null,"colorPalette":{}},"files":{}};InitialData.scrollToContent=true;App=()=>{const e=React.useRef(null),t=React.useRef(null),[n,i]=React.useState({width:void 0,height:void 0});return React.useEffect(()=>{i({width:t.current.getBoundingClientRect().width,height:t.current.getBoundingClientRect().height});const e=()=>{i({width:t.current.getBoundingClientRect().width,height:t.current.getBoundingClientRect().height})};return window.addEventListener("resize",e),()=>window.removeEventListener("resize",e)},[t]),React.createElement(React.Fragment,null,React.createElement("div",{className:"excalidraw-wrapper",ref:t},React.createElement(ExcalidrawLib.Excalidraw,{ref:e,width:n.width,height:n.height,initialData:InitialData,viewModeEnabled:!0,zenModeEnabled:!0,gridModeEnabled:!1})))},excalidrawWrapper=document.getElementById("Torchlight_Platformer_Part_2_Fix_Collisionexcalidraw.md2");ReactDOM.render(React.createElement(App),excalidrawWrapper);})();</script>

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

when I receive [set scene v]  
set x to (-233)  
set [touched lava v] to [0]  
broadcast [move left / right v]

```ad-scratch
title: Walls, switch costume stacks
~~~scratchblock
when gf clicked
switch costume to (screen)

when I receive (new screen v)
switch costume to (screen)


~~~
```

### Make Visual Effects

Torchlight  
Using a gradient


LAYERS

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
change y by (y speed) by single steps::custom  
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

---

## Footnotes

---

[^1]: It runs a little faster if we don't use an `if`, but put it all on one line. We can do this with a change block. If I have 10, and I change it by -10, I get zero. This is true for any number. We multiply `distance to ground` by __-1__ and then multiply by the condition.

    ```ad-scratch
    ~~~scratchblock
    change [distance to ground v] by (((distance to ground) * (-1)) * (<falling?::custom> * <touching [walls v]?>))
    ~~~
    ```

[^2]: Pull out routine with one liners:

    ```ad-scratch
    title: 
    ~~~scratchblock
    define pull up or down if touching walls and <falling?> or not
    change [y speed v] by (<touching [walls v]?> * ((-1) * (y speed)))
    change [distance to ground v] by (((distance to ground) * (-1)) * (<falling?::custom> * <touching [walls v]?>))
    change y by (<touching [walls v]?> * (falling?::custom)
    ~~~
    ```
