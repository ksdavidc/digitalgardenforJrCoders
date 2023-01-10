---
{"dg-publish":true,"permalink":"/digital-garden/torchlight/torchlight-class-2/"}
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

1) __Fall__ from __Gravity__ 
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

<div id="Torchlight_Class_2_2023-01-10_1858.37.excalidraw.md2"></div><script>(function(){const InitialData={"type":"excalidraw","version":2,"source":"https://excalidraw.com","elements":[{"type":"rectangle","version":950,"versionNonce":1898665445,"isDeleted":false,"id":"IQ6rOFFZvMTSWgcGEyLwy","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":0,"opacity":90,"angle":0,"x":-693.407946611588,"y":-325.1235165066188,"strokeColor":"#000000","backgroundColor":"#15aabf","width":631.8104790581597,"height":429.9882100423177,"seed":88604805,"groupIds":[],"roundness":null,"boundElements":[],"updated":1673346069724,"link":null,"locked":false},{"type":"rectangle","version":107,"versionNonce":172566251,"isDeleted":false,"id":"poqJSmdk8S9buRCclfX3_","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-668.4341430664062,"y":-301.8651123046875,"strokeColor":"#000000","backgroundColor":"#fab005","width":278.25018310546875,"height":126.27056884765625,"seed":226496779,"groupIds":[],"roundness":{"type":3},"boundElements":[],"updated":1673346069724,"link":null,"locked":false},{"type":"rectangle","version":248,"versionNonce":2003915077,"isDeleted":false,"id":"Jk_6WMozSdcFwE4UfjcuV","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-665.6501973470051,"y":-146.12066650390625,"strokeColor":"#000000","backgroundColor":"#fab005","width":278.25018310546875,"height":217.73073323567706,"seed":769815819,"groupIds":[],"roundness":{"type":3},"boundElements":[],"updated":1673346069724,"link":null,"locked":false},{"type":"rectangle","version":685,"versionNonce":1878725003,"isDeleted":false,"id":"4ARIsV723Ale1Hzpt-n0o","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-653.4804438235251,"y":2.4655970908437155,"strokeColor":"#000000","backgroundColor":"#fa5252","width":245.58959960937503,"height":52.170654296875,"seed":1402598987,"groupIds":[],"roundness":{"type":1},"boundElements":[],"updated":1673346069724,"link":null,"locked":false},{"type":"rectangle","version":437,"versionNonce":1847648421,"isDeleted":false,"id":"kH-TN1tiyZGaeis8QmrFk","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-638.4808744604607,"y":-140.45203499698502,"strokeColor":"#000000","backgroundColor":"#4c6ef5","width":57.265625,"height":54.74920654296875,"seed":1138730981,"groupIds":[],"roundness":{"type":1},"boundElements":[{"id":"N-cHoNNujxTXZFgxEkRx0","type":"arrow"},{"id":"Rkz_objtIuEJ-PblH2lf9","type":"arrow"}],"updated":1673346069724,"link":null,"locked":false},{"type":"arrow","version":816,"versionNonce":693545003,"isDeleted":false,"id":"qscEptWjRIlFw4dWU2RoE","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-631.3924666768735,"y":-222.43307001760124,"strokeColor":"#000000","backgroundColor":"transparent","width":49.419652491337274,"height":16.607871681258615,"seed":691729643,"groupIds":[],"roundness":{"type":2},"boundElements":[],"updated":1673346069724,"link":null,"locked":false,"startBinding":{"elementId":"Nj36U0et","focus":0.5245995326500494,"gap":1.7020313007581365},"endBinding":{"elementId":"6TKJVMlw","focus":-0.4796930032683661,"gap":8.921788794911208},"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[18.074332772433536,13.73910958426336],[49.419652491337274,16.607871681258615]]},{"type":"text","version":632,"versionNonce":988251141,"isDeleted":false,"id":"gxoUBJpg","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-560.409405683334,"y":-286.70359896781775,"strokeColor":"#000000","backgroundColor":"transparent","width":136,"height":25,"seed":1329761291,"groupIds":["Q5-BjvZm_5sE9lBQEm7oA"],"roundness":null,"boundElements":[],"updated":1673346069724,"link":null,"locked":false,"fontSize":20,"fontFamily":1,"text":"1. add gravity","rawText":"1. add gravity","baseline":18,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"1. add gravity"},{"type":"text","version":620,"versionNonce":1816554187,"isDeleted":false,"id":"Nj36U0et","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-658.80126953125,"y":-249.13510131835938,"strokeColor":"#000000","backgroundColor":"transparent","width":73,"height":25,"seed":1410524037,"groupIds":["Sq7Hp2ej9xpHKHd2UYMeM"],"roundness":null,"boundElements":[{"id":"qscEptWjRIlFw4dWU2RoE","type":"arrow"}],"updated":1673346069724,"link":null,"locked":false,"fontSize":20,"fontFamily":1,"text":"y-speed","rawText":"y-speed","baseline":18,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"y-speed"},{"type":"text","version":733,"versionNonce":834845541,"isDeleted":false,"id":"6TKJVMlw","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-573.051025390625,"y":-219.38577270507812,"strokeColor":"#000000","backgroundColor":"transparent","width":173,"height":25,"seed":1885692811,"groupIds":["9EkArsalkhG__msVzi9pd"],"roundness":null,"boundElements":[{"id":"qscEptWjRIlFw4dWU2RoE","type":"arrow"}],"updated":1673346069724,"link":null,"locked":false,"fontSize":20,"fontFamily":1,"text":"y-speed + gravity","rawText":"y-speed + gravity","baseline":18,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"y-speed + gravity"},{"type":"text","version":896,"versionNonce":1298454891,"isDeleted":false,"id":"PGbQoU0a","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-561.703640407986,"y":-70.78773328993049,"strokeColor":"#000000","backgroundColor":"transparent","width":121,"height":38,"seed":1506928965,"groupIds":["azPgFYYkKFsJDfWnb-Bik"],"roundness":null,"boundElements":[],"updated":1673346069724,"link":null,"locked":false,"fontSize":15.080829196506082,"fontFamily":1,"text":"y-speed times\nor until touching","rawText":"y-speed times\nor until touching","baseline":33,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"y-speed times\nor until touching"},{"type":"rectangle","version":651,"versionNonce":1258292933,"isDeleted":false,"id":"M5w74z-gCEA7IZ7EEx2YT","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-639.2559746636285,"y":-41.40579901801215,"strokeColor":"#000000","backgroundColor":"#4c6ef5","width":57.265625,"height":54.74920654296875,"seed":2124772107,"groupIds":[],"roundness":{"type":1},"boundElements":[{"id":"Rkz_objtIuEJ-PblH2lf9","type":"arrow"},{"id":"siybOWI-owhbHOHHdNYGN","type":"arrow"}],"updated":1673346069724,"link":null,"locked":false},{"type":"text","version":637,"versionNonce":1778152459,"isDeleted":false,"id":"6wSdeR8Z","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-559.332275390625,"y":-129.90850830078125,"strokeColor":"#000000","backgroundColor":"transparent","width":66,"height":25,"seed":126222597,"groupIds":["ljTKNwCFK053olMavlFFu"],"roundness":null,"boundElements":[],"updated":1673346069724,"link":null,"locked":false,"fontSize":20,"fontFamily":1,"text":"2. Fall","rawText":"2. Fall","baseline":18,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"2. Fall"},{"type":"rectangle","version":294,"versionNonce":423421477,"isDeleted":false,"id":"MYzZO5Dt6lDp-w5prWJV9","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-362.0101962619357,"y":-298.3898555658212,"strokeColor":"#000000","backgroundColor":"#fab005","width":278.25018310546875,"height":126.27056884765625,"seed":2089437573,"groupIds":[],"roundness":{"type":3},"boundElements":[],"updated":1673346069724,"link":null,"locked":false},{"type":"rectangle","version":609,"versionNonce":1376238251,"isDeleted":false,"id":"eMXy_H3SAXetnKv8J1Jg1","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-351.94194081245723,"y":-200.77798433218237,"strokeColor":"#000000","backgroundColor":"#fa5252","width":245.58959960937503,"height":52.170654296875,"seed":524074315,"groupIds":[],"roundness":{"type":1},"boundElements":[],"updated":1673346069724,"link":null,"locked":false},{"type":"arrow","version":1915,"versionNonce":2137446789,"isDeleted":false,"id":"1NnlCxxfk4ttlkO89U_So","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":3.141592653589793,"x":-251.6573626159534,"y":-206.27239887499172,"strokeColor":"#000000","backgroundColor":"transparent","width":21.262150912917775,"height":21.85233881414382,"seed":585948139,"groupIds":[],"roundness":{"type":2},"boundElements":[],"updated":1673346069724,"link":null,"locked":false,"startBinding":{"elementId":"sq11EZPOH0HIE4Z57e4hq","focus":0.9878536225439541,"gap":1.0000000000001137},"endBinding":{"elementId":"N9VB5b_WfASD5hGMIIkH1","focus":0.1713089656302935,"gap":1},"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[-21.057432165872854,10.175077219401771],[0.20471874704492166,21.85233881414382]]},{"type":"rectangle","version":612,"versionNonce":842083659,"isDeleted":false,"id":"sq11EZPOH0HIE4Z57e4hq","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-330.1132473415797,"y":-236.24544977697568,"strokeColor":"#000000","backgroundColor":"#4c6ef5","width":57.265625,"height":54.74920654296875,"seed":73410187,"groupIds":[],"roundness":{"type":1},"boundElements":[{"id":"1NnlCxxfk4ttlkO89U_So","type":"arrow"}],"updated":1673346069724,"link":null,"locked":false},{"type":"text","version":758,"versionNonce":649814245,"isDeleted":false,"id":"6rEjge58","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-255.5566134982638,"y":-282.0646466899531,"strokeColor":"#000000","backgroundColor":"transparent","width":100,"height":25,"seed":235117477,"groupIds":["pWYhEjWpBMPhp9P2taodM"],"roundness":null,"boundElements":[],"updated":1673346069724,"link":null,"locked":false,"fontSize":20,"fontFamily":1,"text":"3. Pull Up","rawText":"3. Pull Up","baseline":18,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"3. Pull Up"},{"type":"rectangle","version":600,"versionNonce":1037257707,"isDeleted":false,"id":"N9VB5b_WfASD5hGMIIkH1","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-330.0251193576388,"y":-255.2039693196615,"strokeColor":"#000000","backgroundColor":"#4c6ef5","width":57.265625,"height":54.74920654296875,"seed":1957829035,"groupIds":[],"roundness":{"type":1},"boundElements":[{"id":"1NnlCxxfk4ttlkO89U_So","type":"arrow"}],"updated":1673346069724,"link":null,"locked":false},{"type":"arrow","version":2010,"versionNonce":885521477,"isDeleted":false,"id":"N-cHoNNujxTXZFgxEkRx0","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-579.2536972227203,"y":-108.1237796923203,"strokeColor":"#000000","backgroundColor":"transparent","width":13.22988649398576,"height":30.4132343941547,"seed":1332719045,"groupIds":["YEQl5zrYrDuD-N5TNySP_"],"roundness":{"type":2},"boundElements":[],"updated":1673346069724,"link":null,"locked":false,"startBinding":{"elementId":"kH-TN1tiyZGaeis8QmrFk","focus":-0.5023346710137028,"gap":1.9615522377403067},"endBinding":{"elementId":"kH-TN1tiyZGaeis8QmrFk","focus":1.1856923123622165,"gap":8.105333828593714},"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[13.22988649398576,15.265039097155807],[0.8943984499916269,30.4132343941547]]},{"type":"arrow","version":2076,"versionNonce":1492686475,"isDeleted":false,"id":"Rkz_objtIuEJ-PblH2lf9","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-578.3321869372833,"y":-77.30190555291409,"strokeColor":"#000000","backgroundColor":"transparent","width":13.22988649398576,"height":30.4132343941547,"seed":1626704165,"groupIds":["YEQl5zrYrDuD-N5TNySP_"],"roundness":{"type":2},"boundElements":[],"updated":1673346069724,"link":null,"locked":false,"startBinding":{"elementId":"kH-TN1tiyZGaeis8QmrFk","focus":-0.0654729436808464,"gap":9.437998576360329},"endBinding":{"elementId":"M5w74z-gCEA7IZ7EEx2YT","focus":0.21777748572590575,"gap":8.369408930810437},"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[13.22988649398576,15.265039097155807],[0.8943984499916269,30.4132343941547]]},{"type":"arrow","version":2041,"versionNonce":1097477029,"isDeleted":false,"id":"siybOWI-owhbHOHHdNYGN","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-579.2528920199978,"y":-45.99129065239545,"strokeColor":"#000000","backgroundColor":"transparent","width":13.22988649398576,"height":30.4132343941547,"seed":1593846597,"groupIds":["YEQl5zrYrDuD-N5TNySP_"],"roundness":{"type":2},"boundElements":[],"updated":1673346069724,"link":null,"locked":false,"startBinding":{"elementId":"M5w74z-gCEA7IZ7EEx2YT","focus":-1.2748889165379966,"gap":10.41843089097506},"endBinding":{"focus":1.1856923123622165,"gap":8.105333828593714,"elementId":"kH-TN1tiyZGaeis8QmrFk"},"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[13.22988649398576,15.265039097155807],[0.8943984499916269,30.4132343941547]]},{"type":"text","version":1038,"versionNonce":39554347,"isDeleted":false,"id":"vD6lUpAI","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-249.08482649440043,"y":-201.93467203776038,"strokeColor":"#000000","backgroundColor":"transparent","width":130,"height":19,"seed":1781318475,"groupIds":["1U3lFeZvA_3wUHwOpBEJc"],"roundness":null,"boundElements":[],"updated":1673346069724,"link":null,"locked":false,"fontSize":15.080829196506082,"fontFamily":1,"text":"until not touching","rawText":"until not touching","baseline":14,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"until not touching"},{"type":"rectangle","version":385,"versionNonce":1491364133,"isDeleted":false,"id":"yDgPDw7UbQDo2_lGPJLNW","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-363.90813206456266,"y":-97.35563072791439,"strokeColor":"#000000","backgroundColor":"#fab005","width":278.25018310546875,"height":126.27056884765625,"seed":1626105387,"groupIds":[],"roundness":{"type":3},"boundElements":[],"updated":1673346757876,"link":null,"locked":false},{"type":"text","version":884,"versionNonce":1691215787,"isDeleted":false,"id":"Mq2FG90g","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-257.4545493008908,"y":-81.03042185204629,"strokeColor":"#000000","backgroundColor":"transparent","width":146,"height":50,"seed":939236709,"groupIds":["kY4lA0OEEtiMvCXmvI1fv"],"roundness":null,"boundElements":[],"updated":1673346757876,"link":null,"locked":false,"fontSize":20,"fontFamily":1,"text":"4. Go back to\nleft/right step","rawText":"4. Go back to\nleft/right step","baseline":43,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"4. Go back to\nleft/right step"},{"type":"text","version":1024,"versionNonce":86375557,"isDeleted":false,"id":"60LsnkBs","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-336.64559664330557,"y":-10.701501741530397,"strokeColor":"#087f5b","backgroundColor":"transparent","width":216.60307742387818,"height":18.369165576583303,"seed":2065542501,"groupIds":["n5w3Fm6yKOe24LtxkIG4M"],"roundness":null,"boundElements":null,"updated":1673346757876,"link":null,"locked":false,"fontSize":15.307637980486085,"fontFamily":3,"text":"broadcast [left right v]","rawText":"broadcast [left right v]","baseline":14.369165576583303,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"broadcast [left right v]"}],"appState":{"theme":"light","viewBackgroundColor":"#ffffff","currentItemStrokeColor":"#087f5b","currentItemBackgroundColor":"#fa5252","currentItemFillStyle":"hachure","currentItemStrokeWidth":1,"currentItemStrokeStyle":"solid","currentItemRoughness":1,"currentItemOpacity":100,"currentItemFontFamily":3,"currentItemFontSize":20,"currentItemTextAlign":"left","currentItemStartArrowhead":null,"currentItemEndArrowhead":"arrow","scrollX":715.0527230455491,"scrollY":368.70312943417787,"zoom":{"value":1.9500000000000002},"currentItemRoundness":"round","gridSize":null,"colorPalette":{}},"files":{}};InitialData.scrollToContent=true;App=()=>{const e=React.useRef(null),t=React.useRef(null),[n,i]=React.useState({width:void 0,height:void 0});return React.useEffect(()=>{i({width:t.current.getBoundingClientRect().width,height:t.current.getBoundingClientRect().height});const e=()=>{i({width:t.current.getBoundingClientRect().width,height:t.current.getBoundingClientRect().height})};return window.addEventListener("resize",e),()=>window.removeEventListener("resize",e)},[t]),React.createElement(React.Fragment,null,React.createElement("div",{className:"excalidraw-wrapper",ref:t},React.createElement(ExcalidrawLib.Excalidraw,{ref:e,width:n.width,height:n.height,initialData:InitialData,viewModeEnabled:!0,zenModeEnabled:!0,gridModeEnabled:!1})))},excalidrawWrapper=document.getElementById("Torchlight_Class_2_2023-01-10_1858.37.excalidraw.md2");ReactDOM.render(React.createElement(App),excalidrawWrapper);})();</script>

### Turning words into code

The important thing is to translate these words into things that Scratch understands. We have to turn words into code. Let's see how to do it.

Look at step 1.
<br/>
**Step 1:** Scratch doesn't know what **fall faster** means. But Scratch does understand: 
	- **Change `y speed` by `gravity`**, which is the same thing.
<br/>
**Step 2:** Again, scratch doesn't know what **move down** means. But it does understand:
	- **Change `y position` by `y speed`**. `y speed` tells us how much to fall.
<br/>

**Step 3:** __Hit a wall__ and __stop falling and pull out__ means
	- **If** `touching wall` **then** **set `y speed` to 0** and **pull out**. 
Do you see how the words become code?
<br/>

**Step 4:** Scratch can't **go back to moving left and right**, but it can
	- **Broadcast `left/right`**. "Go to" is like **broadcast** in scratch.
  



### Create Myblocks
We will use myblocks for the 2 middle steps. 

- **Change** `y position` by `y speed`
- When you hit a wall **set `y speed` to 0** and **pull out**


I will show how to make these below, but first I will explain what is different about them.
   
    

#### Inputs and Booleans


```ad-example
title: Myblocks with Inputs


**Myblocks with inputs** are a little different from the **simple myblocks** we made in the first class for `set x speed` and `keep x speed below max`. 
- We give these myblocks **information**. 
- There are 2 kinds of information.
	-  __Inputs__ can be any kind of number or text
	-  __Booleans__ can only be `true` or `false`  

I will give these myblocks names that explain how to use the inputs.
```




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

<div id="HatlightFalllingInSteps.excalidraw.md3"></div><script>(function(){const InitialData={"type":"excalidraw","version":2,"source":"https://excalidraw.com","elements":[{"type":"rectangle","version":509,"versionNonce":1097604415,"isDeleted":false,"id":"X3eKC4g-yx-XMt1rWBuif","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":0,"opacity":90,"angle":0,"x":-449.85944519800233,"y":-216.8266251263254,"strokeColor":"#000000","backgroundColor":"#15aabf","width":580.8837890625,"height":409.2378845214844,"seed":1523261399,"groupIds":[],"strokeSharpness":"sharp","boundElements":[],"updated":1670350288450,"link":null,"locked":false},{"type":"rectangle","version":302,"versionNonce":628174593,"isDeleted":false,"id":"0fbDeUvnFGOAHWrwifOSV","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-447.225341796875,"y":60.57232666015625,"strokeColor":"#000000","backgroundColor":"#fa5252","width":578.7227783203125,"height":52.170654296875,"seed":1658367257,"groupIds":[],"strokeSharpness":"round","boundElements":[{"id":"KzzUe-i6RXE-mzwhfi58q","type":"arrow"},{"id":"BLtrddpDIMI7sGaAGwKk-","type":"arrow"},{"id":"X0vEXzL366tfW-NuY40fC","type":"arrow"}],"updated":1669876161475,"link":null,"locked":false},{"type":"rectangle","version":246,"versionNonce":146668943,"isDeleted":false,"id":"aSzZsl74H852Oj-GLVfFu","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-378.5940653483073,"y":-171.21595836821058,"strokeColor":"#000000","backgroundColor":"#4c6ef5","width":57.265625,"height":54.74920654296875,"seed":1445399799,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1669876161475,"link":null,"locked":false},{"type":"arrow","version":468,"versionNonce":1750443745,"isDeleted":false,"id":"g4ekkcbqxsQejMG8sMtHJ","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-322.04160417829235,"y":-119.28085908435634,"strokeColor":"#000000","backgroundColor":"transparent","width":34.315359933035836,"height":40.774100167410666,"seed":1905810487,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1669876161475,"link":null,"locked":false,"startBinding":null,"endBinding":null,"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[30.880417596726204,25.17081124441961],[-3.434942336309632,40.774100167410666]]},{"type":"arrow","version":663,"versionNonce":778400687,"isDeleted":false,"id":"2AgNi4LavDQ_DT3pTVCAZ","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-325.1728239513577,"y":-75.07850138346353,"strokeColor":"#000000","backgroundColor":"transparent","width":30.530598958333485,"height":47.169131324404646,"seed":983790713,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1669876161475,"link":null,"locked":false,"startBinding":null,"endBinding":null,"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[28.942522321428612,24.00812058221726],[-1.5880766369048729,47.169131324404646]]},{"type":"arrow","version":1091,"versionNonce":1805656769,"isDeleted":false,"id":"X0vEXzL366tfW-NuY40fC","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-327.6087661016555,"y":-26.44208490280866,"strokeColor":"#000000","backgroundColor":"transparent","width":34.75597563244054,"height":71.13309442429308,"seed":1849024089,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1669876161475,"link":null,"locked":false,"startBinding":null,"endBinding":{"elementId":"0fbDeUvnFGOAHWrwifOSV","focus":-0.6814801411047785,"gap":15.881317138671847},"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[34.75597563244054,31.764758882068406],[10.047314073160862,71.13309442429308]]},{"type":"arrow","version":1088,"versionNonce":939075023,"isDeleted":false,"id":"KzzUe-i6RXE-mzwhfi58q","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-318.67275529515456,"y":46.66189139229917,"strokeColor":"#000000","backgroundColor":"transparent","width":36.471470424107224,"height":99.6491335914248,"seed":595548951,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1669876161475,"link":null,"locked":false,"startBinding":{"elementId":"0fbDeUvnFGOAHWrwifOSV","focus":0.4731328064733432,"gap":13.910435267857082},"endBinding":{"elementId":"FFjJe3DO","focus":-0.22043555957681688,"gap":1.6255536760602638},"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[21.017031360072792,46.019605364118206],[-15.454439064034432,99.6491335914248]]},{"type":"text","version":162,"versionNonce":1005593249,"isDeleted":false,"id":"FFjJe3DO","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-431.50949823288687,"y":147.93657865978423,"strokeColor":"#000000","backgroundColor":"transparent","width":230,"height":25,"seed":1764694073,"groupIds":[],"strokeSharpness":"sharp","boundElements":[{"id":"KzzUe-i6RXE-mzwhfi58q","type":"arrow"}],"updated":1669876161475,"link":null,"locked":false,"fontSize":20,"fontFamily":1,"text":"oops I jumped too far!","rawText":"oops I jumped too far!","baseline":18,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"oops I jumped too far!"},{"type":"rectangle","version":379,"versionNonce":1418826735,"isDeleted":false,"id":"UdmsIpWycJ77Ag8M3_jmW","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-147.30171857561396,"y":-169.37390500023255,"strokeColor":"#000000","backgroundColor":"#4c6ef5","width":57.265625,"height":54.74920654296875,"seed":1579585465,"groupIds":[],"strokeSharpness":"round","boundElements":[{"id":"i5h6ALg0GKwRab9r0C90J","type":"arrow"}],"updated":1669876161475,"link":null,"locked":false},{"type":"text","version":474,"versionNonce":636823169,"isDeleted":false,"id":"XbZ1dBRn","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-147.31605893089665,"y":67.45377478661476,"strokeColor":"#000000","backgroundColor":"transparent","width":109,"height":40,"seed":327270615,"groupIds":[],"strokeSharpness":"sharp","boundElements":[],"updated":1669876161475,"link":null,"locked":false,"fontSize":15.849432887262545,"fontFamily":1,"text":"I stop when\nI hit the wall","rawText":"I stop when\nI hit the wall","baseline":34,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"I stop when\nI hit the wall"},{"type":"arrow","version":2600,"versionNonce":1010253327,"isDeleted":false,"id":"bwETjqIAwsfaCBXToq7mr","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-96.99687863162217,"y":-114.2402766778728,"strokeColor":"#c92a2a","backgroundColor":"transparent","width":13.856572150963103,"height":10.931379070486201,"seed":1736422807,"groupIds":["wyA1Lk3TbbMGq0vS8op__"],"strokeSharpness":"round","boundElements":[],"updated":1669876161475,"link":null,"locked":false,"startBinding":{"elementId":"ctgLPHBO","focus":1.3025348090580142,"gap":11.247209584646924},"endBinding":{"elementId":"FTeCu3eZ","focus":0.21833418349062747,"gap":14.0985978045654},"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[-10.570859372029787,5.047996387929032],[3.2857127789333163,10.931379070486201]]},{"type":"text","version":1145,"versionNonce":879668833,"isDeleted":false,"id":"FTeCu3eZ","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-113.80976365725425,"y":-117.71653355325589,"strokeColor":"#c92a2a","backgroundColor":"transparent","width":6,"height":18,"seed":431051609,"groupIds":["wyA1Lk3TbbMGq0vS8op__"],"strokeSharpness":"sharp","boundElements":[{"id":"bwETjqIAwsfaCBXToq7mr","type":"arrow"}],"updated":1669876161475,"link":null,"locked":false,"fontSize":14.39868181190029,"fontFamily":1,"text":"1","rawText":"1","baseline":13,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"1"},{"type":"arrow","version":574,"versionNonce":300065839,"isDeleted":false,"id":"i5h6ALg0GKwRab9r0C90J","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-86.0445995248241,"y":-118.44435015194466,"strokeColor":"#000000","backgroundColor":"transparent","width":36.829425328712304,"height":41.91725264538508,"seed":2040880983,"groupIds":["GqIiQvxPWWtvjf3-ZGR_E"],"strokeSharpness":"round","boundElements":[],"updated":1669876161475,"link":null,"locked":false,"startBinding":{"elementId":"UdmsIpWycJ77Ag8M3_jmW","focus":-0.058536680852082454,"gap":3.9914940507898677},"endBinding":{"elementId":"jJvHk8rL","focus":0.5505995457757742,"gap":15.816156400444058},"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[30.880417596726204,25.17081124441961],[-5.9490077319861,41.91725264538508]]},{"type":"arrow","version":771,"versionNonce":1848392257,"isDeleted":false,"id":"xE_jOsYBF4k_BoFbHpGdK","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-91.73554451131523,"y":-76.36531089920823,"strokeColor":"#000000","backgroundColor":"transparent","width":31.502247534854376,"height":49.38529208954589,"seed":1701062041,"groupIds":["GqIiQvxPWWtvjf3-ZGR_E"],"strokeSharpness":"round","boundElements":[],"updated":1669876161475,"link":null,"locked":false,"startBinding":{"elementId":"7XmCKnsZ","focus":-3.0261669778726485,"gap":15.746478778799087},"endBinding":null,"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[31.502247534854376,26.131439030373656],[0.8699029710521415,49.38529208954589]]},{"type":"arrow","version":1109,"versionNonce":92030543,"isDeleted":false,"id":"BLtrddpDIMI7sGaAGwKk-","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-91.61176144818722,"y":-25.530696345233416,"strokeColor":"#000000","backgroundColor":"transparent","width":38.19080171130963,"height":70.15996040459827,"seed":781016183,"groupIds":["GqIiQvxPWWtvjf3-ZGR_E"],"strokeSharpness":"round","boundElements":[],"updated":1669876161475,"link":null,"locked":false,"startBinding":null,"endBinding":{"elementId":"lDDvswtv","focus":0.5780699842586904,"gap":12.76317613019792},"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[34.75597563244054,31.689879256904867],[-3.4348260788690936,70.15996040459827]]},{"type":"arrow","version":2772,"versionNonce":1410157089,"isDeleted":false,"id":"30AQK5MQuPXKIWI8XeajQ","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-96.99687863162218,"y":-99.51681021784279,"strokeColor":"#c92a2a","backgroundColor":"transparent","width":13.856572150963103,"height":10.931379070486201,"seed":882254841,"groupIds":["UCExYSlleJjMwFZ7Qzell"],"strokeSharpness":"round","boundElements":[],"updated":1669876161475,"link":null,"locked":false,"startBinding":{"elementId":"ctgLPHBO","focus":-0.05236135082726946,"gap":10.812885025632056},"endBinding":{"elementId":"ctgLPHBO","focus":0.21833418349062633,"gap":14.098597804565372},"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[-10.570859372029787,5.047996387929032],[3.2857127789333163,10.931379070486201]]},{"type":"text","version":1237,"versionNonce":903652463,"isDeleted":false,"id":"ctgLPHBO","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-113.80976365725424,"y":-102.99306709322587,"strokeColor":"#c92a2a","backgroundColor":"transparent","width":6,"height":18,"seed":575206423,"groupIds":["UCExYSlleJjMwFZ7Qzell"],"strokeSharpness":"sharp","boundElements":[{"id":"30AQK5MQuPXKIWI8XeajQ","type":"arrow"},{"id":"i5h6ALg0GKwRab9r0C90J","type":"arrow"},{"id":"xE_jOsYBF4k_BoFbHpGdK","type":"arrow"},{"id":"bwETjqIAwsfaCBXToq7mr","type":"arrow"}],"updated":1669876161475,"link":null,"locked":false,"fontSize":14.39868181190029,"fontFamily":1,"text":"1","rawText":"1","baseline":13,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"1"},{"type":"arrow","version":3153,"versionNonce":520183297,"isDeleted":false,"id":"G4TbwLAZZPqXZpdYasfnt","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-96.66913826448226,"y":-61.49893796083916,"strokeColor":"#c92a2a","backgroundColor":"transparent","width":13.201091416683255,"height":11.462341104562512,"seed":526494103,"groupIds":["weyBgE4-Gw0c2s9XRE2_F"],"strokeSharpness":"round","boundElements":[],"updated":1669876161475,"link":null,"locked":false,"startBinding":{"elementId":"jJvHk8rL","focus":-1.644936525924756,"gap":8.722620557558997},"endBinding":{"elementId":"jJvHk8rL","focus":-1.4923387363459997,"gap":13.899216539584984},"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[-10.570859372029787,5.047996387929032],[2.630232044653468,11.462341104562512]]},{"type":"text","version":1376,"versionNonce":1389117071,"isDeleted":false,"id":"7XmCKnsZ","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-113.48202329011431,"y":-65.06769084119384,"strokeColor":"#c92a2a","backgroundColor":"transparent","width":6,"height":18,"seed":1075355481,"groupIds":["weyBgE4-Gw0c2s9XRE2_F"],"strokeSharpness":"sharp","boundElements":[{"id":"G4TbwLAZZPqXZpdYasfnt","type":"arrow"},{"id":"i5h6ALg0GKwRab9r0C90J","type":"arrow"},{"id":"xE_jOsYBF4k_BoFbHpGdK","type":"arrow"},{"id":"itKSWnAAJjQpjm2vWnion","type":"arrow"}],"updated":1669876161475,"link":null,"locked":false,"fontSize":14.39868181190029,"fontFamily":1,"text":"1","rawText":"1","baseline":13,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"1"},{"type":"arrow","version":3137,"versionNonce":1040709089,"isDeleted":false,"id":"BIlN-z6qp0Zwaqb-TssE9","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-96.9968786316222,"y":-42.58356603282854,"strokeColor":"#c92a2a","backgroundColor":"transparent","width":13.856572150963103,"height":10.931379070486201,"seed":1807732951,"groupIds":["NQ-rDOsEk5HrskJzH4NlO"],"strokeSharpness":"round","boundElements":[],"updated":1669876161475,"link":null,"locked":false,"startBinding":{"elementId":"htRXZrxu","focus":1.6426025233326276,"gap":14.580910871420855},"endBinding":{"focus":0.21833418349062633,"gap":14.098597804565372,"elementId":"lW84oqgi"},"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[-10.570859372029787,5.047996387929032],[3.2857127789333163,10.931379070486201]]},{"type":"text","version":1418,"versionNonce":2130941103,"isDeleted":false,"id":"lW84oqgi","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-113.80976365725422,"y":-46.05982290821163,"strokeColor":"#c92a2a","backgroundColor":"transparent","width":6,"height":18,"seed":226724889,"groupIds":["NQ-rDOsEk5HrskJzH4NlO"],"strokeSharpness":"sharp","boundElements":[{"id":"BIlN-z6qp0Zwaqb-TssE9","type":"arrow"},{"id":"i5h6ALg0GKwRab9r0C90J","type":"arrow"},{"id":"xE_jOsYBF4k_BoFbHpGdK","type":"arrow"},{"id":"itKSWnAAJjQpjm2vWnion","type":"arrow"},{"id":"G4TbwLAZZPqXZpdYasfnt","type":"arrow"}],"updated":1669876161475,"link":null,"locked":false,"fontSize":14.39868181190029,"fontFamily":1,"text":"1","rawText":"1","baseline":13,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"1"},{"type":"arrow","version":3319,"versionNonce":338727361,"isDeleted":false,"id":"itKSWnAAJjQpjm2vWnion","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-98.07172168029871,"y":-79.2060268563084,"strokeColor":"#c92a2a","backgroundColor":"transparent","width":12.926063450679067,"height":10.229271525456682,"seed":1900335223,"groupIds":["rDGyDIC4wj-sxzu3feEwR"],"strokeSharpness":"round","boundElements":[],"updated":1669876161475,"link":null,"locked":false,"startBinding":{"elementId":"jJvHk8rL","focus":-0.4600932661649485,"gap":9.738041976955543},"endBinding":{"elementId":"jJvHk8rL","focus":0.21833418349062747,"gap":14.0985978045654},"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[-8.565507623069209,7.309658929014603],[4.360555827609858,10.229271525456682]]},{"type":"text","version":1323,"versionNonce":1915430607,"isDeleted":false,"id":"jJvHk8rL","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-113.80976365725425,"y":-83.384391276721,"strokeColor":"#c92a2a","backgroundColor":"transparent","width":6,"height":18,"seed":1317525113,"groupIds":["rDGyDIC4wj-sxzu3feEwR"],"strokeSharpness":"sharp","boundElements":[{"id":"itKSWnAAJjQpjm2vWnion","type":"arrow"},{"id":"G4TbwLAZZPqXZpdYasfnt","type":"arrow"},{"id":"i5h6ALg0GKwRab9r0C90J","type":"arrow"}],"updated":1669876161475,"link":null,"locked":false,"fontSize":14.39868181190029,"fontFamily":1,"text":"1","rawText":"1","baseline":13,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"1"},{"type":"arrow","version":2920,"versionNonce":1989849505,"isDeleted":false,"id":"pbeHb5a0uoNX9WtBB610c","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-96.99687863162218,"y":-24.52639828602463,"strokeColor":"#c92a2a","backgroundColor":"transparent","width":13.856572150963103,"height":10.931379070486201,"seed":652062743,"groupIds":["4rrK6TF_CuV7ezukefjSq"],"strokeSharpness":"round","boundElements":[],"updated":1669876161475,"link":null,"locked":false,"startBinding":{"elementId":"FriW2rj1","focus":1.2454866162586973,"gap":13.018445883231465},"endBinding":{"elementId":"htRXZrxu","focus":0.218334183490629,"gap":14.098597804565372},"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[-10.570859372029787,5.047996387929032],[3.2857127789333163,10.931379070486201]]},{"type":"text","version":1311,"versionNonce":1524331759,"isDeleted":false,"id":"htRXZrxu","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-113.80976365725424,"y":-28.002655161407688,"strokeColor":"#c92a2a","backgroundColor":"transparent","width":6,"height":18,"seed":52838617,"groupIds":["4rrK6TF_CuV7ezukefjSq"],"strokeSharpness":"sharp","boundElements":[{"id":"pbeHb5a0uoNX9WtBB610c","type":"arrow"},{"id":"i5h6ALg0GKwRab9r0C90J","type":"arrow"},{"id":"BIlN-z6qp0Zwaqb-TssE9","type":"arrow"}],"updated":1669876161475,"link":null,"locked":false,"fontSize":14.39868181190029,"fontFamily":1,"text":"1","rawText":"1","baseline":13,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"1"},{"type":"arrow","version":3278,"versionNonce":1786107265,"isDeleted":false,"id":"BZmTNh1W-NmZpnKNsAg8b","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-96.99687863162218,"y":32.21260428854929,"strokeColor":"#c92a2a","backgroundColor":"transparent","width":13.856572150963103,"height":10.931379070486201,"seed":639882839,"groupIds":["8H2UnQk_e6PsHRJ2vF_T5"],"strokeSharpness":"round","boundElements":[],"updated":1669876161475,"link":null,"locked":false,"startBinding":{"elementId":"gyk0nbcr","focus":-2.0005529473798833,"gap":11.941413967393373},"endBinding":{"elementId":"lDDvswtv","focus":1.4681909500270411,"gap":10.245825698741498},"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[-10.570859372029787,5.047996387929032],[3.2857127789333163,10.931379070486201]]},{"type":"text","version":1490,"versionNonce":10288911,"isDeleted":false,"id":"GhGulrWn","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-113.80976365725424,"y":28.7363474131662,"strokeColor":"#c92a2a","backgroundColor":"transparent","width":6,"height":18,"seed":527212185,"groupIds":["8H2UnQk_e6PsHRJ2vF_T5"],"strokeSharpness":"sharp","boundElements":[{"id":"BZmTNh1W-NmZpnKNsAg8b","type":"arrow"},{"id":"i5h6ALg0GKwRab9r0C90J","type":"arrow"},{"id":"xE_jOsYBF4k_BoFbHpGdK","type":"arrow"},{"id":"itKSWnAAJjQpjm2vWnion","type":"arrow"}],"updated":1669876161475,"link":null,"locked":false,"fontSize":14.39868181190029,"fontFamily":1,"text":"1","rawText":"1","baseline":13,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"1"},{"type":"arrow","version":3413,"versionNonce":587300193,"isDeleted":false,"id":"Sz8xeGELrBil9xoaOIm_J","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-96.99687863162218,"y":47.314133496645894,"strokeColor":"#c92a2a","backgroundColor":"transparent","width":13.856572150963103,"height":10.931379070486201,"seed":1549525337,"groupIds":["UWcnU8VbgbX9PWpg8IRha"],"strokeSharpness":"round","boundElements":[],"updated":1669876161475,"link":null,"locked":false,"startBinding":{"elementId":"lDDvswtv","focus":-0.05236135082726946,"gap":10.812885025632056},"endBinding":{"focus":0.21833418349062633,"gap":14.098597804565372,"elementId":"lDDvswtv"},"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[-10.570859372029787,5.047996387929032],[3.2857127789333163,10.931379070486201]]},{"type":"text","version":1563,"versionNonce":635979055,"isDeleted":false,"id":"lDDvswtv","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-113.80976365725424,"y":43.83787662126281,"strokeColor":"#c92a2a","backgroundColor":"transparent","width":6,"height":18,"seed":282082487,"groupIds":["UWcnU8VbgbX9PWpg8IRha"],"strokeSharpness":"sharp","boundElements":[{"id":"Sz8xeGELrBil9xoaOIm_J","type":"arrow"},{"id":"i5h6ALg0GKwRab9r0C90J","type":"arrow"},{"id":"xE_jOsYBF4k_BoFbHpGdK","type":"arrow"},{"id":"itKSWnAAJjQpjm2vWnion","type":"arrow"},{"id":"BZmTNh1W-NmZpnKNsAg8b","type":"arrow"},{"id":"BLtrddpDIMI7sGaAGwKk-","type":"arrow"}],"updated":1669876161475,"link":null,"locked":false,"fontSize":14.39868181190029,"fontFamily":1,"text":"1","rawText":"1","baseline":13,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"1"},{"type":"arrow","version":3341,"versionNonce":1066215745,"isDeleted":false,"id":"R4mfxyq1rVtvRc5OSL9QM","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-96.99687863162221,"y":-9.284282918482006,"strokeColor":"#c92a2a","backgroundColor":"transparent","width":13.856572150963103,"height":10.931379070486201,"seed":1492729529,"groupIds":["nwIQTCVt-HW39_YL7nIJy"],"strokeSharpness":"round","boundElements":[],"updated":1669876161475,"link":null,"locked":false,"startBinding":{"elementId":"FriW2rj1","focus":-0.052361350827266985,"gap":10.812885025632},"endBinding":{"focus":0.21833418349062633,"gap":14.098597804565372,"elementId":"FriW2rj1"},"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[-10.570859372029787,5.047996387929032],[3.2857127789333163,10.931379070486201]]},{"type":"text","version":1523,"versionNonce":707118927,"isDeleted":false,"id":"FriW2rj1","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-113.80976365725421,"y":-12.760539793865092,"strokeColor":"#c92a2a","backgroundColor":"transparent","width":6,"height":18,"seed":1028253015,"groupIds":["nwIQTCVt-HW39_YL7nIJy"],"strokeSharpness":"sharp","boundElements":[{"id":"R4mfxyq1rVtvRc5OSL9QM","type":"arrow"},{"id":"i5h6ALg0GKwRab9r0C90J","type":"arrow"},{"id":"xE_jOsYBF4k_BoFbHpGdK","type":"arrow"},{"id":"itKSWnAAJjQpjm2vWnion","type":"arrow"},{"id":"G4TbwLAZZPqXZpdYasfnt","type":"arrow"},{"id":"pbeHb5a0uoNX9WtBB610c","type":"arrow"}],"updated":1669876161475,"link":null,"locked":false,"fontSize":14.39868181190029,"fontFamily":1,"text":"1","rawText":"1","baseline":13,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"1"},{"type":"arrow","version":3473,"versionNonce":1232623905,"isDeleted":false,"id":"sGG3rEuEkggAAXmB2n6iz","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-96.99687863162221,"y":11.452688849983957,"strokeColor":"#c92a2a","backgroundColor":"transparent","width":13.856572150963103,"height":10.931379070486201,"seed":567682297,"groupIds":["8PqRhJn4x0YIw2xmuRPxm"],"strokeSharpness":"round","boundElements":[],"updated":1669876161475,"link":null,"locked":false,"startBinding":{"elementId":"gyk0nbcr","focus":-0.052361350827266985,"gap":10.812885025632},"endBinding":{"focus":0.21833418349062633,"gap":14.098597804565372,"elementId":"gyk0nbcr"},"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[-10.570859372029787,5.047996387929032],[3.2857127789333163,10.931379070486201]]},{"type":"text","version":1589,"versionNonce":1806566767,"isDeleted":false,"id":"gyk0nbcr","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-113.80976365725421,"y":7.976431974600871,"strokeColor":"#c92a2a","backgroundColor":"transparent","width":6,"height":18,"seed":700810007,"groupIds":["8PqRhJn4x0YIw2xmuRPxm"],"strokeSharpness":"sharp","boundElements":[{"id":"sGG3rEuEkggAAXmB2n6iz","type":"arrow"},{"id":"i5h6ALg0GKwRab9r0C90J","type":"arrow"},{"id":"xE_jOsYBF4k_BoFbHpGdK","type":"arrow"},{"id":"itKSWnAAJjQpjm2vWnion","type":"arrow"},{"id":"G4TbwLAZZPqXZpdYasfnt","type":"arrow"},{"id":"BZmTNh1W-NmZpnKNsAg8b","type":"arrow"}],"updated":1669876161475,"link":null,"locked":false,"fontSize":14.39868181190029,"fontFamily":1,"text":"1","rawText":"1","baseline":13,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"1"},{"type":"text","version":291,"versionNonce":1915915521,"isDeleted":false,"id":"eF8vvNIu","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-49.29003906249994,"y":-99.5947307900434,"strokeColor":"#000000","backgroundColor":"transparent","width":25,"height":25,"seed":1001960855,"groupIds":["XTuGMrxn6Otwpjz8ioNSR"],"strokeSharpness":"sharp","boundElements":[],"updated":1669876161475,"link":null,"locked":false,"fontSize":20,"fontFamily":1,"text":"-2","rawText":"-2","baseline":18,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"-2"},{"type":"text","version":348,"versionNonce":1774813071,"isDeleted":false,"id":"1eX2ixah","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-48.29003906249994,"y":-4.668798405370609,"strokeColor":"#000000","backgroundColor":"transparent","width":23,"height":25,"seed":2019289783,"groupIds":["XTuGMrxn6Otwpjz8ioNSR"],"strokeSharpness":"sharp","boundElements":[],"updated":1669876161475,"link":null,"locked":false,"fontSize":20,"fontFamily":1,"text":"-4","rawText":"-4","baseline":18,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"-4"},{"type":"text","version":338,"versionNonce":289096929,"isDeleted":false,"id":"uqL6JY9q","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-48.79003906249994,"y":-59.30485448796003,"strokeColor":"#000000","backgroundColor":"transparent","width":24,"height":25,"seed":1001816121,"groupIds":["XTuGMrxn6Otwpjz8ioNSR"],"strokeSharpness":"sharp","boundElements":[],"updated":1669876161476,"link":null,"locked":false,"fontSize":20,"fontFamily":1,"text":"-3","rawText":"-3","baseline":18,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"-3"},{"type":"text","version":219,"versionNonce":649115055,"isDeleted":false,"id":"WcU2UzjQ","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-73.79003906249994,"y":-139.4268966608749,"strokeColor":"#000000","backgroundColor":"transparent","width":74,"height":25,"seed":1711725591,"groupIds":["XTuGMrxn6Otwpjz8ioNSR"],"strokeSharpness":"sharp","boundElements":[],"updated":1669876161476,"link":null,"locked":false,"fontSize":20,"fontFamily":1,"text":"y-speed","rawText":"y-speed","baseline":18,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"y-speed"},{"type":"text","version":322,"versionNonce":1646395585,"isDeleted":false,"id":"IrI6KQJV","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-48.29003906249994,"y":38.547635033017116,"strokeColor":"#000000","backgroundColor":"transparent","width":23,"height":25,"seed":572946999,"groupIds":["XTuGMrxn6Otwpjz8ioNSR"],"strokeSharpness":"sharp","boundElements":[],"updated":1669876161476,"link":null,"locked":false,"fontSize":20,"fontFamily":1,"text":"-5","rawText":"-5","baseline":18,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"-5"},{"type":"text","version":310,"versionNonce":1233921999,"isDeleted":false,"id":"Dtv9HTI8","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-211.4044189453125,"y":-104.82800583612351,"strokeColor":"#000000","backgroundColor":"transparent","width":88,"height":14,"seed":1940233465,"groupIds":[],"strokeSharpness":"sharp","boundElements":[],"updated":1669876161476,"link":null,"locked":false,"fontSize":11.564513367491873,"fontFamily":1,"text":"repeat 2 times","rawText":"repeat 2 times","baseline":10,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"repeat 2 times"},{"type":"text","version":327,"versionNonce":42352801,"isDeleted":false,"id":"8oL2ADB6","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-210.4044189453125,"y":-66.63830044568874,"strokeColor":"#000000","backgroundColor":"transparent","width":88,"height":14,"seed":1478327543,"groupIds":[],"strokeSharpness":"sharp","boundElements":[],"updated":1669876161476,"link":null,"locked":false,"fontSize":11.564513367491873,"fontFamily":1,"text":"repeat 3 times","rawText":"repeat 3 times","baseline":10,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"repeat 3 times"},{"type":"text","version":339,"versionNonce":7624175,"isDeleted":false,"id":"8xaobg7y","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-210.4044189453125,"y":-10.758631256235617,"strokeColor":"#000000","backgroundColor":"transparent","width":87,"height":14,"seed":1050181433,"groupIds":[],"strokeSharpness":"sharp","boundElements":[],"updated":1669876161476,"link":null,"locked":false,"fontSize":11.564513367491873,"fontFamily":1,"text":"repeat 4 times","rawText":"repeat 4 times","baseline":10,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"repeat 4 times"},{"type":"text","version":487,"versionNonce":806847617,"isDeleted":false,"id":"2lyzJYzq","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-184.4044189453125,"y":42.81446547735305,"strokeColor":"#000000","backgroundColor":"transparent","width":62,"height":14,"seed":666969721,"groupIds":[],"strokeSharpness":"sharp","boundElements":[],"updated":1669876161476,"link":null,"locked":false,"fontSize":11.564513367491873,"fontFamily":1,"text":"only once!!!","rawText":"only once!!!","baseline":10,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"only once!!!"},{"type":"text","version":423,"versionNonce":577880079,"isDeleted":false,"id":"IbInAoJb","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-278.8067321777344,"y":-99.5947307900434,"strokeColor":"#000000","backgroundColor":"transparent","width":25,"height":25,"seed":963405561,"groupIds":["L2mtHY-W5mC-w7fjiNLVf"],"strokeSharpness":"sharp","boundElements":[],"updated":1669876161476,"link":null,"locked":false,"fontSize":20,"fontFamily":1,"text":"-2","rawText":"-2","baseline":18,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"-2"},{"type":"text","version":481,"versionNonce":1184189537,"isDeleted":false,"id":"hSc6JIhn","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-277.8067321777344,"y":-4.668798405370609,"strokeColor":"#000000","backgroundColor":"transparent","width":23,"height":25,"seed":791437591,"groupIds":["L2mtHY-W5mC-w7fjiNLVf"],"strokeSharpness":"sharp","boundElements":[],"updated":1669876161476,"link":null,"locked":false,"fontSize":20,"fontFamily":1,"text":"-4","rawText":"-4","baseline":18,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"-4"},{"type":"text","version":469,"versionNonce":293398063,"isDeleted":false,"id":"VhzbCA86","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-278.3067321777344,"y":-59.30485448796003,"strokeColor":"#000000","backgroundColor":"transparent","width":24,"height":25,"seed":1897340889,"groupIds":["L2mtHY-W5mC-w7fjiNLVf"],"strokeSharpness":"sharp","boundElements":[],"updated":1669876161476,"link":null,"locked":false,"fontSize":20,"fontFamily":1,"text":"-3","rawText":"-3","baseline":18,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"-3"},{"type":"text","version":352,"versionNonce":2110724161,"isDeleted":false,"id":"QrDPRnCQ","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-303.3067321777344,"y":-139.4268966608749,"strokeColor":"#000000","backgroundColor":"transparent","width":74,"height":25,"seed":659433015,"groupIds":["L2mtHY-W5mC-w7fjiNLVf"],"strokeSharpness":"sharp","boundElements":[],"updated":1669876161476,"link":null,"locked":false,"fontSize":20,"fontFamily":1,"text":"y-speed","rawText":"y-speed","baseline":18,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"y-speed"},{"type":"text","version":455,"versionNonce":1551779919,"isDeleted":false,"id":"CPx8eJtp","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-277.8067321777344,"y":38.547635033017116,"strokeColor":"#000000","backgroundColor":"transparent","width":23,"height":25,"seed":1488436409,"groupIds":["L2mtHY-W5mC-w7fjiNLVf"],"strokeSharpness":"sharp","boundElements":[],"updated":1669876161476,"link":null,"locked":false,"fontSize":20,"fontFamily":1,"text":"-5","rawText":"-5","baseline":18,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"-5"},{"type":"text","version":233,"versionNonce":923340049,"isDeleted":false,"id":"wQFuVFii","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":0,"opacity":90,"angle":0,"x":-372.37231729544834,"y":-203.7640727434215,"strokeColor":"#000000","backgroundColor":"#15aabf","width":135,"height":28,"seed":1343495823,"groupIds":[],"strokeSharpness":"sharp","boundElements":[],"updated":1670350281802,"link":null,"locked":false,"fontSize":20,"fontFamily":1,"text":"BIG jumps ❌","rawText":"BIG jumps ❌","baseline":20,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"BIG jumps ❌"},{"type":"text","version":534,"versionNonce":1666067473,"isDeleted":false,"id":"csfpIZ0v","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":0,"opacity":90,"angle":0,"x":-143.57462243231532,"y":-203.9287469630633,"strokeColor":"#000000","backgroundColor":"#15aabf","width":160,"height":28,"seed":2028349825,"groupIds":[],"strokeSharpness":"sharp","boundElements":[],"updated":1670350305140,"link":null,"locked":false,"fontSize":20,"fontFamily":1,"text":"SMALL steps ✅","rawText":"SMALL steps ✅","baseline":20,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"SMALL steps ✅"}],"appState":{"theme":"dark","viewBackgroundColor":"transparent","currentItemStrokeColor":"#000000","currentItemBackgroundColor":"#15aabf","currentItemFillStyle":"solid","currentItemStrokeWidth":1,"currentItemStrokeStyle":"solid","currentItemRoughness":0,"currentItemOpacity":90,"currentItemFontFamily":1,"currentItemFontSize":20,"currentItemTextAlign":"left","currentItemStrokeSharpness":"sharp","currentItemStartArrowhead":null,"currentItemEndArrowhead":"arrow","currentItemLinearStrokeSharpness":"round","gridSize":null,"colorPalette":{}},"files":{}};InitialData.scrollToContent=true;App=()=>{const e=React.useRef(null),t=React.useRef(null),[n,i]=React.useState({width:void 0,height:void 0});return React.useEffect(()=>{i({width:t.current.getBoundingClientRect().width,height:t.current.getBoundingClientRect().height});const e=()=>{i({width:t.current.getBoundingClientRect().width,height:t.current.getBoundingClientRect().height})};return window.addEventListener("resize",e),()=>window.removeEventListener("resize",e)},[t]),React.createElement(React.Fragment,null,React.createElement("div",{className:"excalidraw-wrapper",ref:t},React.createElement(ExcalidrawLib.Excalidraw,{ref:e,width:n.width,height:n.height,initialData:InitialData,viewModeEnabled:!0,zenModeEnabled:!0,gridModeEnabled:!1})))},excalidrawWrapper=document.getElementById("HatlightFalllingInSteps.excalidraw.md3");ReactDOM.render(React.createElement(App),excalidrawWrapper);})();</script>

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
