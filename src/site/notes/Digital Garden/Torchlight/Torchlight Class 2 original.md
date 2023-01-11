---
{"dg-publish":true,"permalink":"/digital-garden/torchlight/torchlight-class-2-original/"}
---


## Where we left off 中断した場所

This is the second class. The first class is [[Digital Garden/Torchlight/Torchlight Platformer Part 1, First Class\|here]]. 
2番目のクラスです。 ファーストクラスは【トーチライトプラクター パート1、ファーストクラス|こちら】

In the first part we made an **if/else** block in the `set xspeed`. We finished the first condition. It worked like this:
最初の部分では、 `set xspeed` に **if/else** ブロックを作成しました。最初の条件を終えました。次のように機能しました。
```ad-scratch
title: 
~~~scratchblock
define set xspeed
if <no key is pressed> then
We slow down. 減速します. 
else

end
~~~
```
- Slowing down had two parts, left and right.
- 減速には、左右の 2 つの部分がありました。


```ad-scratch
title:
~~~scratchblock
define set xspeed
if <no key pressed キーが押されていません> then
slowing down has two parts. スローダウンには 2 つの部分があります。
if <moving left> then
slow down left 左に減速

      end
if <moving right> then
slow down right 右に減速
      end
else
end
~~~
```
Now we will do the 2nd condition, the **else** part.
次に、2 番目の条件である **else** 部分を実行します。

```ad-scratch
title: 
~~~scratchblock
define set xspeed
if <no key is pressed> then
...
else
We will do this now. 今すぐこれを行います。

end
~~~
```

## Move left and right  左に移動して右に移動
The **else** part is for when the left or right arrow key is pressed. 
**else** の部分は、左右の矢印キーが押されたときのためのものです。
The arrow keys should make us go faster. 矢印キーを使用すると、より速く進むことができます。
Again there are 2 parts. ここでも 2 つの部分があります。


- If we want to go faster to the right, we __add 1__ to `x speed`
- 右に速く移動したい場合は、`x speed` に __1__ を追加します

```ad-scratch
title: Hitbox, set x speed
~~~scratchblock
if <key [right arrow v] pressed> then
	change (x speed) by (1)
end
~~~
```

- If we want to go faster to the left, we __subtract 1__ from `x speed`
- 左に速く移動したい場合は、`x speed` から __減算 1__ します。

```ad-scratch
title: Hitbox, set x speed
~~~scratchblock
if <key [left arrow v] pressed> then
	change (x speed) by (-1)
~~~
```

All together it looks like this:[^1]
まとめると、次のようになります。[^1]

```ad-scratch
title:
~~~scratchblock
define set xspeed
if <<not <key [left arrow v] pressed?>> and <not <key [right arrow v] pressed?>>> then
if <(x speed) < (0)> then
	change (x speed) by (1)
	end
	if <(x speed) > (0)> then
	change (x speed) by (-1)
	end
else
right 
if <key [right arrow v] pressed> then
	change (x speed) by (1)
end
left
if <key [left arrow v] pressed> then
	change (x speed) by (-1)
end
end
~~~
```
## Test run

**Run the project now**. The sprite should move left and right. 
**プロジェクトを今すぐ実行**。 ここでプロジェクトを実行すると、スプライトが左右に移動するはずです。


## Slow the Sprite Down
**Hitbox** moves too fast. Again there are two possibilities, left and right.
**ヒットボックス**の動きが速すぎる。ここでも、左と右の 2 つの可能性があります。
If the maximum speed is 4, then when we move right, the speed is 4, when we move left the speed is -4.
最大速度が 4 の場合、右に移動すると速度は 4 になり、左に移動すると速度は -4 になります。


```ad-scratch
title: hitbox, define keep speed below max
~~~scratchblock
define keep speed below max
set maximum speed
moving right:
if <(x speed) \> [4]> then
    set [x speed v] to [4]
end
moving left:
if <(x speed) \< [-4]> then
    set [x speed v] to [-4]
end
~~~
```


## Falling
## 落下
Next we will teach our guy to fall. 
次に、私たちは男に落ちるように教えます。

### Create a Platform
### プラットフォームを作成する

**Create a platform** (wall) for the character to fall onto.
キャラクターが落ちるための**プラットフォーム** (壁) を作成します。
It should look like this:
次のようになります。

<style>
.container {font-family: sans-serif; text-align: center;}
.button-wrapper button {z-index: 1;height: 40px; width: 100px; margin: 10px;padding: 5px;}
.excalidraw .App-menu_top .buttonList { display: flex;}
.excalidraw-wrapper { height: 800px; margin: 50px; position: relative;}
:root[dir="ltr"] .excalidraw .layer-ui__wrapper .zen-mode-transition.App-menu_bottom--transition-left {transform: none;}
</style><script src="https://unpkg.com/react@17/umd/react.production.min.js"></script><script src="https://unpkg.com/react-dom@17/umd/react-dom.production.min.js"></script><script type="text/javascript" src="https://unpkg.com/@excalidraw/excalidraw@0.12.0/dist/excalidraw.production.min.js"></script><div id="HatlightPlatform.excalidraw.md1"></div><script>(function(){const InitialData={"type":"excalidraw","version":2,"source":"https://excalidraw.com","elements":[{"type":"rectangle","version":147,"versionNonce":2023188251,"isDeleted":false,"id":"-BhE3qjFz7EzdAMw-8k5u","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-198.8213895022215,"y":-231.31190412472455,"strokeColor":"#000000","backgroundColor":"#15aabf","width":580.8837890625,"height":391.697998046875,"seed":2096960897,"groupIds":[],"roundness":null,"boundElements":[],"updated":1669149990766,"link":null,"locked":false},{"type":"rectangle","version":141,"versionNonce":870929379,"isDeleted":false,"id":"K6F48gfgbAf7FfVEZiAFg","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-200.221923828125,"y":52.3824462890625,"strokeColor":"#000000","backgroundColor":"#fa5252","width":578.7227783203125,"height":52.170654296875,"seed":82281487,"groupIds":[],"roundness":{"type":1},"boundElements":[{"id":"9I-onR_TnxsWehH5Y7p2I","type":"arrow"},{"id":"oIGih9U9zFPPHVnpe0U7I","type":"arrow"}],"updated":1669342661397,"link":null,"locked":false},{"type":"rectangle","version":179,"versionNonce":745533753,"isDeleted":false,"id":"n2TPaNDw8CFg9ZS1F-NcI","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-131.50845336914062,"y":-49.205535888671875,"strokeColor":"#000000","backgroundColor":"#4c6ef5","width":57.265625,"height":54.74920654296875,"seed":1020124033,"groupIds":[],"roundness":{"type":1},"boundElements":[{"id":"0nTujerjs8bk4BAkzAtd5","type":"arrow"},{"id":"9I-onR_TnxsWehH5Y7p2I","type":"arrow"}],"updated":1668907730051,"link":null,"locked":false},{"type":"text","version":158,"versionNonce":1486115523,"isDeleted":false,"id":"S13IR9yP","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":37.955902099609375,"y":-46.94099426269531,"strokeColor":"#000000","backgroundColor":"#4c6ef5","width":142,"height":24,"seed":78555537,"groupIds":[],"roundness":{"type":2},"boundElements":[{"id":"oIGih9U9zFPPHVnpe0U7I","type":"arrow"}],"updated":1669342670503,"link":null,"locked":false,"fontSize":20,"fontFamily":3,"text":"New Platform","rawText":"New Platform","baseline":20,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"New Platform"},{"type":"arrow","version":471,"versionNonce":1889731171,"isDeleted":false,"id":"oIGih9U9zFPPHVnpe0U7I","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":114.17423255368223,"y":-19.569026294354188,"strokeColor":"#000000","backgroundColor":"#4c6ef5","width":56.65499939963845,"height":69.81109172404169,"seed":875514001,"groupIds":[],"roundness":{"type":2},"boundElements":[],"updated":1669342670503,"link":null,"locked":false,"startBinding":{"elementId":"S13IR9yP","focus":-0.2115405083438377,"gap":3.3719679683411243},"endBinding":{"elementId":"K6F48gfgbAf7FfVEZiAFg","focus":-0.17559197508991395,"gap":2.140380859375},"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[-56.65499939963845,69.81109172404169]]},{"type":"text","version":315,"versionNonce":1758840217,"isDeleted":false,"id":"nqnPZZR9","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-8.20112205570581,"y":-136.19928121974326,"strokeColor":"#000000","backgroundColor":"#4c6ef5","width":130,"height":24,"seed":430884447,"groupIds":[],"roundness":{"type":2},"boundElements":[{"id":"0nTujerjs8bk4BAkzAtd5","type":"arrow"}],"updated":1673243909372,"link":null,"locked":false,"fontSize":20,"fontFamily":3,"text":"Main Sprite","rawText":"Main Sprite","baseline":20,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"Main Sprite"},{"type":"arrow","version":840,"versionNonce":891005561,"isDeleted":false,"id":"0nTujerjs8bk4BAkzAtd5","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-14.73923481878687,"y":-103.96286750978939,"strokeColor":"#000000","backgroundColor":"#4c6ef5","width":63.52899038169615,"height":52.15573860353939,"seed":503215935,"groupIds":[],"roundness":{"type":2},"boundElements":[],"updated":1673243909373,"link":null,"locked":false,"startBinding":{"elementId":"nqnPZZR9","focus":0.5851118584451094,"gap":10.515960693359375},"endBinding":{"elementId":"n2TPaNDw8CFg9ZS1F-NcI","focus":-0.1920958528217059,"gap":2.601593017578125},"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[-63.52899038169615,52.15573860353939]]},{"type":"arrow","version":204,"versionNonce":579342615,"isDeleted":false,"id":"9I-onR_TnxsWehH5Y7p2I","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-89.84741210937501,"y":13.333648681640629,"strokeColor":"#000000","backgroundColor":"#4c6ef5","width":1.22406005859375,"height":35.57952880859375,"seed":470672351,"groupIds":[],"roundness":{"type":2},"boundElements":[],"updated":1668907730051,"link":null,"locked":false,"startBinding":{"elementId":"n2TPaNDw8CFg9ZS1F-NcI","focus":-0.4814271652162273,"gap":7.78997802734375},"endBinding":{"elementId":"K6F48gfgbAf7FfVEZiAFg","focus":-0.6243659421659179,"gap":3.469268798828125},"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[-1.22406005859375,35.57952880859375]]},{"type":"text","version":53,"versionNonce":915304409,"isDeleted":false,"id":"Wls7tnzk","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-81.95840454101562,"y":16.0592041015625,"strokeColor":"#000000","backgroundColor":"#4c6ef5","width":60,"height":24,"seed":1494065215,"groupIds":[],"roundness":{"type":2},"boundElements":[],"updated":1668907730051,"link":null,"locked":false,"fontSize":20,"fontFamily":3,"text":"fall!","rawText":"fall!","baseline":20,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"fall!"}],"appState":{"theme":"dark","viewBackgroundColor":"transparent","currentItemStrokeColor":"#000000","currentItemBackgroundColor":"#15aabf","currentItemFillStyle":"solid","currentItemStrokeWidth":1,"currentItemStrokeStyle":"solid","currentItemRoughness":2,"currentItemOpacity":100,"currentItemFontFamily":3,"currentItemFontSize":20,"currentItemTextAlign":"left","currentItemStartArrowhead":null,"currentItemEndArrowhead":"arrow","scrollX":221.30198435614548,"scrollY":315.5844328790648,"zoom":{"value":1.8},"currentItemRoundness":"round","gridSize":null,"colorPalette":{}},"files":{}};InitialData.scrollToContent=true;App=()=>{const e=React.useRef(null),t=React.useRef(null),[n,i]=React.useState({width:void 0,height:void 0});return React.useEffect(()=>{i({width:t.current.getBoundingClientRect().width,height:t.current.getBoundingClientRect().height});const e=()=>{i({width:t.current.getBoundingClientRect().width,height:t.current.getBoundingClientRect().height})};return window.addEventListener("resize",e),()=>window.removeEventListener("resize",e)},[t]),React.createElement(React.Fragment,null,React.createElement("div",{className:"excalidraw-wrapper",ref:t},React.createElement(ExcalidrawLib.Excalidraw,{ref:e,width:n.width,height:n.height,initialData:InitialData,viewModeEnabled:!0,zenModeEnabled:!0,gridModeEnabled:!1})))},excalidrawWrapper=document.getElementById("HatlightPlatform.excalidraw.md1");ReactDOM.render(React.createElement(App),excalidrawWrapper);})();</script>

### How We Fall
### どのように私たちは落ちるか

There are 4 steps to falling.

1) __Gravity__ 
	__落下速度が速くなります__。
1) __Move down__.
	**下に移動します**。
1) **Stop falling and pull out**.
	__壁にぶつかった__ 、__落ちるのをやめ__
1) **Go to `left/right`**.
	**`左右`の移動に戻ります**。

In detail:

1) First **gravity** makes us __fall faster__ 
	第 1 重力により、__落下速度が速くなります__。
1) Then we actually __move down__ if we can.
	次に、可能であれば実際に__下に移動__します。
1) If we __hit a wall__, we have to __stop falling and pull out__ of the wall.
	__壁にぶつかった__ 場合、__落ちるのをやめ__、壁から抜け出さなければなりません。
1) When we are done, we **go back to moving left and right**.
	完了したら、**左右の移動に戻ります**。

In terms of a flowchart and `y speed`, these 4 steps are:
1. Change `y speed` by `gravity`
1. Change `y position` by `y speed`
1. When you hit a wall **set `y speed` to 0** and **pull out**
1. **go back** to left/right



<div id="HatlightFalling.excalidraw.md2"></div><script>(function(){const InitialData={"type":"excalidraw","version":2,"source":"https://excalidraw.com","elements":[{"type":"rectangle","version":1719,"versionNonce":922237041,"isDeleted":false,"id":"Nwu0LtqoSmT45PmOhGbI0","fillStyle":"solid","strokeWidth":2,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-75.93290898354974,"y":-23037.31027142501,"strokeColor":"#5f3dc4","backgroundColor":"#fd7e14","width":417,"height":58,"seed":1762656049,"groupIds":[],"strokeSharpness":"round","boundElements":[{"id":"71yE5y0v","type":"text"},{"id":"jhNFrphANp3u00ECumDDS","type":"arrow"}],"updated":1670354397317,"link":null,"locked":false},{"type":"text","version":1873,"versionNonce":660205233,"isDeleted":false,"id":"71yE5y0v","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-38.43290898354974,"y":-23032.31027142501,"strokeColor":"#5f3dc4","backgroundColor":"transparent","width":342,"height":48,"seed":1868007519,"groupIds":[],"strokeSharpness":"sharp","boundElements":[],"updated":1670354406477,"link":null,"locked":false,"fontSize":20,"fontFamily":3,"text":"FALL FASTER:\nChange the y-speed by gravity","rawText":"FALL FASTER:\nChange the y-speed by gravity","baseline":43,"textAlign":"center","verticalAlign":"middle","containerId":"Nwu0LtqoSmT45PmOhGbI0","originalText":"FALL FASTER:\nChange the y-speed by gravity"},{"type":"rectangle","version":1943,"versionNonce":164967519,"isDeleted":false,"id":"1P7VB9ARxlKRJr1lHPf5q","fillStyle":"solid","strokeWidth":2,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-98.1226719587508,"y":-22963.595090922932,"strokeColor":"#5f3dc4","backgroundColor":"#fd7e14","width":459,"height":58,"seed":2047537425,"groupIds":[],"strokeSharpness":"round","boundElements":[{"id":"oCoGhJVT","type":"text"},{"id":"KUXSVk7kjG8YUUAb-OWLF","type":"arrow"},{"id":"jhNFrphANp3u00ECumDDS","type":"arrow"}],"updated":1670354380168,"link":null,"locked":false},{"type":"text","version":2014,"versionNonce":277742865,"isDeleted":false,"id":"oCoGhJVT","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-57.1226719587508,"y":-22958.595090922932,"strokeColor":"#5f3dc4","backgroundColor":"transparent","width":377,"height":48,"seed":891626623,"groupIds":[],"strokeSharpness":"sharp","boundElements":[],"updated":1670354380170,"link":null,"locked":false,"fontSize":20,"fontFamily":3,"text":"MOVE DOWN:\nChange the y position by y-speed","rawText":"MOVE DOWN:\nChange the y position by y-speed","baseline":43,"textAlign":"center","verticalAlign":"middle","containerId":"1P7VB9ARxlKRJr1lHPf5q","originalText":"MOVE DOWN:\nChange the y position by y-speed"},{"type":"rectangle","version":1973,"versionNonce":84975441,"isDeleted":false,"id":"dG_sTAK3ANmmsONJBhqjK","fillStyle":"solid","strokeWidth":2,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-100.91863808267414,"y":-22885.62611939426,"strokeColor":"#5f3dc4","backgroundColor":"#fd7e14","width":465,"height":58,"seed":1988929265,"groupIds":[],"strokeSharpness":"round","boundElements":[{"id":"QObjDLxV","type":"text"},{"id":"d5gJhw0lYPrHBm7mtrV9n","type":"arrow"},{"id":"KUXSVk7kjG8YUUAb-OWLF","type":"arrow"}],"updated":1670354422209,"link":null,"locked":false},{"type":"text","version":2172,"versionNonce":1793913713,"isDeleted":false,"id":"QObjDLxV","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-39.418638082674136,"y":-22880.62611939426,"strokeColor":"#5f3dc4","backgroundColor":"transparent","width":342,"height":48,"seed":53099679,"groupIds":[],"strokeSharpness":"sharp","boundElements":[],"updated":1670354432532,"link":null,"locked":false,"fontSize":20,"fontFamily":3,"text":"HIT A WALL OR PLATFORM:\nset y-speed to 0 and pull out","rawText":"HIT A WALL OR PLATFORM:\nset y-speed to 0 and pull out","baseline":43,"textAlign":"center","verticalAlign":"middle","containerId":"dG_sTAK3ANmmsONJBhqjK","originalText":"HIT A WALL OR PLATFORM:\nset y-speed to 0 and pull out"},{"type":"rectangle","version":2069,"versionNonce":1126528895,"isDeleted":false,"id":"u9b9U3IXBOQMFf2--IXVE","fillStyle":"solid","strokeWidth":2,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-44.75979565353754,"y":-22791.675596132824,"strokeColor":"#5f3dc4","backgroundColor":"#fd7e14","width":354,"height":40,"seed":1226612945,"groupIds":[],"strokeSharpness":"round","boundElements":[{"id":"Ar1U8pJf","type":"text"},{"id":"d5gJhw0lYPrHBm7mtrV9n","type":"arrow"}],"updated":1670349337260,"link":null,"locked":false},{"type":"text","version":2218,"versionNonce":606995935,"isDeleted":false,"id":"Ar1U8pJf","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":8.240204346462463,"y":-22783.675596132824,"strokeColor":"#5f3dc4","backgroundColor":"transparent","width":248,"height":24,"seed":1561809087,"groupIds":[],"strokeSharpness":"sharp","boundElements":[],"updated":1670354465465,"link":null,"locked":false,"fontSize":20,"fontFamily":3,"text":"GO BACK to left/right","rawText":"GO BACK to left/right","baseline":19,"textAlign":"center","verticalAlign":"middle","containerId":"u9b9U3IXBOQMFf2--IXVE","originalText":"GO BACK to left/right"},{"type":"arrow","version":1848,"versionNonce":600943825,"isDeleted":false,"id":"jhNFrphANp3u00ECumDDS","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":132.4910963441618,"y":-22978.31027142501,"strokeColor":"#e67700","backgroundColor":"transparent","width":0.01715843146524776,"height":13.715180502076691,"seed":525491889,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1670354454037,"link":null,"locked":false,"startBinding":{"elementId":"Nwu0LtqoSmT45PmOhGbI0","gap":1,"focus":0.0001844457279652866},"endBinding":{"elementId":"1P7VB9ARxlKRJr1lHPf5q","gap":1,"focus":0.00461399064563401},"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[-0.01715843146524776,13.715180502076691]]},{"type":"arrow","version":2575,"versionNonce":699886737,"isDeleted":false,"id":"KUXSVk7kjG8YUUAb-OWLF","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":132.94382706677362,"y":-22899.48266400566,"strokeColor":"#e67700","backgroundColor":"transparent","width":0.18853070633008429,"height":11.568341429647262,"seed":2089607391,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1670354454044,"link":null,"locked":false,"startBinding":{"elementId":"1P7VB9ARxlKRJr1lHPf5q","gap":6.112426917272387,"focus":-0.004223765307398561},"endBinding":{"elementId":"dG_sTAK3ANmmsONJBhqjK","gap":2.288203181753488,"focus":0.008846119530847275},"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[0.18853070633008429,11.568341429647262]]},{"type":"arrow","version":2149,"versionNonce":1431302655,"isDeleted":false,"id":"d5gJhw0lYPrHBm7mtrV9n","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":133.81713396769115,"y":-22822.596470478176,"strokeColor":"#e67700","backgroundColor":"transparent","width":0.9161803656889731,"height":27.675622459577426,"seed":131424401,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1670354474285,"link":null,"locked":false,"startBinding":{"elementId":"dG_sTAK3ANmmsONJBhqjK","gap":5.029648916082806,"focus":-0.014401483586944952},"endBinding":{"elementId":"u9b9U3IXBOQMFf2--IXVE","gap":3.2452518857753603,"focus":-0.0006122131952285393},"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[-0.9161803656889731,27.675622459577426]]}],"appState":{"theme":"dark","viewBackgroundColor":"transparent","currentItemStrokeColor":"#e67700","currentItemBackgroundColor":"transparent","currentItemFillStyle":"hachure","currentItemStrokeWidth":1,"currentItemStrokeStyle":"solid","currentItemRoughness":1,"currentItemOpacity":100,"currentItemFontFamily":3,"currentItemFontSize":20,"currentItemTextAlign":"left","currentItemStrokeSharpness":"sharp","currentItemStartArrowhead":null,"currentItemEndArrowhead":"arrow","currentItemLinearStrokeSharpness":"round","gridSize":null,"colorPalette":{}},"files":{}};InitialData.scrollToContent=true;App=()=>{const e=React.useRef(null),t=React.useRef(null),[n,i]=React.useState({width:void 0,height:void 0});return React.useEffect(()=>{i({width:t.current.getBoundingClientRect().width,height:t.current.getBoundingClientRect().height});const e=()=>{i({width:t.current.getBoundingClientRect().width,height:t.current.getBoundingClientRect().height})};return window.addEventListener("resize",e),()=>window.removeEventListener("resize",e)},[t]),React.createElement(React.Fragment,null,React.createElement("div",{className:"excalidraw-wrapper",ref:t},React.createElement(ExcalidrawLib.Excalidraw,{ref:e,width:n.width,height:n.height,initialData:InitialData,viewModeEnabled:!0,zenModeEnabled:!0,gridModeEnabled:!1})))},excalidrawWrapper=document.getElementById("HatlightFalling.excalidraw.md2");ReactDOM.render(React.createElement(App),excalidrawWrapper);})();</script>

### Create Myblocks
We will use myblocks for the 2 middle steps. I will show how to make these below, but first I will explain what is different about them.
   
    

#### Inputs and Booleans

````ad-example
title: Steps:


These myblocks are a little different from the simple ones we made in the first class for `set x speed` and `keep x speed below max`. We have to give these myblocks information. One has an __input field__, and the other has a __boolean field__.  In fact, I will give these myblocks names that explain more clearly what they actually do.




1) To MOVE DOWN/`change y by y-speed` we will actually fall (change the y speed) *one step at a time* because we want to stop as soon as we hit a wall. So I call the myblock "**change y by `y speed` in steps. Stop at wall**". How many steps we take (how far we fall) (and the direction) depends on  `y speed`, so we will give that information to the myblock. This is our __input field__, and it will be a number like -5 if we are falling, or +3 if we are jumping.
2) The did we HIT A WALL?`set y and pull out` step has a different piece of information it needs to get. This is because we could be falling OR jumping when we hit the wall. When we hit a "wall", we could be *falling* and hitting the ground, OR in fact we could be *jumping* and hitting a ceiling. Do we pull up out of the ground, or down out of the ceiling?? We need to let the myblock know if we are falling or jumping, that is, "**is  `y speed < 0` or not?**" We have to give that information to the myblock. Therefore I am calling that myblock "pull out if touching wall and `y speed < 0` or not". Like MOVE DOWN, this myblock also has an input, but this time the input is "are we falling?" or "is  `y speed < 0`?" The answer is yes (true) or no (false), not a number, so it is a __boolean__ input. In the myblock, Scratch will turn the boolean into the number we need, which tells us how much and which way to pull out. 
```ad-scratch
title:
~~~scratchblock
when I receive [fall v]
change [y speed v] by (-1)
change y by (y speed) in steps. Stop at wall.::custom
At this point we may be touching a wall
If so, we should pull out of the wall.
We use the value of <(y speed) \< [0]> like this: 
TRUE: we were falling \(hitting the floor\)
FALSE: we were jumping \(hitting a ceiling/platform\)
pull out if touching wall and <(y speed) \< [0]> or not?::custom
broadcast [move left / right v]
~~~
```
````

#### Change Y Block

First, let's make the *change y* myblock. To make this, click `create a block` like before, and this time:

````ad-example
title: Steps:
1. Fill in the first label ("`change y by`")  
2. Add an input field (`y speed`) (round edges "( ... )" )  
```ad-tip
title: 
Input fields take variables and expressions like a + b.  
```
3. And add another label field ("`in steps. Stop at wall`")

The actual label text is not important, and you can choose your own words. Make it meaningful for you.  
````

Final result:

```ad-scratch
title: hitbox, define change y
~~~scratchblock
define change y by (y speed) in steps. Stop at wall.::custom
~~~
```

#### Pull Out if Touching Wall Block

````ad-example
title: Steps
1. Fill in the first label ("`pull out if touching wall and`")  
2. Add a **boolean** field <`falling?`> (pointy edges "< ... >")  
```ad-tip
title:
A **boolean** field is different than an input field. It only takes things like sensing blocks and logical connectors (`and`, `or`)
```
3. And another label field ("`or not`")

Again you can choose your own words for the text of the fields.  Make it meaningful for you.
````

Final result:

```ad-scratch
title: Htibox, define pull up
~~~scratchblock
define pull out if touching wall and <falling?> or not
~~~
```

## Falling Myblock Code

Now, let's make the code for the myblocks.

### Change Y: Not Big Jumps, but Single Steps

We could change the y position by y speed in big jumps, like on the left in the diagram below, but it might turn out we would jump beyond the platform. Notice how the jumps get bigger and bigger. This is gravity pulling the hitbox down.

<div id="HatlightFalllingInSteps.excalidraw.md3"></div><script>(function(){const InitialData={"type":"excalidraw","version":2,"source":"https://excalidraw.com","elements":[{"type":"rectangle","version":573,"versionNonce":779415510,"isDeleted":false,"id":"X3eKC4g-yx-XMt1rWBuif","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":0,"opacity":90,"angle":0,"x":-446.13886414331495,"y":-218.2046463665598,"strokeColor":"#000000","backgroundColor":"#15aabf","width":580.8837890625,"height":409.2378845214844,"seed":1523261399,"groupIds":[],"roundness":null,"boundElements":[],"updated":1673394088142,"link":null,"locked":false},{"type":"rectangle","version":343,"versionNonce":169716746,"isDeleted":false,"id":"0fbDeUvnFGOAHWrwifOSV","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-447.1328125,"y":60.158935546875,"strokeColor":"#000000","backgroundColor":"#fa5252","width":578.7227783203125,"height":52.170654296875,"seed":1658367257,"groupIds":[],"roundness":{"type":1},"boundElements":[{"id":"KzzUe-i6RXE-mzwhfi58q","type":"arrow"},{"id":"BLtrddpDIMI7sGaAGwKk-","type":"arrow"},{"id":"X0vEXzL366tfW-NuY40fC","type":"arrow"},{"id":"blo4yQwW9sP5B3XOH_GAR","type":"arrow"}],"updated":1673393715123,"link":null,"locked":false},{"type":"rectangle","version":268,"versionNonce":2106928406,"isDeleted":false,"id":"aSzZsl74H852Oj-GLVfFu","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-378.5940653483073,"y":-171.21595836821058,"strokeColor":"#000000","backgroundColor":"#4c6ef5","width":57.265625,"height":54.74920654296875,"seed":1445399799,"groupIds":[],"roundness":{"type":1},"boundElements":[],"updated":1673393475368,"link":null,"locked":false},{"type":"arrow","version":490,"versionNonce":863000394,"isDeleted":false,"id":"g4ekkcbqxsQejMG8sMtHJ","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-322.04160417829235,"y":-119.28085908435634,"strokeColor":"#000000","backgroundColor":"transparent","width":34.315359933035836,"height":40.774100167410666,"seed":1905810487,"groupIds":[],"roundness":{"type":2},"boundElements":[],"updated":1673393475368,"link":null,"locked":false,"startBinding":null,"endBinding":null,"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[30.880417596726204,25.17081124441961],[-3.434942336309632,40.774100167410666]]},{"type":"arrow","version":685,"versionNonce":1004214870,"isDeleted":false,"id":"2AgNi4LavDQ_DT3pTVCAZ","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-325.1728239513577,"y":-75.07850138346353,"strokeColor":"#000000","backgroundColor":"transparent","width":30.530598958333485,"height":47.169131324404646,"seed":983790713,"groupIds":[],"roundness":{"type":2},"boundElements":[],"updated":1673393475368,"link":null,"locked":false,"startBinding":null,"endBinding":null,"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[28.942522321428612,24.00812058221726],[-1.5880766369048729,47.169131324404646]]},{"type":"arrow","version":1131,"versionNonce":1455087114,"isDeleted":false,"id":"X0vEXzL366tfW-NuY40fC","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-327.6087661016555,"y":-26.44208490280866,"strokeColor":"#000000","backgroundColor":"transparent","width":34.75597563244054,"height":70.71970331101181,"seed":1849024089,"groupIds":[],"roundness":{"type":2},"boundElements":[],"updated":1673393475368,"link":null,"locked":false,"startBinding":null,"endBinding":{"elementId":"0fbDeUvnFGOAHWrwifOSV","focus":-0.6814801411047785,"gap":15.881317138671847},"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[34.75597563244054,31.764758882068406],[10.240886056457782,70.71970331101181]]},{"type":"arrow","version":1188,"versionNonce":386412874,"isDeleted":false,"id":"KzzUe-i6RXE-mzwhfi58q","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-316.7308580750426,"y":47.09451729910708,"strokeColor":"#000000","backgroundColor":"transparent","width":36.471470424107224,"height":99.21650768461689,"seed":595548951,"groupIds":[],"roundness":{"type":2},"boundElements":[],"updated":1673393863889,"link":null,"locked":false,"startBinding":{"elementId":"0fbDeUvnFGOAHWrwifOSV","focus":0.4748220978688334,"gap":13.064418247767918},"endBinding":{"elementId":"FFjJe3DO","focus":-0.21726661880131412,"gap":1.6255536760602638},"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[19.075134139960824,45.58697945731029],[-17.3963362841464,99.21650768461689]]},{"type":"text","version":184,"versionNonce":612797642,"isDeleted":false,"id":"FFjJe3DO","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-431.50949823288687,"y":147.93657865978423,"strokeColor":"#000000","backgroundColor":"transparent","width":229,"height":25,"seed":1764694073,"groupIds":[],"roundness":null,"boundElements":[{"id":"KzzUe-i6RXE-mzwhfi58q","type":"arrow"}],"updated":1673393475368,"link":null,"locked":false,"fontSize":20,"fontFamily":1,"text":"oops I jumped too far!","rawText":"oops I jumped too far!","baseline":18,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"oops I jumped too far!"},{"type":"rectangle","version":401,"versionNonce":915209430,"isDeleted":false,"id":"UdmsIpWycJ77Ag8M3_jmW","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-147.30171857561396,"y":-169.37390500023255,"strokeColor":"#000000","backgroundColor":"#4c6ef5","width":57.265625,"height":54.74920654296875,"seed":1579585465,"groupIds":[],"roundness":{"type":1},"boundElements":[{"id":"i5h6ALg0GKwRab9r0C90J","type":"arrow"}],"updated":1673393475368,"link":null,"locked":false},{"type":"text","version":562,"versionNonce":769775946,"isDeleted":false,"id":"XbZ1dBRn","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-145.6397283644904,"y":75.02710852684913,"strokeColor":"#000000","backgroundColor":"transparent","width":175,"height":20,"seed":327270615,"groupIds":[],"roundness":null,"boundElements":[{"id":"blo4yQwW9sP5B3XOH_GAR","type":"arrow"}],"updated":1673393839219,"link":null,"locked":false,"fontSize":15.849432887262545,"fontFamily":1,"text":"I stop inside the wall!","rawText":"I stop inside the wall!","baseline":14,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"I stop inside the wall!"},{"type":"rectangle","version":451,"versionNonce":1061873430,"isDeleted":false,"id":"-Dk-PL6qwRITfi6xHjJ4O","fillStyle":"solid","strokeWidth":0.5,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-146.3138168372824,"y":20.027088862932374,"strokeColor":"#000000","backgroundColor":"#ced4da","width":57.265625,"height":54.74920654296875,"seed":670711562,"groupIds":[],"roundness":{"type":1},"boundElements":[{"id":"BLtrddpDIMI7sGaAGwKk-","type":"arrow"},{"id":"blo4yQwW9sP5B3XOH_GAR","type":"arrow"}],"updated":1673393720587,"link":null,"locked":false},{"type":"arrow","version":684,"versionNonce":32918038,"isDeleted":false,"id":"i5h6ALg0GKwRab9r0C90J","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-85.63133048185534,"y":-119.54676714413216,"strokeColor":"#000000","backgroundColor":"transparent","width":39.765834051648156,"height":43.69067235312329,"seed":2040880983,"groupIds":["GqIiQvxPWWtvjf3-ZGR_E"],"roundness":{"type":2},"boundElements":[],"updated":1673394090256,"link":null,"locked":false,"startBinding":{"elementId":"WcU2UzjQ","focus":1.1040025402346152,"gap":11.8412914193554},"endBinding":null,"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[30.880417596726204,25.17081124441961],[-8.885416454921952,43.69067235312329]]},{"type":"arrow","version":913,"versionNonce":628530838,"isDeleted":false,"id":"xE_jOsYBF4k_BoFbHpGdK","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-92.42129286473882,"y":-73.61957030239121,"strokeColor":"#000000","backgroundColor":"transparent","width":32.87689969687172,"height":45.53713450054138,"seed":1701062041,"groupIds":["GqIiQvxPWWtvjf3-ZGR_E"],"roundness":{"type":2},"boundElements":[],"updated":1673394023761,"link":null,"locked":false,"startBinding":null,"endBinding":null,"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[32.87689969687172,22.28328144136914],[2.2445551330694826,45.53713450054138]]},{"type":"arrow","version":1231,"versionNonce":1996196426,"isDeleted":false,"id":"BLtrddpDIMI7sGaAGwKk-","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-91.19849240521847,"y":-26.633113337420916,"strokeColor":"#000000","backgroundColor":"transparent","width":34.75597563244054,"height":65.91786633468992,"seed":781016183,"groupIds":["GqIiQvxPWWtvjf3-ZGR_E"],"roundness":{"type":2},"boundElements":[],"updated":1673394090256,"link":null,"locked":false,"startBinding":null,"endBinding":{"elementId":"IrI6KQJV","focus":-1.1272728471639077,"gap":11.71138980467974},"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[34.75597563244054,31.689879256904867],[3.5958062138200404,65.91786633468992]]},{"type":"text","version":314,"versionNonce":1256151498,"isDeleted":false,"id":"eF8vvNIu","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-49.29003906249994,"y":-99.45694392480902,"strokeColor":"#000000","backgroundColor":"transparent","width":24,"height":25,"seed":1001960855,"groupIds":["XTuGMrxn6Otwpjz8ioNSR"],"roundness":null,"boundElements":[],"updated":1673393605769,"link":null,"locked":false,"fontSize":20,"fontFamily":1,"text":"-2","rawText":"-2","baseline":18,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"-2"},{"type":"text","version":371,"versionNonce":1488158678,"isDeleted":false,"id":"1eX2ixah","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-48.29003906249994,"y":-4.531011540136234,"strokeColor":"#000000","backgroundColor":"transparent","width":22,"height":25,"seed":2019289783,"groupIds":["XTuGMrxn6Otwpjz8ioNSR"],"roundness":null,"boundElements":[],"updated":1673393605769,"link":null,"locked":false,"fontSize":20,"fontFamily":1,"text":"-4","rawText":"-4","baseline":18,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"-4"},{"type":"text","version":361,"versionNonce":1579520138,"isDeleted":false,"id":"uqL6JY9q","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-48.79003906249994,"y":-59.167067622725654,"strokeColor":"#000000","backgroundColor":"transparent","width":23,"height":25,"seed":1001816121,"groupIds":["XTuGMrxn6Otwpjz8ioNSR"],"roundness":null,"boundElements":[],"updated":1673393605769,"link":null,"locked":false,"fontSize":20,"fontFamily":1,"text":"-3","rawText":"-3","baseline":18,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"-3"},{"type":"text","version":243,"versionNonce":134953942,"isDeleted":false,"id":"WcU2UzjQ","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-73.79003906249994,"y":-139.2891097956405,"strokeColor":"#000000","backgroundColor":"transparent","width":73,"height":25,"seed":1711725591,"groupIds":["XTuGMrxn6Otwpjz8ioNSR"],"roundness":null,"boundElements":[{"id":"i5h6ALg0GKwRab9r0C90J","type":"arrow"}],"updated":1673393676208,"link":null,"locked":false,"fontSize":20,"fontFamily":1,"text":"y-speed","rawText":"y-speed","baseline":18,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"y-speed"},{"type":"text","version":440,"versionNonce":1539789642,"isDeleted":false,"id":"IrI6KQJV","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-75.8912963867187,"y":38.985806419735866,"strokeColor":"#000000","backgroundColor":"transparent","width":157,"height":25,"seed":572946999,"groupIds":["XTuGMrxn6Otwpjz8ioNSR"],"roundness":null,"boundElements":[{"id":"blo4yQwW9sP5B3XOH_GAR","type":"arrow"},{"id":"BLtrddpDIMI7sGaAGwKk-","type":"arrow"}],"updated":1673394023797,"link":null,"locked":false,"fontSize":20,"fontFamily":1,"text":"-5 but we stop!","rawText":"-5 but we stop!","baseline":18,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"-5 but we stop!"},{"type":"text","version":332,"versionNonce":2033419082,"isDeleted":false,"id":"Dtv9HTI8","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-211.4044189453125,"y":-104.82800583612351,"strokeColor":"#000000","backgroundColor":"transparent","width":88,"height":15,"seed":1940233465,"groupIds":[],"roundness":null,"boundElements":[],"updated":1673393475368,"link":null,"locked":false,"fontSize":11.564513367491873,"fontFamily":1,"text":"repeat 2 times","rawText":"repeat 2 times","baseline":10,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"repeat 2 times"},{"type":"text","version":349,"versionNonce":137408086,"isDeleted":false,"id":"8oL2ADB6","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-210.4044189453125,"y":-66.63830044568874,"strokeColor":"#000000","backgroundColor":"transparent","width":87,"height":15,"seed":1478327543,"groupIds":[],"roundness":null,"boundElements":[],"updated":1673393475368,"link":null,"locked":false,"fontSize":11.564513367491873,"fontFamily":1,"text":"repeat 3 times","rawText":"repeat 3 times","baseline":10,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"repeat 3 times"},{"type":"text","version":361,"versionNonce":1396214282,"isDeleted":false,"id":"8xaobg7y","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-210.4044189453125,"y":-10.758631256235617,"strokeColor":"#000000","backgroundColor":"transparent","width":87,"height":15,"seed":1050181433,"groupIds":[],"roundness":null,"boundElements":[],"updated":1673393475368,"link":null,"locked":false,"fontSize":11.564513367491873,"fontFamily":1,"text":"repeat 4 times","rawText":"repeat 4 times","baseline":10,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"repeat 4 times"},{"id":"lyaz_giGeAbzGXOc5AhNk","type":"rectangle","x":-213.1973007240012,"y":41.74690697816675,"width":94.03475952148438,"height":30.5076904296875,"angle":0,"strokeColor":"#862e9c","backgroundColor":"#12b886","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":90,"groupIds":["SCUoM_LGPu_yXPUHhbyLu"],"roundness":{"type":3},"seed":275945942,"version":126,"versionNonce":830607830,"isDeleted":false,"boundElements":null,"updated":1673393991572,"link":null,"locked":false},{"type":"text","version":742,"versionNonce":750853770,"isDeleted":false,"id":"2lyzJYzq","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-206.679920963259,"y":42.83079238164993,"strokeColor":"#000000","backgroundColor":"transparent","width":81,"height":29,"seed":666969721,"groupIds":["SCUoM_LGPu_yXPUHhbyLu"],"roundness":null,"boundElements":[],"updated":1673393991572,"link":null,"locked":false,"fontSize":11.564513367491873,"fontFamily":1,"text":"we stop after\nthe 2nd time","rawText":"we stop after\nthe 2nd time","baseline":25,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"we stop after\nthe 2nd time"},{"type":"text","version":445,"versionNonce":477018314,"isDeleted":false,"id":"IbInAoJb","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-278.8067321777344,"y":-99.5947307900434,"strokeColor":"#000000","backgroundColor":"transparent","width":24,"height":25,"seed":963405561,"groupIds":["L2mtHY-W5mC-w7fjiNLVf"],"roundness":null,"boundElements":[],"updated":1673393475368,"link":null,"locked":false,"fontSize":20,"fontFamily":1,"text":"-2","rawText":"-2","baseline":18,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"-2"},{"type":"text","version":503,"versionNonce":831361238,"isDeleted":false,"id":"hSc6JIhn","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-277.8067321777344,"y":-4.668798405370609,"strokeColor":"#000000","backgroundColor":"transparent","width":22,"height":25,"seed":791437591,"groupIds":["L2mtHY-W5mC-w7fjiNLVf"],"roundness":null,"boundElements":[],"updated":1673393475368,"link":null,"locked":false,"fontSize":20,"fontFamily":1,"text":"-4","rawText":"-4","baseline":18,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"-4"},{"type":"text","version":491,"versionNonce":611389322,"isDeleted":false,"id":"VhzbCA86","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-278.3067321777344,"y":-59.30485448796003,"strokeColor":"#000000","backgroundColor":"transparent","width":23,"height":25,"seed":1897340889,"groupIds":["L2mtHY-W5mC-w7fjiNLVf"],"roundness":null,"boundElements":[],"updated":1673393475368,"link":null,"locked":false,"fontSize":20,"fontFamily":1,"text":"-3","rawText":"-3","baseline":18,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"-3"},{"type":"text","version":374,"versionNonce":1653671446,"isDeleted":false,"id":"QrDPRnCQ","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-303.3067321777344,"y":-139.4268966608749,"strokeColor":"#000000","backgroundColor":"transparent","width":73,"height":25,"seed":659433015,"groupIds":["L2mtHY-W5mC-w7fjiNLVf"],"roundness":null,"boundElements":[],"updated":1673393475368,"link":null,"locked":false,"fontSize":20,"fontFamily":1,"text":"y-speed","rawText":"y-speed","baseline":18,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"y-speed"},{"type":"text","version":477,"versionNonce":259690058,"isDeleted":false,"id":"CPx8eJtp","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-277.8067321777344,"y":38.547635033017116,"strokeColor":"#000000","backgroundColor":"transparent","width":22,"height":25,"seed":1488436409,"groupIds":["L2mtHY-W5mC-w7fjiNLVf"],"roundness":null,"boundElements":[],"updated":1673393475368,"link":null,"locked":false,"fontSize":20,"fontFamily":1,"text":"-5","rawText":"-5","baseline":18,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"-5"},{"type":"text","version":255,"versionNonce":636736342,"isDeleted":false,"id":"wQFuVFii","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":0,"opacity":90,"angle":0,"x":-372.37231729544834,"y":-203.7640727434215,"strokeColor":"#000000","backgroundColor":"#15aabf","width":134,"height":28,"seed":1343495823,"groupIds":[],"roundness":null,"boundElements":[],"updated":1673393475368,"link":null,"locked":false,"fontSize":20,"fontFamily":1,"text":"BIG jumps ❌","rawText":"BIG jumps ❌","baseline":20,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"BIG jumps ❌"},{"type":"text","version":556,"versionNonce":1113994506,"isDeleted":false,"id":"csfpIZ0v","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":0,"opacity":90,"angle":0,"x":-143.57462243231532,"y":-203.9287469630633,"strokeColor":"#000000","backgroundColor":"#15aabf","width":160,"height":28,"seed":2028349825,"groupIds":[],"roundness":null,"boundElements":[],"updated":1673393475368,"link":null,"locked":false,"fontSize":20,"fontFamily":1,"text":"SMALL steps ✅","rawText":"SMALL steps ✅","baseline":20,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"SMALL steps ✅"},{"type":"arrow","version":2842,"versionNonce":1136044490,"isDeleted":false,"id":"bwETjqIAwsfaCBXToq7mr","fillStyle":"hachure","strokeWidth":2,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-98.93328735455802,"y":-112.81501422670092,"strokeColor":"#862e9c","backgroundColor":"transparent","width":13.856572150963103,"height":10.931379070486201,"seed":51659158,"groupIds":["wyA1Lk3TbbMGq0vS8op__","Q6DyyDpRBzA7F5T9GJ9Nt"],"roundness":{"type":2},"boundElements":[],"updated":1673393563878,"link":null,"locked":false,"startBinding":{"elementId":"ctgLPHBO","focus":1.5463870030531564,"gap":13.871785480981828},"endBinding":{"elementId":"FTeCu3eZ","focus":0.21833418349062747,"gap":14.0985978045654},"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[-10.570859372029787,5.047996387929032],[3.2857127789333163,10.931379070486201]]},{"type":"text","version":1243,"versionNonce":1850694038,"isDeleted":false,"id":"FTeCu3eZ","fillStyle":"hachure","strokeWidth":2,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-115.7461723801901,"y":-116.29127110208401,"strokeColor":"#862e9c","backgroundColor":"transparent","width":5,"height":19,"seed":1501798102,"groupIds":["wyA1Lk3TbbMGq0vS8op__","Q6DyyDpRBzA7F5T9GJ9Nt"],"roundness":null,"boundElements":[{"id":"bwETjqIAwsfaCBXToq7mr","type":"arrow"},{"id":"xE_jOsYBF4k_BoFbHpGdK","type":"arrow"}],"updated":1673393563325,"link":null,"locked":false,"fontSize":14.39868181190029,"fontFamily":1,"text":"1","rawText":"1","baseline":13,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"1"},{"type":"arrow","version":3029,"versionNonce":2008625110,"isDeleted":false,"id":"30AQK5MQuPXKIWI8XeajQ","fillStyle":"hachure","strokeWidth":2,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-98.93328735455805,"y":-95.46697187033601,"strokeColor":"#862e9c","backgroundColor":"transparent","width":11.205346347050934,"height":13.077480845036746,"seed":2090161174,"groupIds":["UCExYSlleJjMwFZ7Qzell","Q6DyyDpRBzA7F5T9GJ9Nt"],"roundness":{"type":2},"boundElements":[],"updated":1673393563879,"link":null,"locked":false,"startBinding":{"elementId":"jJvHk8rL","focus":1.546387003053157,"gap":13.871785480981828},"endBinding":{"elementId":"jJvHk8rL","focus":2.036078995773421,"gap":12.447372000653218},"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[-10.570859372029787,5.047996387929032],[0.6344869750211473,13.077480845036746]]},{"type":"text","version":1331,"versionNonce":1978297366,"isDeleted":false,"id":"ctgLPHBO","fillStyle":"hachure","strokeWidth":2,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-115.7461723801901,"y":-98.9432287457191,"strokeColor":"#862e9c","backgroundColor":"transparent","width":5,"height":19,"seed":1446928726,"groupIds":["UCExYSlleJjMwFZ7Qzell","Q6DyyDpRBzA7F5T9GJ9Nt"],"roundness":null,"boundElements":[{"id":"30AQK5MQuPXKIWI8XeajQ","type":"arrow"},{"id":"i5h6ALg0GKwRab9r0C90J","type":"arrow"},{"id":"xE_jOsYBF4k_BoFbHpGdK","type":"arrow"},{"id":"bwETjqIAwsfaCBXToq7mr","type":"arrow"}],"updated":1673393563325,"link":null,"locked":false,"fontSize":14.39868181190029,"fontFamily":1,"text":"1","rawText":"1","baseline":13,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"1"},{"type":"arrow","version":3316,"versionNonce":1603461258,"isDeleted":false,"id":"BIlN-z6qp0Zwaqb-TssE9","fillStyle":"hachure","strokeWidth":2,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-98.93328735455808,"y":-43.422844801241254,"strokeColor":"#862e9c","backgroundColor":"transparent","width":13.856572150963103,"height":10.931379070486201,"seed":1238615702,"groupIds":["NQ-rDOsEk5HrskJzH4NlO","Q6DyyDpRBzA7F5T9GJ9Nt"],"roundness":{"type":2},"boundElements":[],"updated":1673393563879,"link":null,"locked":false,"startBinding":{"elementId":"3l5Xdm3B","focus":-1.6981034063394247,"gap":11.812885025632028},"endBinding":{"elementId":"htRXZrxu","focus":1.9525435086164775,"gap":15.098597804565358},"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[-10.570859372029787,5.047996387929032],[3.2857127789333163,10.931379070486201]]},{"type":"text","version":1498,"versionNonce":1865346826,"isDeleted":false,"id":"lW84oqgi","fillStyle":"hachure","strokeWidth":2,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-115.7461723801901,"y":-46.89910167662434,"strokeColor":"#862e9c","backgroundColor":"transparent","width":5,"height":19,"seed":134906838,"groupIds":["NQ-rDOsEk5HrskJzH4NlO","Q6DyyDpRBzA7F5T9GJ9Nt"],"roundness":null,"boundElements":[{"id":"BIlN-z6qp0Zwaqb-TssE9","type":"arrow"},{"id":"i5h6ALg0GKwRab9r0C90J","type":"arrow"},{"id":"xE_jOsYBF4k_BoFbHpGdK","type":"arrow"},{"id":"itKSWnAAJjQpjm2vWnion","type":"arrow"},{"id":"pbeHb5a0uoNX9WtBB610c","type":"arrow"}],"updated":1673393563325,"link":null,"locked":false,"fontSize":14.39868181190029,"fontFamily":1,"text":"1","rawText":"1","baseline":13,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"1"},{"type":"arrow","version":3531,"versionNonce":1072743702,"isDeleted":false,"id":"itKSWnAAJjQpjm2vWnion","fillStyle":"hachure","strokeWidth":2,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-100.00813040323456,"y":-77.41682196894158,"strokeColor":"#862e9c","backgroundColor":"transparent","width":12.926063450679067,"height":10.229271525456682,"seed":1660393750,"groupIds":["rDGyDIC4wj-sxzu3feEwR","Q6DyyDpRBzA7F5T9GJ9Nt"],"roundness":{"type":2},"boundElements":[],"updated":1673393563879,"link":null,"locked":false,"startBinding":{"elementId":"3l5Xdm3B","focus":0.9775732917173402,"gap":13.169677935952308},"endBinding":{"elementId":"jJvHk8rL","focus":0.21833418349062747,"gap":14.0985978045654},"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[-8.565507623069209,7.309658929014603],[4.360555827609858,10.229271525456682]]},{"type":"text","version":1423,"versionNonce":267427670,"isDeleted":false,"id":"jJvHk8rL","fillStyle":"hachure","strokeWidth":2,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-115.7461723801901,"y":-81.59518638935418,"strokeColor":"#862e9c","backgroundColor":"transparent","width":5,"height":19,"seed":571475542,"groupIds":["rDGyDIC4wj-sxzu3feEwR","Q6DyyDpRBzA7F5T9GJ9Nt"],"roundness":null,"boundElements":[{"id":"itKSWnAAJjQpjm2vWnion","type":"arrow"},{"id":"i5h6ALg0GKwRab9r0C90J","type":"arrow"},{"id":"30AQK5MQuPXKIWI8XeajQ","type":"arrow"}],"updated":1673393691339,"link":null,"locked":false,"fontSize":14.39868181190029,"fontFamily":1,"text":"1","rawText":"1","baseline":13,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"1"},{"type":"arrow","version":3084,"versionNonce":138035018,"isDeleted":false,"id":"pbeHb5a0uoNX9WtBB610c","fillStyle":"hachure","strokeWidth":2,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-98.93328735455805,"y":-26.07480244487636,"strokeColor":"#862e9c","backgroundColor":"transparent","width":13.856572150963103,"height":10.931379070486201,"seed":1445514134,"groupIds":["4rrK6TF_CuV7ezukefjSq","Q6DyyDpRBzA7F5T9GJ9Nt"],"roundness":{"type":2},"boundElements":[],"updated":1673393563879,"link":null,"locked":false,"startBinding":{"elementId":"FriW2rj1","focus":1.5463870030531606,"gap":13.871785480981863},"endBinding":{"elementId":"lW84oqgi","focus":-1.4668957946110344,"gap":15.098597804565358},"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[-10.570859372029787,5.047996387929032],[3.2857127789333163,10.931379070486201]]},{"type":"text","version":1388,"versionNonce":1635916298,"isDeleted":false,"id":"htRXZrxu","fillStyle":"hachure","strokeWidth":2,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-115.7461723801901,"y":-29.55105932025942,"strokeColor":"#862e9c","backgroundColor":"transparent","width":5,"height":19,"seed":762767574,"groupIds":["4rrK6TF_CuV7ezukefjSq","Q6DyyDpRBzA7F5T9GJ9Nt"],"roundness":null,"boundElements":[{"id":"i5h6ALg0GKwRab9r0C90J","type":"arrow"},{"id":"BIlN-z6qp0Zwaqb-TssE9","type":"arrow"}],"updated":1673393563325,"link":null,"locked":false,"fontSize":14.39868181190029,"fontFamily":1,"text":"1","rawText":"1","baseline":13,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"1"},{"type":"arrow","version":3528,"versionNonce":1594077782,"isDeleted":false,"id":"Sz8xeGELrBil9xoaOIm_J","fillStyle":"hachure","strokeWidth":2,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-98.79546997174555,"y":43.31736698058335,"strokeColor":"#862e9c","backgroundColor":"transparent","width":13.856572150963103,"height":10.931379070486201,"seed":1200578070,"groupIds":["UWcnU8VbgbX9PWpg8IRha","Q6DyyDpRBzA7F5T9GJ9Nt"],"roundness":{"type":2},"boundElements":[],"updated":1673393563879,"link":null,"locked":false,"startBinding":{"elementId":"FTpz62VY","focus":-1.704257707770645,"gap":11.950702408444556},"endBinding":{"focus":0.21833418349062633,"gap":14.098597804565372,"elementId":"lDDvswtv"},"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[-10.570859372029787,5.047996387929032],[3.2857127789333163,10.931379070486201]]},{"type":"text","version":1625,"versionNonce":100073686,"isDeleted":false,"id":"lDDvswtv","fillStyle":"hachure","strokeWidth":2,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-115.7461723801901,"y":39.841110105200265,"strokeColor":"#862e9c","backgroundColor":"transparent","width":5,"height":19,"seed":157756246,"groupIds":["UWcnU8VbgbX9PWpg8IRha","Q6DyyDpRBzA7F5T9GJ9Nt"],"roundness":null,"boundElements":[{"id":"Sz8xeGELrBil9xoaOIm_J","type":"arrow"},{"id":"i5h6ALg0GKwRab9r0C90J","type":"arrow"},{"id":"xE_jOsYBF4k_BoFbHpGdK","type":"arrow"},{"id":"itKSWnAAJjQpjm2vWnion","type":"arrow"},{"id":"BLtrddpDIMI7sGaAGwKk-","type":"arrow"}],"updated":1673393563325,"link":null,"locked":false,"fontSize":14.39868181190029,"fontFamily":1,"text":"1","rawText":"1","baseline":13,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"1"},{"type":"arrow","version":3472,"versionNonce":1242023434,"isDeleted":false,"id":"R4mfxyq1rVtvRc5OSL9QM","fillStyle":"hachure","strokeWidth":2,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-98.9332873545581,"y":-8.726760088511412,"strokeColor":"#862e9c","backgroundColor":"transparent","width":13.856572150963103,"height":10.931379070486201,"seed":1901285526,"groupIds":["nwIQTCVt-HW39_YL7nIJy","Q6DyyDpRBzA7F5T9GJ9Nt"],"roundness":{"type":2},"boundElements":[],"updated":1673393563879,"link":null,"locked":false,"startBinding":{"elementId":"gyk0nbcr","focus":1.5463870030531606,"gap":13.871785480981835},"endBinding":{"elementId":"gyk0nbcr","focus":2.245421592220018,"gap":15.098597804565316},"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[-10.570859372029787,5.047996387929032],[3.2857127789333163,10.931379070486201]]},{"type":"text","version":1593,"versionNonce":583091030,"isDeleted":false,"id":"FriW2rj1","fillStyle":"hachure","strokeWidth":2,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-115.7461723801901,"y":-12.203016963894498,"strokeColor":"#862e9c","backgroundColor":"transparent","width":5,"height":19,"seed":1795739094,"groupIds":["nwIQTCVt-HW39_YL7nIJy","Q6DyyDpRBzA7F5T9GJ9Nt"],"roundness":null,"boundElements":[{"id":"R4mfxyq1rVtvRc5OSL9QM","type":"arrow"},{"id":"i5h6ALg0GKwRab9r0C90J","type":"arrow"},{"id":"xE_jOsYBF4k_BoFbHpGdK","type":"arrow"},{"id":"itKSWnAAJjQpjm2vWnion","type":"arrow"},{"id":"pbeHb5a0uoNX9WtBB610c","type":"arrow"}],"updated":1673393563325,"link":null,"locked":false,"fontSize":14.39868181190029,"fontFamily":1,"text":"1","rawText":"1","baseline":13,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"1"},{"type":"arrow","version":3577,"versionNonce":264697750,"isDeleted":false,"id":"sGG3rEuEkggAAXmB2n6iz","fillStyle":"hachure","strokeWidth":2,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-98.9332873545581,"y":8.621282267853509,"strokeColor":"#862e9c","backgroundColor":"transparent","width":13.856572150963103,"height":10.931379070486201,"seed":597467926,"groupIds":["8PqRhJn4x0YIw2xmuRPxm","Q6DyyDpRBzA7F5T9GJ9Nt"],"roundness":{"type":2},"boundElements":[],"updated":1673393563879,"link":null,"locked":false,"startBinding":{"elementId":"FTpz62VY","focus":1.5463870030531606,"gap":13.871785480981835},"endBinding":{"focus":0.21833418349062633,"gap":14.098597804565372,"elementId":"gyk0nbcr"},"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[-10.570859372029787,5.047996387929032],[3.2857127789333163,10.931379070486201]]},{"type":"text","version":1656,"versionNonce":1828623306,"isDeleted":false,"id":"gyk0nbcr","fillStyle":"hachure","strokeWidth":2,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-115.7461723801901,"y":5.145025392470423,"strokeColor":"#862e9c","backgroundColor":"transparent","width":5,"height":19,"seed":1568919638,"groupIds":["8PqRhJn4x0YIw2xmuRPxm","Q6DyyDpRBzA7F5T9GJ9Nt"],"roundness":null,"boundElements":[{"id":"sGG3rEuEkggAAXmB2n6iz","type":"arrow"},{"id":"i5h6ALg0GKwRab9r0C90J","type":"arrow"},{"id":"xE_jOsYBF4k_BoFbHpGdK","type":"arrow"},{"id":"itKSWnAAJjQpjm2vWnion","type":"arrow"},{"id":"R4mfxyq1rVtvRc5OSL9QM","type":"arrow"}],"updated":1673393563325,"link":null,"locked":false,"fontSize":14.39868181190029,"fontFamily":1,"text":"1","rawText":"1","baseline":13,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"1"},{"type":"arrow","version":3548,"versionNonce":1844868298,"isDeleted":false,"id":"3bknPLUtZ6TwY8rTrR0l8","fillStyle":"hachure","strokeWidth":2,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-98.93328735455805,"y":60.66540933694827,"strokeColor":"#862e9c","backgroundColor":"transparent","width":13.856572150963103,"height":10.931379070486201,"seed":1150506390,"groupIds":["KaZYyii1iTZ8-nNvVM93q","Q6DyyDpRBzA7F5T9GJ9Nt"],"roundness":{"type":2},"boundElements":[],"updated":1673393563879,"link":null,"locked":false,"startBinding":{"elementId":"0hRDdidg","focus":-0.07585820164313373,"gap":11.812885025632056},"endBinding":{"focus":0.21833418349062633,"gap":14.098597804565372,"elementId":"0hRDdidg"},"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[-10.570859372029787,5.047996387929032],[3.2857127789333163,10.931379070486201]]},{"type":"text","version":1641,"versionNonce":2081401162,"isDeleted":false,"id":"0hRDdidg","fillStyle":"hachure","strokeWidth":2,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-115.7461723801901,"y":57.189152461565186,"strokeColor":"#862e9c","backgroundColor":"transparent","width":5,"height":19,"seed":1107309270,"groupIds":["KaZYyii1iTZ8-nNvVM93q","Q6DyyDpRBzA7F5T9GJ9Nt"],"roundness":null,"boundElements":[{"id":"3bknPLUtZ6TwY8rTrR0l8","type":"arrow"},{"id":"Sz8xeGELrBil9xoaOIm_J","type":"arrow"}],"updated":1673393563325,"link":null,"locked":false,"fontSize":14.39868181190029,"fontFamily":1,"text":"1","rawText":"1","baseline":13,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"1"},{"type":"arrow","version":3597,"versionNonce":1785697494,"isDeleted":false,"id":"Q2Hvhj1OV0s49QWlaM0n-","fillStyle":"hachure","strokeWidth":2,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-98.93328735455805,"y":25.96932462421843,"strokeColor":"#862e9c","backgroundColor":"transparent","width":13.856572150963103,"height":10.931379070486201,"seed":1348429846,"groupIds":["v6ehIYzU_8UqNDHsXca7J","Q6DyyDpRBzA7F5T9GJ9Nt"],"roundness":{"type":2},"boundElements":[],"updated":1673393563879,"link":null,"locked":false,"startBinding":{"elementId":"FTpz62VY","focus":-0.07585820164313373,"gap":11.812885025632056},"endBinding":{"focus":0.21833418349062633,"gap":14.098597804565372,"elementId":"FTpz62VY"},"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[-10.570859372029787,5.047996387929032],[3.2857127789333163,10.931379070486201]]},{"type":"text","version":1693,"versionNonce":1780443722,"isDeleted":false,"id":"FTpz62VY","fillStyle":"hachure","strokeWidth":2,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-115.7461723801901,"y":22.493067748835344,"strokeColor":"#862e9c","backgroundColor":"transparent","width":5,"height":19,"seed":1336276310,"groupIds":["v6ehIYzU_8UqNDHsXca7J","Q6DyyDpRBzA7F5T9GJ9Nt"],"roundness":null,"boundElements":[{"id":"Q2Hvhj1OV0s49QWlaM0n-","type":"arrow"},{"id":"Sz8xeGELrBil9xoaOIm_J","type":"arrow"},{"id":"sGG3rEuEkggAAXmB2n6iz","type":"arrow"},{"id":"BLtrddpDIMI7sGaAGwKk-","type":"arrow"},{"id":"blo4yQwW9sP5B3XOH_GAR","type":"arrow"}],"updated":1673393769961,"link":null,"locked":false,"fontSize":14.39868181190029,"fontFamily":1,"text":"1","rawText":"1","baseline":13,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"1"},{"type":"arrow","version":3627,"versionNonce":1705069450,"isDeleted":false,"id":"N75qmV4NvdlD_1JMYiIBX","fillStyle":"hachure","strokeWidth":2,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-98.93328735455802,"y":-60.770887157606175,"strokeColor":"#862e9c","backgroundColor":"transparent","width":13.856572150963103,"height":10.931379070486201,"seed":1495849622,"groupIds":["vX8KgjJzzZ2_QFC87SDqb","Q6DyyDpRBzA7F5T9GJ9Nt"],"roundness":{"type":2},"boundElements":[],"updated":1673393563879,"link":null,"locked":false,"startBinding":{"elementId":"3l5Xdm3B","focus":-0.07585820164313568,"gap":11.812885025632085},"endBinding":{"focus":0.21833418349062633,"gap":14.098597804565372,"elementId":"3l5Xdm3B"},"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[-10.570859372029787,5.047996387929032],[3.2857127789333163,10.931379070486201]]},{"type":"text","version":1709,"versionNonce":977609994,"isDeleted":false,"id":"3l5Xdm3B","fillStyle":"hachure","strokeWidth":2,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-115.7461723801901,"y":-64.24714403298927,"strokeColor":"#862e9c","backgroundColor":"transparent","width":5,"height":19,"seed":329062358,"groupIds":["vX8KgjJzzZ2_QFC87SDqb","Q6DyyDpRBzA7F5T9GJ9Nt"],"roundness":null,"boundElements":[{"id":"N75qmV4NvdlD_1JMYiIBX","type":"arrow"},{"id":"itKSWnAAJjQpjm2vWnion","type":"arrow"},{"id":"BIlN-z6qp0Zwaqb-TssE9","type":"arrow"}],"updated":1673393676354,"link":null,"locked":false,"fontSize":14.39868181190029,"fontFamily":1,"text":"1","rawText":"1","baseline":13,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"1"},{"type":"arrow","version":1871,"versionNonce":1814377174,"isDeleted":false,"id":"blo4yQwW9sP5B3XOH_GAR","fillStyle":"hachure","strokeWidth":4,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-87.48453930066168,"y":43.731680938914444,"strokeColor":"#000000","backgroundColor":"transparent","width":7.8995303199405384,"height":30.439869508518036,"seed":1872603222,"groupIds":["GqIiQvxPWWtvjf3-ZGR_E"],"roundness":null,"boundElements":[],"updated":1673394096864,"link":null,"locked":false,"startBinding":{"elementId":"IrI6KQJV","focus":1.009884790854482,"gap":11.593242913942987},"endBinding":{"elementId":"IrI6KQJV","focus":-1.0448964730963926,"gap":10.185744027696614},"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"bar","points":[[0,0],[7.8995303199405384,14.881193954170492],[7.76902398725754,30.439869508518036]]}],"appState":{"theme":"dark","viewBackgroundColor":"transparent","currentItemStrokeColor":"#000000","currentItemBackgroundColor":"#12b886","currentItemFillStyle":"solid","currentItemStrokeWidth":4,"currentItemStrokeStyle":"solid","currentItemRoughness":0,"currentItemOpacity":100,"currentItemFontFamily":1,"currentItemFontSize":20,"currentItemTextAlign":"left","currentItemStartArrowhead":null,"currentItemEndArrowhead":"bar","scrollX":468.28845672986057,"scrollY":265.6950485882395,"zoom":{"value":2},"currentItemRoundness":"sharp","gridSize":null,"colorPalette":{}},"files":{}};InitialData.scrollToContent=true;App=()=>{const e=React.useRef(null),t=React.useRef(null),[n,i]=React.useState({width:void 0,height:void 0});return React.useEffect(()=>{i({width:t.current.getBoundingClientRect().width,height:t.current.getBoundingClientRect().height});const e=()=>{i({width:t.current.getBoundingClientRect().width,height:t.current.getBoundingClientRect().height})};return window.addEventListener("resize",e),()=>window.removeEventListener("resize",e)},[t]),React.createElement(React.Fragment,null,React.createElement("div",{className:"excalidraw-wrapper",ref:t},React.createElement(ExcalidrawLib.Excalidraw,{ref:e,width:n.width,height:n.height,initialData:InitialData,viewModeEnabled:!0,zenModeEnabled:!0,gridModeEnabled:!1})))},excalidrawWrapper=document.getElementById("HatlightFalllingInSteps.excalidraw.md3");ReactDOM.render(React.createElement(App),excalidrawWrapper);})();</script>

Instead we want to change y in small steps as in the right. 

### Define the Change Y by Yspeed in Steps Myblock

Our first task is to make each __small step__ repeat *y-speed times*. Later we will make it stop.  
So, the first part is:
- __Small step__: change y by 1 step each time --  each small step is __down__ so we change y by  __-1__.
- Repeat this `y speed` times

In code it would look like this (EXAMPLE 1): 

```ad-scratch
title: EXAMPLE 1
~~~scratchblock
define change y by (y speed) in steps. Stop at wall.::custom
repeat (y speed)
    change y by (-1)
end
~~~
```

This has 2 problems:

#### Problem 1: Works Only if We Are Falling

Notice that this only works if we are falling (`y speed` < 0), because y is going down. Later we will fix this so that it works even if we are moving up, in other words jumping. But remember to imagine that `y speed` could be > 0.

#### Problem 2: Repeat Blocks Only Take Positive Numbers

If I tell you to jump -3 times, you would be right to be puzzled. That's impossible, right?

The number of times something repeats cannot be a number *less than* than 0 (-__negative__), like -1, -2, -3, ….It has to be __positive__ (or zero).

We say it has to have a __sign of +1__.

But, when the sprite is __falling__, the variable `y speed`  __is__ less than zero (it is -__negative__). It is like -1, -2, -3… It has a __sign of -1__.

To use it as the number of times to repeat in a repeat block, that -__negative__ number has to be made +__positive__.

#### Absolute Value to the Rescue

Luckily, in Scratch there is something that can help us, called __abs__, which is short for __absolute value__: 

```ad-scratch
title: abs block
~~~scratchblock
[abs v] of (y speed)
~~~
```

__Abs__ does exactly what we want. It keeps a +positive number positive, but changes a -negative to a +positive. 

So EXAMPLE 1 should be:

```ad-scratch
title: EXAMPLE 2
~~~scratchblock
repeat ([abs v] of (y speed))
    change y by (-1)
end
~~~
```

#### Stopping if We Touch a Wall

That's pretty good. But, we also want to stop if we are touching a wall. We only want to change y by -1 __IF__ we are __not touching a wall__. In code that means:

```ad-scratch
title: Htibox, define change y
~~~scratchblock

define change y  by (speed)  in steps. stop at wall.
repeat ([abs v] of (speed::custom)::operators)
    if <not <touching [walls v]?>> then
    change y by (-1)
    end
end
~~~
```

(There is a way to do this in one line.[^2])

How does this work? What happens when we hit a wall when falling? If we change y and we enter a wall, the next time we repeat, the change y doesn't change y, and were are just left inside the wall. That's important: we are **inside the wall** when we stop. We have to **pull out** of the wall.

### Define the Pull Out if Touching Wall Myblock

Here is the pull out if touching wall myblock. Note that instead of an input field it has a boolean field with pointy edges: <>. Boolean fields just accept sensing and other logic blocks, not variables and expressions.

```ad-scratch
title: hitbox, pull up definition
~~~scratchblock
define pull out if touching wall and <falling?> or not
~~~
```

How *do* we pull out? If we are touching a wall, we have to do two things, __in this order__:  

1) Set `y speed` to zero. (This is realistic. When you fall, the ground absorbs your speed. You stop moving.)[^3]
2) Pull out of the wall  

<div id="pullUp1excalidraw.md4"></div><script>(function(){const InitialData={"type":"excalidraw","version":2,"source":"https://excalidraw.com","elements":[{"type":"rectangle","version":496,"versionNonce":253122377,"isDeleted":false,"id":"kX6mdJgu6Z9zYzt4QkKQC","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":0,"opacity":90,"angle":0,"x":-309.1316215319511,"y":-323.43956521841193,"strokeColor":"#000000","backgroundColor":"#15aabf","width":580.8837890625,"height":409.2378845214844,"seed":524826683,"groupIds":[],"strokeSharpness":"sharp","boundElements":[],"updated":1671583808422,"link":null,"locked":false},{"type":"rectangle","version":366,"versionNonce":1186153193,"isDeleted":false,"id":"btiQUpFtBA806yPFVw0O4","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-308.62730916341144,"y":-141.68146946119225,"strokeColor":"#000000","backgroundColor":"#fa5252","width":578.7227783203125,"height":52.170654296875,"seed":44219637,"groupIds":[],"strokeSharpness":"round","boundElements":[{"id":"UcskjoFCvHzCqT3uSCxMh","type":"arrow"}],"updated":1671583791523,"link":null,"locked":false},{"type":"rectangle","version":617,"versionNonce":591756327,"isDeleted":false,"id":"h2uqRkhOXHx654X-XRb_Z","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-262.0369364420573,"y":-183.8746464573324,"strokeColor":"#000000","backgroundColor":"#4c6ef5","width":57.265625,"height":54.74920654296875,"seed":2074835163,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1671583791523,"link":null,"locked":false},{"type":"arrow","version":338,"versionNonce":989658569,"isDeleted":false,"id":"f8Uzi4SwRvBu9EFRjHf0t","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-155.02411891657368,"y":-168.93575815054083,"strokeColor":"#000000","backgroundColor":"transparent","width":0,"height":59.370208740234375,"seed":231274421,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1671583791523,"link":null,"locked":false,"startBinding":{"elementId":"QwswnlTb","focus":0.132333157240707,"gap":4.791787652533429},"endBinding":null,"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[0,59.370208740234375]]},{"type":"text","version":85,"versionNonce":1035034439,"isDeleted":false,"id":"QwswnlTb","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-192.4592895507813,"y":-198.72754580307426,"strokeColor":"#000000","backgroundColor":"transparent","width":76,"height":25,"seed":104294235,"groupIds":[],"strokeSharpness":"sharp","boundElements":[{"id":"f8Uzi4SwRvBu9EFRjHf0t","type":"arrow"}],"updated":1671583791523,"link":null,"locked":false,"fontSize":20,"fontFamily":1,"text":"speed y","rawText":"speed y","baseline":18,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"speed y"},{"type":"rectangle","version":727,"versionNonce":940334249,"isDeleted":false,"id":"7ROID8RLUbPYdA3Pg-am9","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-107.46558125813806,"y":-183.8746464573324,"strokeColor":"#000000","backgroundColor":"#4c6ef5","width":57.265625,"height":54.74920654296875,"seed":2113005077,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1671583791523,"link":null,"locked":false},{"type":"text","version":198,"versionNonce":1660149351,"isDeleted":false,"id":"ZpKNmGDT","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-37.9922888340094,"y":-199.14230825111613,"strokeColor":"#000000","backgroundColor":"transparent","width":76,"height":25,"seed":1465277301,"groupIds":[],"strokeSharpness":"sharp","boundElements":[],"updated":1671583791523,"link":null,"locked":false,"fontSize":20,"fontFamily":1,"text":"speed y","rawText":"speed y","baseline":18,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"speed y"},{"type":"text","version":40,"versionNonce":1569513353,"isDeleted":false,"id":"rQd7o4Mi","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-7.9922888340094005,"y":-167.28807961673064,"strokeColor":"#000000","backgroundColor":"transparent","width":16,"height":25,"seed":1635862747,"groupIds":[],"strokeSharpness":"sharp","boundElements":[],"updated":1671583791523,"link":null,"locked":false,"fontSize":20,"fontFamily":1,"text":"0","rawText":"0","baseline":18,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"0"},{"type":"rectangle","version":957,"versionNonce":903444871,"isDeleted":false,"id":"vEIBqNI4qxu5-18LGiWQE","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":80.32943921211427,"y":-200.77953222584304,"strokeColor":"#000000","backgroundColor":"#4c6ef5","width":57.265625,"height":54.74920654296875,"seed":1920351419,"groupIds":[],"strokeSharpness":"round","boundElements":[{"id":"UcskjoFCvHzCqT3uSCxMh","type":"arrow"}],"updated":1671583791523,"link":null,"locked":false},{"type":"text","version":275,"versionNonce":1236928105,"isDeleted":false,"id":"vSFzy3VC","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":156.79945412660248,"y":-198.9336149668613,"strokeColor":"#000000","backgroundColor":"transparent","width":76,"height":25,"seed":487731541,"groupIds":[],"strokeSharpness":"sharp","boundElements":[],"updated":1671583791523,"link":null,"locked":false,"fontSize":20,"fontFamily":1,"text":"speed y","rawText":"speed y","baseline":18,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"speed y"},{"type":"text","version":119,"versionNonce":1268691111,"isDeleted":false,"id":"RhLxkizO","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":186.79945412660248,"y":-171.39498859204417,"strokeColor":"#000000","backgroundColor":"transparent","width":16,"height":25,"seed":425982587,"groupIds":[],"strokeSharpness":"sharp","boundElements":[],"updated":1671583791523,"link":null,"locked":false,"fontSize":20,"fontFamily":1,"text":"0","rawText":"0","baseline":18,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"0"},{"type":"arrow","version":1019,"versionNonce":1197429065,"isDeleted":false,"id":"UcskjoFCvHzCqT3uSCxMh","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":112.02164244040449,"y":-119.58971927142812,"strokeColor":"#000000","backgroundColor":"transparent","width":28.716396233974365,"height":21.483466515174285,"seed":1512917051,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1671583791523,"link":null,"locked":false,"startBinding":null,"endBinding":{"elementId":"vEIBqNI4qxu5-18LGiWQE","focus":0.8157109159252531,"gap":4.957139896271883},"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[28.716396233974365,-12.348799485426696],[2.3998008391852466,-21.483466515174285]]},{"type":"text","version":111,"versionNonce":1576010695,"isDeleted":false,"id":"t43ZZ7QC","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":72.21938539162653,"y":-233.3396355437138,"strokeColor":"#000000","backgroundColor":"transparent","width":78,"height":25,"seed":1768232251,"groupIds":[],"strokeSharpness":"sharp","boundElements":[],"updated":1671583791523,"link":null,"locked":false,"fontSize":20,"fontFamily":1,"text":"pull out","rawText":"pull out","baseline":18,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"pull out"},{"id":"jyLgLtbQ","type":"text","x":-83.93130414913861,"y":-304.96635202261115,"width":12,"height":46,"angle":0,"strokeColor":"#000000","backgroundColor":"transparent","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"groupIds":[],"strokeSharpness":"sharp","seed":862883625,"version":85,"versionNonce":513663335,"isDeleted":false,"boundElements":null,"updated":1671583821521,"link":null,"locked":false,"text":"1","rawText":"1","fontSize":36,"fontFamily":1,"textAlign":"center","verticalAlign":"top","baseline":32,"containerId":null,"originalText":"1"},{"type":"text","version":134,"versionNonce":196643977,"isDeleted":false,"id":"s8tzDwiJ","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":88.80050737429889,"y":-304.96635202261115,"strokeColor":"#000000","backgroundColor":"transparent","width":28,"height":46,"seed":1933288297,"groupIds":[],"strokeSharpness":"sharp","boundElements":null,"updated":1671583821522,"link":null,"locked":false,"fontSize":36,"fontFamily":1,"text":"2","rawText":"2","baseline":32,"textAlign":"center","verticalAlign":"top","containerId":null,"originalText":"2"},{"id":"NaF8tHwV","type":"text","x":90.61441118289264,"y":-270.11586526724005,"width":16,"height":25,"angle":0,"strokeColor":"#000000","backgroundColor":"transparent","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"groupIds":[],"strokeSharpness":"sharp","seed":1296904873,"version":8,"versionNonce":1021965031,"isDeleted":true,"boundElements":null,"updated":1671583791523,"link":null,"locked":false,"text":"2","rawText":"2","fontSize":20,"fontFamily":1,"textAlign":"left","verticalAlign":"top","baseline":18,"containerId":null,"originalText":"2"}],"appState":{"theme":"dark","viewBackgroundColor":"transparent","currentItemStrokeColor":"#000000","currentItemBackgroundColor":"transparent","currentItemFillStyle":"hachure","currentItemStrokeWidth":1,"currentItemStrokeStyle":"solid","currentItemRoughness":1,"currentItemOpacity":100,"currentItemFontFamily":1,"currentItemFontSize":36,"currentItemTextAlign":"center","currentItemStrokeSharpness":"sharp","currentItemStartArrowhead":null,"currentItemEndArrowhead":"arrow","scrollX":371.96530073116986,"scrollY":370.1031852135291,"zoom":{"value":2},"currentItemLinearStrokeSharpness":"round","gridSize":null,"colorPalette":{}},"files":{}};InitialData.scrollToContent=true;App=()=>{const e=React.useRef(null),t=React.useRef(null),[n,i]=React.useState({width:void 0,height:void 0});return React.useEffect(()=>{i({width:t.current.getBoundingClientRect().width,height:t.current.getBoundingClientRect().height});const e=()=>{i({width:t.current.getBoundingClientRect().width,height:t.current.getBoundingClientRect().height})};return window.addEventListener("resize",e),()=>window.removeEventListener("resize",e)},[t]),React.createElement(React.Fragment,null,React.createElement("div",{className:"excalidraw-wrapper",ref:t},React.createElement(ExcalidrawLib.Excalidraw,{ref:e,width:n.width,height:n.height,initialData:InitialData,viewModeEnabled:!0,zenModeEnabled:!0,gridModeEnabled:!1})))},excalidrawWrapper=document.getElementById("pullUp1excalidraw.md4");ReactDOM.render(React.createElement(App),excalidrawWrapper);})();</script>

Here is the code:  
1) Set y-speed to zero so we are touching a wall. We can use an if block:

```ad-scratch
title: Htibox, pull up definition
~~~scratchblock
define pull out if touching wall and <falling?> or not
if <touching [walls v]> then
set [y speed v] to (0)
end
...
~~~
```

One line version in footnote[^4]

&nbsp;  
The next step is:  
2. We __Pull out__ by +1 to cancel the last step, the one that landed in the wall. (remember that at this point we are still only looking at the case when we are falling, not jumping.) We only want to do this if we are touching the wall, __and__ if we are falling. 
- Notice that in the `receive fall` stack we called this myblock with an input of `y speed < 0` (this is true when we are falling, and false when we are not):

```ad-scratch
title:
~~~scratchblock
when I receive [fall v]
...
pull out if touching wall and <(y speed) \< [0]> or not::custom
...
~~~
```

- We send the value of  `y speed < 0 ` into the boolean called <__falling?__> in the myblock definition. 

```ad-scratch
~~~scratchblock
define pull out if touching wall and <falling?> or not
...
~~~
```

   - <`falling?`> is true if we are falling, but  false if we are not falling. 
  - Drag the <`falling?`> boolean from the definition into the `change y` block. HUHN? How can I do that? The change y block expects a number, but <`falling?`> is a boolean! Well, guess what? Scratch will change <`falling?`> into a __zero__ or __1__!!!

```ad-tip
This is how booleans work. If the condition is true, the boolean actually takes the value `true`, but Scratch "knows" to make this into a **1** if we try to use it like a number. If the boolean is `false`, Scratch makes it **zero** for us if we try to use it as a number.
```

- Therefore, this will change y __only if__ we are __both__ *touching the wall* __and__ *falling*:

```ad-scratch
title: hitbox, pull up definition
~~~scratchblock
define pull out if touching wall and <falling?> or not
if <touching [walls v]> then
set [y speed v] to (0)
change y by <falling?::custom>
end
~~~
```

- <`falling?`> will be __0__ if we are going up, and this block won't change y, which is good (for now).
- It only pulls out (up) if we are falling and touching the wall.

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

One line version of the pull out routine is in the footnotes [^5]

Here is the diagram again. After we pull out, the speed is __0__, which means we stop falling, as we should. This is realistic. When you hit the ground, you stop moving. When we are done we are sitting on the ground and not moving, just as you would be when you land on the ground from falling.

<div id="pullUp1excalidraw.md5"></div><script>(function(){const InitialData={"type":"excalidraw","version":2,"source":"https://excalidraw.com","elements":[{"type":"rectangle","version":496,"versionNonce":253122377,"isDeleted":false,"id":"kX6mdJgu6Z9zYzt4QkKQC","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":0,"opacity":90,"angle":0,"x":-309.1316215319511,"y":-323.43956521841193,"strokeColor":"#000000","backgroundColor":"#15aabf","width":580.8837890625,"height":409.2378845214844,"seed":524826683,"groupIds":[],"strokeSharpness":"sharp","boundElements":[],"updated":1671583808422,"link":null,"locked":false},{"type":"rectangle","version":366,"versionNonce":1186153193,"isDeleted":false,"id":"btiQUpFtBA806yPFVw0O4","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-308.62730916341144,"y":-141.68146946119225,"strokeColor":"#000000","backgroundColor":"#fa5252","width":578.7227783203125,"height":52.170654296875,"seed":44219637,"groupIds":[],"strokeSharpness":"round","boundElements":[{"id":"UcskjoFCvHzCqT3uSCxMh","type":"arrow"}],"updated":1671583791523,"link":null,"locked":false},{"type":"rectangle","version":617,"versionNonce":591756327,"isDeleted":false,"id":"h2uqRkhOXHx654X-XRb_Z","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-262.0369364420573,"y":-183.8746464573324,"strokeColor":"#000000","backgroundColor":"#4c6ef5","width":57.265625,"height":54.74920654296875,"seed":2074835163,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1671583791523,"link":null,"locked":false},{"type":"arrow","version":338,"versionNonce":989658569,"isDeleted":false,"id":"f8Uzi4SwRvBu9EFRjHf0t","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-155.02411891657368,"y":-168.93575815054083,"strokeColor":"#000000","backgroundColor":"transparent","width":0,"height":59.370208740234375,"seed":231274421,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1671583791523,"link":null,"locked":false,"startBinding":{"elementId":"QwswnlTb","focus":0.132333157240707,"gap":4.791787652533429},"endBinding":null,"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[0,59.370208740234375]]},{"type":"text","version":85,"versionNonce":1035034439,"isDeleted":false,"id":"QwswnlTb","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-192.4592895507813,"y":-198.72754580307426,"strokeColor":"#000000","backgroundColor":"transparent","width":76,"height":25,"seed":104294235,"groupIds":[],"strokeSharpness":"sharp","boundElements":[{"id":"f8Uzi4SwRvBu9EFRjHf0t","type":"arrow"}],"updated":1671583791523,"link":null,"locked":false,"fontSize":20,"fontFamily":1,"text":"speed y","rawText":"speed y","baseline":18,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"speed y"},{"type":"rectangle","version":727,"versionNonce":940334249,"isDeleted":false,"id":"7ROID8RLUbPYdA3Pg-am9","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-107.46558125813806,"y":-183.8746464573324,"strokeColor":"#000000","backgroundColor":"#4c6ef5","width":57.265625,"height":54.74920654296875,"seed":2113005077,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1671583791523,"link":null,"locked":false},{"type":"text","version":198,"versionNonce":1660149351,"isDeleted":false,"id":"ZpKNmGDT","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-37.9922888340094,"y":-199.14230825111613,"strokeColor":"#000000","backgroundColor":"transparent","width":76,"height":25,"seed":1465277301,"groupIds":[],"strokeSharpness":"sharp","boundElements":[],"updated":1671583791523,"link":null,"locked":false,"fontSize":20,"fontFamily":1,"text":"speed y","rawText":"speed y","baseline":18,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"speed y"},{"type":"text","version":40,"versionNonce":1569513353,"isDeleted":false,"id":"rQd7o4Mi","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-7.9922888340094005,"y":-167.28807961673064,"strokeColor":"#000000","backgroundColor":"transparent","width":16,"height":25,"seed":1635862747,"groupIds":[],"strokeSharpness":"sharp","boundElements":[],"updated":1671583791523,"link":null,"locked":false,"fontSize":20,"fontFamily":1,"text":"0","rawText":"0","baseline":18,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"0"},{"type":"rectangle","version":957,"versionNonce":903444871,"isDeleted":false,"id":"vEIBqNI4qxu5-18LGiWQE","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":80.32943921211427,"y":-200.77953222584304,"strokeColor":"#000000","backgroundColor":"#4c6ef5","width":57.265625,"height":54.74920654296875,"seed":1920351419,"groupIds":[],"strokeSharpness":"round","boundElements":[{"id":"UcskjoFCvHzCqT3uSCxMh","type":"arrow"}],"updated":1671583791523,"link":null,"locked":false},{"type":"text","version":275,"versionNonce":1236928105,"isDeleted":false,"id":"vSFzy3VC","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":156.79945412660248,"y":-198.9336149668613,"strokeColor":"#000000","backgroundColor":"transparent","width":76,"height":25,"seed":487731541,"groupIds":[],"strokeSharpness":"sharp","boundElements":[],"updated":1671583791523,"link":null,"locked":false,"fontSize":20,"fontFamily":1,"text":"speed y","rawText":"speed y","baseline":18,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"speed y"},{"type":"text","version":119,"versionNonce":1268691111,"isDeleted":false,"id":"RhLxkizO","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":186.79945412660248,"y":-171.39498859204417,"strokeColor":"#000000","backgroundColor":"transparent","width":16,"height":25,"seed":425982587,"groupIds":[],"strokeSharpness":"sharp","boundElements":[],"updated":1671583791523,"link":null,"locked":false,"fontSize":20,"fontFamily":1,"text":"0","rawText":"0","baseline":18,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"0"},{"type":"arrow","version":1019,"versionNonce":1197429065,"isDeleted":false,"id":"UcskjoFCvHzCqT3uSCxMh","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":112.02164244040449,"y":-119.58971927142812,"strokeColor":"#000000","backgroundColor":"transparent","width":28.716396233974365,"height":21.483466515174285,"seed":1512917051,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1671583791523,"link":null,"locked":false,"startBinding":null,"endBinding":{"elementId":"vEIBqNI4qxu5-18LGiWQE","focus":0.8157109159252531,"gap":4.957139896271883},"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[28.716396233974365,-12.348799485426696],[2.3998008391852466,-21.483466515174285]]},{"type":"text","version":111,"versionNonce":1576010695,"isDeleted":false,"id":"t43ZZ7QC","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":72.21938539162653,"y":-233.3396355437138,"strokeColor":"#000000","backgroundColor":"transparent","width":78,"height":25,"seed":1768232251,"groupIds":[],"strokeSharpness":"sharp","boundElements":[],"updated":1671583791523,"link":null,"locked":false,"fontSize":20,"fontFamily":1,"text":"pull out","rawText":"pull out","baseline":18,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"pull out"},{"id":"jyLgLtbQ","type":"text","x":-83.93130414913861,"y":-304.96635202261115,"width":12,"height":46,"angle":0,"strokeColor":"#000000","backgroundColor":"transparent","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"groupIds":[],"strokeSharpness":"sharp","seed":862883625,"version":85,"versionNonce":513663335,"isDeleted":false,"boundElements":null,"updated":1671583821521,"link":null,"locked":false,"text":"1","rawText":"1","fontSize":36,"fontFamily":1,"textAlign":"center","verticalAlign":"top","baseline":32,"containerId":null,"originalText":"1"},{"type":"text","version":134,"versionNonce":196643977,"isDeleted":false,"id":"s8tzDwiJ","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":88.80050737429889,"y":-304.96635202261115,"strokeColor":"#000000","backgroundColor":"transparent","width":28,"height":46,"seed":1933288297,"groupIds":[],"strokeSharpness":"sharp","boundElements":null,"updated":1671583821522,"link":null,"locked":false,"fontSize":36,"fontFamily":1,"text":"2","rawText":"2","baseline":32,"textAlign":"center","verticalAlign":"top","containerId":null,"originalText":"2"},{"id":"NaF8tHwV","type":"text","x":90.61441118289264,"y":-270.11586526724005,"width":16,"height":25,"angle":0,"strokeColor":"#000000","backgroundColor":"transparent","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"groupIds":[],"strokeSharpness":"sharp","seed":1296904873,"version":8,"versionNonce":1021965031,"isDeleted":true,"boundElements":null,"updated":1671583791523,"link":null,"locked":false,"text":"2","rawText":"2","fontSize":20,"fontFamily":1,"textAlign":"left","verticalAlign":"top","baseline":18,"containerId":null,"originalText":"2"}],"appState":{"theme":"dark","viewBackgroundColor":"transparent","currentItemStrokeColor":"#000000","currentItemBackgroundColor":"transparent","currentItemFillStyle":"hachure","currentItemStrokeWidth":1,"currentItemStrokeStyle":"solid","currentItemRoughness":1,"currentItemOpacity":100,"currentItemFontFamily":1,"currentItemFontSize":36,"currentItemTextAlign":"center","currentItemStrokeSharpness":"sharp","currentItemStartArrowhead":null,"currentItemEndArrowhead":"arrow","scrollX":371.96530073116986,"scrollY":370.1031852135291,"zoom":{"value":2},"currentItemLinearStrokeSharpness":"round","gridSize":null,"colorPalette":{}},"files":{}};InitialData.scrollToContent=true;App=()=>{const e=React.useRef(null),t=React.useRef(null),[n,i]=React.useState({width:void 0,height:void 0});return React.useEffect(()=>{i({width:t.current.getBoundingClientRect().width,height:t.current.getBoundingClientRect().height});const e=()=>{i({width:t.current.getBoundingClientRect().width,height:t.current.getBoundingClientRect().height})};return window.addEventListener("resize",e),()=>window.removeEventListener("resize",e)},[t]),React.createElement(React.Fragment,null,React.createElement("div",{className:"excalidraw-wrapper",ref:t},React.createElement(ExcalidrawLib.Excalidraw,{ref:e,width:n.width,height:n.height,initialData:InitialData,viewModeEnabled:!0,zenModeEnabled:!0,gridModeEnabled:!1})))},excalidrawWrapper=document.getElementById("pullUp1excalidraw.md5");ReactDOM.render(React.createElement(App),excalidrawWrapper);})();</script>

Note that __order__ is important! If instead we `change y` first and then change the speed…

```ad-scratch
~~~scratchblock
define pull out if touching wall and <falling?> or not
   if <touching [walls v]> then
       change y by <falling?::custom>
       set [y speed v] to (0)
   end
~~~
```

…after the first step we are not touching the wall, but…  
<div id="pullUp2excalidraw.md6"></div><script>(function(){const InitialData={"type":"excalidraw","version":2,"source":"https://excalidraw.com","elements":[{"type":"rectangle","version":465,"versionNonce":1263438855,"isDeleted":false,"id":"kX6mdJgu6Z9zYzt4QkKQC","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":0,"opacity":90,"angle":0,"x":-308.8126241942463,"y":-326.73251471327336,"strokeColor":"#000000","backgroundColor":"#15aabf","width":580.8837890625,"height":409.2378845214844,"seed":524826683,"groupIds":[],"strokeSharpness":"sharp","boundElements":[],"updated":1671583942867,"link":null,"locked":false},{"type":"rectangle","version":345,"versionNonce":822348359,"isDeleted":false,"id":"btiQUpFtBA806yPFVw0O4","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-309.00035603841144,"y":-141.91882501132244,"strokeColor":"#000000","backgroundColor":"#fa5252","width":578.7227783203125,"height":52.170654296875,"seed":44219637,"groupIds":[],"strokeSharpness":"round","boundElements":[{"id":"UcskjoFCvHzCqT3uSCxMh","type":"arrow"}],"updated":1671583913022,"link":null,"locked":false},{"type":"rectangle","version":614,"versionNonce":1489887657,"isDeleted":false,"id":"h2uqRkhOXHx654X-XRb_Z","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-261.6880943661644,"y":-184.1071904026449,"strokeColor":"#000000","backgroundColor":"#4c6ef5","width":57.265625,"height":54.74920654296875,"seed":2074835163,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1671583913022,"link":null,"locked":false},{"type":"arrow","version":291,"versionNonce":1287203175,"isDeleted":false,"id":"f8Uzi4SwRvBu9EFRjHf0t","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-154.18271270952195,"y":-166.59826983046526,"strokeColor":"#000000","backgroundColor":"transparent","width":1.675567626953125,"height":59.69586181640625,"seed":231274421,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1671583913022,"link":null,"locked":false,"startBinding":{"elementId":"QwswnlTb","focus":0.0007407326464248657,"gap":7.324716967445852},"endBinding":null,"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[-1.675567626953125,59.69586181640625]]},{"type":"text","version":82,"versionNonce":1440072841,"isDeleted":false,"id":"QwswnlTb","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-192.4592895507813,"y":-194.98466872318392,"strokeColor":"#000000","backgroundColor":"transparent","width":76,"height":25,"seed":104294235,"groupIds":[],"strokeSharpness":"sharp","boundElements":[{"id":"f8Uzi4SwRvBu9EFRjHf0t","type":"arrow"}],"updated":1671583913022,"link":null,"locked":false,"fontSize":20,"fontFamily":1,"text":"speed y","rawText":"speed y","baseline":18,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"speed y"},{"type":"rectangle","version":972,"versionNonce":1857905799,"isDeleted":false,"id":"vEIBqNI4qxu5-18LGiWQE","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-96.94336759127094,"y":-210.0129713534471,"strokeColor":"#000000","backgroundColor":"#4c6ef5","width":57.265625,"height":54.74920654296875,"seed":1920351419,"groupIds":[],"strokeSharpness":"round","boundElements":[{"id":"UcskjoFCvHzCqT3uSCxMh","type":"arrow"}],"updated":1671583913022,"link":null,"locked":false},{"type":"text","version":430,"versionNonce":1906199401,"isDeleted":false,"id":"vSFzy3VC","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-19.22992122216982,"y":-195.1009494151482,"strokeColor":"#000000","backgroundColor":"transparent","width":76,"height":25,"seed":487731541,"groupIds":[],"strokeSharpness":"sharp","boundElements":[{"id":"44dLB82oMVXvMA_wzfLOo","type":"arrow"}],"updated":1671583913022,"link":null,"locked":false,"fontSize":20,"fontFamily":1,"text":"speed y","rawText":"speed y","baseline":18,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"speed y"},{"type":"arrow","version":694,"versionNonce":919419815,"isDeleted":false,"id":"UcskjoFCvHzCqT3uSCxMh","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-61.70821595803301,"y":-124.68474592344634,"strokeColor":"#000000","backgroundColor":"transparent","width":27.456711088338537,"height":29.57901888703202,"seed":1512917051,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1671583913022,"link":null,"locked":false,"startBinding":null,"endBinding":{"elementId":"vEIBqNI4qxu5-18LGiWQE","focus":0.6448389025672585,"gap":1},"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[19.660488030849365,-12.53169133112982],[-7.796223057489172,-29.57901888703202]]},{"type":"text","version":267,"versionNonce":1416820297,"isDeleted":false,"id":"t43ZZ7QC","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-97.2557122646233,"y":-240.13332145679968,"strokeColor":"#000000","backgroundColor":"transparent","width":78,"height":25,"seed":1768232251,"groupIds":[],"strokeSharpness":"sharp","boundElements":[],"updated":1671583913022,"link":null,"locked":false,"fontSize":20,"fontFamily":1,"text":"pull out","rawText":"pull out","baseline":18,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"pull out"},{"type":"arrow","version":344,"versionNonce":420818631,"isDeleted":false,"id":"44dLB82oMVXvMA_wzfLOo","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":19.39937745528882,"y":-166.42398015550145,"strokeColor":"#000000","backgroundColor":"transparent","width":1.675567626953125,"height":59.69586181640625,"seed":1066318587,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1671583913022,"link":null,"locked":false,"startBinding":{"elementId":"vSFzy3VC","focus":0.2655967455293468,"gap":3.6769692596467394},"endBinding":null,"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[-1.675567626953125,59.69586181640625]]},{"type":"rectangle","version":1017,"versionNonce":288310569,"isDeleted":false,"id":"szdJ8c_tnKgqDPAvWjN_v","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":113.65481514284465,"y":-209.50058983883142,"strokeColor":"#000000","backgroundColor":"#4c6ef5","width":57.265625,"height":54.74920654296875,"seed":1140882325,"groupIds":[],"strokeSharpness":"round","boundElements":[{"id":"UcskjoFCvHzCqT3uSCxMh","type":"arrow"}],"updated":1671583913022,"link":null,"locked":false},{"type":"text","version":496,"versionNonce":1345437159,"isDeleted":false,"id":"Ayia79E8","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":181.8590562142732,"y":-195.59811639108779,"strokeColor":"#000000","backgroundColor":"transparent","width":76,"height":25,"seed":162400853,"groupIds":[],"strokeSharpness":"sharp","boundElements":[{"id":"RSHGkcLSqwCNXqkXrhEHI","type":"arrow"}],"updated":1671583913022,"link":null,"locked":false,"fontSize":20,"fontFamily":1,"text":"speed y","rawText":"speed y","baseline":18,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"speed y"},{"type":"arrow","version":491,"versionNonce":1396619273,"isDeleted":false,"id":"RSHGkcLSqwCNXqkXrhEHI","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":220.48835489173186,"y":-166.92114713144105,"strokeColor":"#000000","backgroundColor":"transparent","width":1.675567626953125,"height":59.69586181640625,"seed":936259963,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1671583913022,"link":null,"locked":false,"startBinding":{"elementId":"Ayia79E8","focus":-0.028248663575349633,"gap":3.6769692596467394},"endBinding":null,"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[-1.675567626953125,59.69586181640625]]},{"type":"text","version":344,"versionNonce":409444201,"isDeleted":false,"id":"CSBAxIxD","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":53.66138078179557,"y":-251.57203714732907,"strokeColor":"#000000","backgroundColor":"transparent","width":191,"height":34,"seed":1454111797,"groupIds":[],"strokeSharpness":"sharp","boundElements":[],"updated":1671583968909,"link":null,"locked":false,"fontSize":13.73906214745037,"fontFamily":1,"text":"Am I still falling,\nor did I just get pulled up?","rawText":"Am I still falling,\nor did I just get pulled up?","baseline":29,"textAlign":"center","verticalAlign":"top","containerId":null,"originalText":"Am I still falling,\nor did I just get pulled up?"},{"type":"text","version":42,"versionNonce":1285345001,"isDeleted":false,"id":"Uar1UP7f","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-85.16984155675857,"y":-298.9922650794843,"strokeColor":"#000000","backgroundColor":"transparent","width":22,"height":46,"seed":1877480297,"groupIds":[],"strokeSharpness":"sharp","boundElements":null,"updated":1671583913022,"link":null,"locked":false,"fontSize":36,"fontFamily":1,"text":"1'","rawText":"1'","baseline":32,"textAlign":"center","verticalAlign":"top","containerId":null,"originalText":"1'"},{"type":"text","version":87,"versionNonce":1348531561,"isDeleted":false,"id":"hEhjmg0x","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":119.7083017537883,"y":-299.2436994056562,"strokeColor":"#000000","backgroundColor":"transparent","width":37,"height":46,"seed":337617257,"groupIds":[],"strokeSharpness":"sharp","boundElements":null,"updated":1671583930047,"link":null,"locked":false,"fontSize":36,"fontFamily":1,"text":"2'","rawText":"2'","baseline":32,"textAlign":"center","verticalAlign":"top","containerId":null,"originalText":"2'"}],"appState":{"theme":"dark","viewBackgroundColor":"transparent","currentItemStrokeColor":"#000000","currentItemBackgroundColor":"transparent","currentItemFillStyle":"hachure","currentItemStrokeWidth":1,"currentItemStrokeStyle":"solid","currentItemRoughness":1,"currentItemOpacity":100,"currentItemFontFamily":1,"currentItemFontSize":20,"currentItemTextAlign":"center","currentItemStrokeSharpness":"sharp","currentItemStartArrowhead":null,"currentItemEndArrowhead":"arrow","scrollX":371.0520742227742,"scrollY":373.12396368788274,"zoom":{"value":2},"currentItemLinearStrokeSharpness":"round","gridSize":null,"colorPalette":{}},"files":{}};InitialData.scrollToContent=true;App=()=>{const e=React.useRef(null),t=React.useRef(null),[n,i]=React.useState({width:void 0,height:void 0});return React.useEffect(()=>{i({width:t.current.getBoundingClientRect().width,height:t.current.getBoundingClientRect().height});const e=()=>{i({width:t.current.getBoundingClientRect().width,height:t.current.getBoundingClientRect().height})};return window.addEventListener("resize",e),()=>window.removeEventListener("resize",e)},[t]),React.createElement(React.Fragment,null,React.createElement("div",{className:"excalidraw-wrapper",ref:t},React.createElement(ExcalidrawLib.Excalidraw,{ref:e,width:n.width,height:n.height,initialData:InitialData,viewModeEnabled:!0,zenModeEnabled:!0,gridModeEnabled:!1})))},excalidrawWrapper=document.getElementById("pullUp2excalidraw.md6");ReactDOM.render(React.createElement(App),excalidrawWrapper);})();</script>

…we are still going down. We are kind of back where we started, in the air and falling. But, we don't know if we touched a wall to get here or whether we were just falling, so *we can't know if we should change `y speed` to zero here yet or not*. Try it and you will see that it won't work.


## Testing Jumps

Okay, so we are done with Part 1 of our Torchlight Platformer. But let's test it. 

To test out jumping, we use a simple when up arrow key pressed stack to change y. The second line lets us keep pressing the  up arrow as long as we are moving slowly (in either direction). You might have to adjust the numbers if they are too large or small.

```ad-scratch
title: hitbox, jumping test
~~~scratchblock
when [up arrow v] key pressed
change y by (50)
wait until < ([abs v] of (y speed))  < (8) >
~~~
```

This works okay but not perfectly. For example, it doesn't work if we hit a platform from below. You can put a platform in your wall and see what happens. We will have to make a better jump routine and add other things in [[Digital Garden/Torchlight/Torchlight Platformer Part 2\|Torchlight Platformer Part 2]].

---

## Footnotes

[^1]: 	In the else part of the if/else block you can use this instead of the 2 if statements:

	```ad-scratch
	title:
	~~~scratchblock
	change [x speed v] by (<key [right arrow v] pressed?> - <key [left arrow v] pressed?>)
	~~~
	```

[^2]: You can do this:

	```ad-scratch
	title:
	~~~scratchblock
	define change y  by (speed)  in steps. stop at wall.
	repeat ([abs v] of (speed::custom)::operators)
	   change y by ((-1) * <not <touching [walls v]?>>)
	end
	~~~
	```

[^3]: In the real world, you are not moving, but still falling (feeling gravity). However, the ground is always stopping us. If a hole suddenly appears below us, we start falling and moving again.
[^4]: This is a one line way to do it:  

	```ad-scratch
	title:
	~~~scratchblock
	change [y speed v] by (<touching [walls v]?> * ((-1) * (y speed)))
	~~~
	```

[^5]: This is the pull out routine using one-liners:

	```ad-scratch
	title:
	~~~scratchblock
	define pull out if touching wall and <falling?> or not
	set [y speed v] to ((y speed) - (<touching [walls v]?> * (y speed)))
	change y by (<falling?> * <touching [walls v]?>)
	...
	~~~
	```
