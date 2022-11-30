---
{"dg-publish":true,"permalink":"/digital-garden/torchlight-platformer-part-1-first-class/"}
---

 
# Torchlight Platformer Part 1, First Class

## Create Hitbox
As always, start by creating your main sprite, which I am calling **hitbox**[^1] and initializing hitbox and your project's variables. 
* In this case, it is important that **hitbox is just a square**. Later, we will make it have a real costume, but for now, just a square.

<style>
.container {font-family: sans-serif; text-align: center;}
.button-wrapper button {z-index: 1;height: 40px; width: 100px; margin: 10px;padding: 5px;}
.excalidraw .App-menu_top .buttonList { display: flex;}
.excalidraw-wrapper { height: 800px; margin: 50px; position: relative;}
:root[dir="ltr"] .excalidraw .layer-ui__wrapper .zen-mode-transition.App-menu_bottom--transition-left {transform: none;}
</style><script src="https://unpkg.com/react@17/umd/react.production.min.js"></script><script src="https://unpkg.com/react-dom@17/umd/react-dom.production.min.js"></script><script type="text/javascript" src="https://unpkg.com/@excalidraw/excalidraw@0.12.0/dist/excalidraw.production.min.js"></script><div id="HatlightMainspriteexcalidraw.md1"></div><script>(function(){const InitialData={"type":"excalidraw","version":2,"source":"https://excalidraw.com","elements":[{"type":"rectangle","version":89,"versionNonce":2123033571,"isDeleted":false,"id":"KRN322rUgILzyqnIiAh0-","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":0,"opacity":100,"angle":0,"x":-588.4230346679688,"y":-174.70481872558594,"strokeColor":"#000000","backgroundColor":"#15aabf","width":580.8837890625,"height":330.75030517578125,"seed":1997566463,"groupIds":[],"strokeSharpness":"sharp","boundElements":[],"updated":1669338857461,"link":null,"locked":false},{"type":"rectangle","version":108,"versionNonce":1067289485,"isDeleted":false,"id":"hQZ7dFkbQxz1MSzeq2DS2","fillStyle":"solid","strokeWidth":1,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-531.61865234375,"y":48.407012939453125,"strokeColor":"#000000","backgroundColor":"#4c6ef5","width":57.265625,"height":54.74920654296875,"seed":1431296543,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1669338862018,"link":null,"locked":false}],"appState":{"theme":"dark","viewBackgroundColor":"transparent","currentItemStrokeColor":"#000000","currentItemBackgroundColor":"#15aabf","currentItemFillStyle":"solid","currentItemStrokeWidth":1,"currentItemStrokeStyle":"solid","currentItemRoughness":1,"currentItemOpacity":100,"currentItemFontFamily":1,"currentItemFontSize":20,"currentItemTextAlign":"left","currentItemStrokeSharpness":"sharp","currentItemStartArrowhead":null,"currentItemEndArrowhead":"arrow","currentItemLinearStrokeSharpness":"round","gridSize":null,"colorPalette":{}},"files":{}};InitialData.scrollToContent=true;App=()=>{const e=React.useRef(null),t=React.useRef(null),[n,i]=React.useState({width:void 0,height:void 0});return React.useEffect(()=>{i({width:t.current.getBoundingClientRect().width,height:t.current.getBoundingClientRect().height});const e=()=>{i({width:t.current.getBoundingClientRect().width,height:t.current.getBoundingClientRect().height})};return window.addEventListener("resize",e),()=>window.removeEventListener("resize",e)},[t]),React.createElement(React.Fragment,null,React.createElement("div",{className:"excalidraw-wrapper",ref:t},React.createElement(ExcalidrawLib.Excalidraw,{ref:e,width:n.width,height:n.height,initialData:InitialData,viewModeEnabled:!0,zenModeEnabled:!0,gridModeEnabled:!1})))},excalidrawWrapper=document.getElementById("HatlightMainspriteexcalidraw.md1");ReactDOM.render(React.createElement(App),excalidrawWrapper);})();</script>

## Initialize the hitbox
- Initialize usually means things like **position**, **direction**, and **effects**. You will also initialize all your **variables**. 
- At the start you don't always know all your variables, but as this is a platformer, we know we will need `x speed `and `y speed`, so let's initialize those.
- To set the **position**, use this trick: Put your sprite at the starting position in the stage. Then find the `go to x` block in the block area, and scratch will put the correct numbers in the block.

This is what we get:

```ad-scratch
title: main sprite
~~~scratchblock

when @greenFlag clicked
broadcast [initialize v]


when I receive [initialize v]
set [ghost v] effect to (0)::looks
go to x: (-205) y: (65)
set [x speed v] to [0]
set [y speed v] to [0]
~~~
```

After we initialize, we 
- move left right, 
- then fall, 
- then repeat.

## Flowchart for the project
The flowchart for this is:

<div id="HatlightOverallexcalidraw.md2"></div><script>(function(){const InitialData={"type":"excalidraw","version":2,"source":"https://excalidraw.com","elements":[{"type":"rectangle","version":1613,"versionNonce":1531498787,"isDeleted":false,"id":"RMNqwfWlgfbMpYooeJoeX","fillStyle":"solid","strokeWidth":2,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-327.07861963655523,"y":-1171.2797250196272,"strokeColor":"#5f3dc4","backgroundColor":"#fd7e14","width":145,"height":48,"seed":1239531121,"groupIds":[],"strokeSharpness":"round","boundElements":[{"id":"bLuBw5Gk","type":"text"},{"id":"CZZBlZLQcMsvBM3Y59OCy","type":"arrow"}],"updated":1669340477775,"link":null,"locked":false},{"type":"text","version":1757,"versionNonce":2000848525,"isDeleted":false,"id":"bLuBw5Gk","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-314.07861963655523,"y":-1159.2797250196272,"strokeColor":"#5f3dc4","backgroundColor":"transparent","width":119,"height":24,"seed":217341215,"groupIds":[],"strokeSharpness":"sharp","boundElements":[],"updated":1669340477776,"link":null,"locked":false,"fontSize":20,"fontFamily":3,"text":"Green Flag","rawText":"Green Flag","baseline":20,"textAlign":"center","verticalAlign":"middle","containerId":"RMNqwfWlgfbMpYooeJoeX","originalText":"Green Flag"},{"type":"rectangle","version":1785,"versionNonce":668755833,"isDeleted":false,"id":"3KIpf-rkzikNMb_aR0m7y","fillStyle":"solid","strokeWidth":2,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-327.87772088228417,"y":-1083.5863582106383,"strokeColor":"#5f3dc4","backgroundColor":"#fd7e14","width":152,"height":34,"seed":820168785,"groupIds":[],"strokeSharpness":"round","boundElements":[{"id":"ZCCwgZWZ","type":"text"},{"id":"CZZBlZLQcMsvBM3Y59OCy","type":"arrow"},{"id":"ZGWdRa8JACOlC9W9gZeZ8","type":"arrow"}],"updated":1668911234444,"link":null,"locked":false},{"type":"text","version":1924,"versionNonce":538618007,"isDeleted":false,"id":"ZCCwgZWZ","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-311.37772088228417,"y":-1078.5863582106383,"strokeColor":"#5f3dc4","backgroundColor":"transparent","width":119,"height":24,"seed":1506369855,"groupIds":[],"strokeSharpness":"sharp","boundElements":[],"updated":1668911234444,"link":null,"locked":false,"fontSize":20,"fontFamily":3,"text":"Initialize","rawText":"Initialize","baseline":20,"textAlign":"center","verticalAlign":"middle","containerId":"3KIpf-rkzikNMb_aR0m7y","originalText":"Initialize"},{"type":"rectangle","version":1771,"versionNonce":45289561,"isDeleted":false,"id":"g3GQAZzBP1tmYREzU3GFV","fillStyle":"solid","strokeWidth":2,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-351.870717277047,"y":-1009.0037078852681,"strokeColor":"#5f3dc4","backgroundColor":"#fd7e14","width":206,"height":34,"seed":182949425,"groupIds":[],"strokeSharpness":"round","boundElements":[{"id":"y03U4cUU","type":"text"},{"id":"ZGWdRa8JACOlC9W9gZeZ8","type":"arrow"},{"id":"SgfLADjg34eKJoEx705pv","type":"arrow"},{"id":"rOdClYNLCyfLF1jbUwU8F","type":"arrow"}],"updated":1668911234444,"link":null,"locked":false},{"type":"text","version":1915,"versionNonce":34045367,"isDeleted":false,"id":"y03U4cUU","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-337.870717277047,"y":-1004.0037078852681,"strokeColor":"#5f3dc4","backgroundColor":"transparent","width":178,"height":24,"seed":698933599,"groupIds":[],"strokeSharpness":"sharp","boundElements":[],"updated":1668911234444,"link":null,"locked":false,"fontSize":20,"fontFamily":3,"text":"Move Left right","rawText":"Move Left right","baseline":20,"textAlign":"center","verticalAlign":"middle","containerId":"g3GQAZzBP1tmYREzU3GFV","originalText":"Move Left right"},{"type":"rectangle","version":1996,"versionNonce":1516184547,"isDeleted":false,"id":"sRV2I3u5YmLmW1mMZtcg3","fillStyle":"solid","strokeWidth":2,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-302.20735670997453,"y":-913.0437352520836,"strokeColor":"#5f3dc4","backgroundColor":"#fd7e14","width":92,"height":34,"seed":1255647249,"groupIds":[],"strokeSharpness":"round","boundElements":[{"id":"XFDnTuBL","type":"text"},{"id":"SgfLADjg34eKJoEx705pv","type":"arrow"},{"id":"rOdClYNLCyfLF1jbUwU8F","type":"arrow"}],"updated":1669340484981,"link":null,"locked":false},{"type":"text","version":2129,"versionNonce":1501544397,"isDeleted":false,"id":"XFDnTuBL","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-280.70735670997453,"y":-908.0437352520836,"strokeColor":"#5f3dc4","backgroundColor":"transparent","width":49,"height":24,"seed":769875327,"groupIds":[],"strokeSharpness":"sharp","boundElements":[],"updated":1669340484981,"link":null,"locked":false,"fontSize":20,"fontFamily":3,"text":"Fall","rawText":"Fall","baseline":20,"textAlign":"center","verticalAlign":"middle","containerId":"sRV2I3u5YmLmW1mMZtcg3","originalText":"Fall"},{"type":"arrow","version":1362,"versionNonce":934030573,"isDeleted":false,"id":"CZZBlZLQcMsvBM3Y59OCy","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-253.4290227195139,"y":-1122.2797250196272,"strokeColor":"#e67700","backgroundColor":"transparent","width":2.2593013004079125,"height":37.69336680898891,"seed":447380977,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1669340477776,"link":null,"locked":false,"startBinding":{"elementId":"RMNqwfWlgfbMpYooeJoeX","gap":1,"focus":-0.03564957328353111},"endBinding":{"elementId":"3KIpf-rkzikNMb_aR0m7y","gap":1,"focus":-0.06348442400404053},"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[-2.2593013004079125,37.69336680898891]]},{"type":"arrow","version":1739,"versionNonce":421711267,"isDeleted":false,"id":"ZGWdRa8JACOlC9W9gZeZ8","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-259.428156359733,"y":-1048.5863582106383,"strokeColor":"#e67700","backgroundColor":"transparent","width":0.23951808540243746,"height":38.582650325370196,"seed":431576479,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1669340474453,"link":null,"locked":false,"startBinding":{"elementId":"3KIpf-rkzikNMb_aR0m7y","gap":1,"focus":0.09774181347325406},"endBinding":{"elementId":"g3GQAZzBP1tmYREzU3GFV","gap":1,"focus":-0.10580130154277227},"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[-0.23951808540243746,38.582650325370196]]},{"type":"arrow","version":1571,"versionNonce":1146865443,"isDeleted":false,"id":"rOdClYNLCyfLF1jbUwU8F","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-255.8599126359509,"y":-974.0037078852681,"strokeColor":"#e67700","backgroundColor":"transparent","width":1.0056080452798994,"height":59.89627715498432,"seed":2036832209,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1669340484982,"link":null,"locked":false,"startBinding":{"elementId":"g3GQAZzBP1tmYREzU3GFV","focus":0.07081131742136672,"gap":1},"endBinding":{"elementId":"sRV2I3u5YmLmW1mMZtcg3","focus":0.035785059455317375,"gap":1.0636954782002022},"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[1.0056080452798994,59.89627715498432]]},{"type":"arrow","version":3073,"versionNonce":1328983939,"isDeleted":false,"id":"SgfLADjg34eKJoEx705pv","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-250.5639760769339,"y":-877.4550336065713,"strokeColor":"#e67700","backgroundColor":"transparent","width":125.88014104754569,"height":130.68243448093324,"seed":1763690303,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1669340484982,"link":null,"locked":false,"startBinding":{"elementId":"sRV2I3u5YmLmW1mMZtcg3","gap":1.5887016455122875,"focus":0.2823770877995944},"endBinding":{"elementId":"g3GQAZzBP1tmYREzU3GFV","gap":2.713513145805365,"focus":-0.9124661334787617},"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[28.644564085615173,21.197090287284823],[110.49562485927345,2.7482281527666146],[125.88014104754569,-77.08036335357099],[107.40677194569227,-109.48534419364842]]}],"appState":{"theme":"dark","viewBackgroundColor":"transparent","currentItemStrokeColor":"#e67700","currentItemBackgroundColor":"transparent","currentItemFillStyle":"hachure","currentItemStrokeWidth":1,"currentItemStrokeStyle":"solid","currentItemRoughness":1,"currentItemOpacity":100,"currentItemFontFamily":3,"currentItemFontSize":20,"currentItemTextAlign":"left","currentItemStrokeSharpness":"sharp","currentItemStartArrowhead":null,"currentItemEndArrowhead":"arrow","currentItemLinearStrokeSharpness":"round","gridSize":null,"colorPalette":{}},"files":{}};InitialData.scrollToContent=true;App=()=>{const e=React.useRef(null),t=React.useRef(null),[n,i]=React.useState({width:void 0,height:void 0});return React.useEffect(()=>{i({width:t.current.getBoundingClientRect().width,height:t.current.getBoundingClientRect().height});const e=()=>{i({width:t.current.getBoundingClientRect().width,height:t.current.getBoundingClientRect().height})};return window.addEventListener("resize",e),()=>window.removeEventListener("resize",e)},[t]),React.createElement(React.Fragment,null,React.createElement("div",{className:"excalidraw-wrapper",ref:t},React.createElement(ExcalidrawLib.Excalidraw,{ref:e,width:n.width,height:n.height,initialData:InitialData,viewModeEnabled:!0,zenModeEnabled:!0,gridModeEnabled:!1})))},excalidrawWrapper=document.getElementById("HatlightOverallexcalidraw.md2");ReactDOM.render(React.createElement(App),excalidrawWrapper);})();</script>


*Move left/right* is the start of a **loop**. After *Fall*, it goes back to the beginning at Left/right. In this case the loop goes forever.

So, let's put in  left/right and fall stacks.

```ad-scratch
title: main sprite
~~~scratchblock
when @greenFlag clicked
broadcast [initialize v]


when I receive [initialize v]
...
broadcast [move left / right v]

when I receive [move left / right v]
broadcast [fall v]


when I receive [fall v]
broadcast [move left / right v]

~~~
```

## Left/Right 
So let's do the left right routine. In words, the basic routine is this:

<div id="HatlightmoveLeftRight.excalidraw.md3"></div><script>(function(){const InitialData={"type":"excalidraw","version":2,"source":"https://excalidraw.com","elements":[{"type":"rectangle","version":2483,"versionNonce":1247119587,"isDeleted":false,"id":"j46Q-mIB_RMtLqBuMi9Jo","fillStyle":"solid","strokeWidth":2,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-333.2813200409966,"y":-457.07274754709914,"strokeColor":"#5f3dc4","backgroundColor":"#fd7e14","width":418,"height":58,"seed":216207345,"groupIds":[],"strokeSharpness":"round","boundElements":[{"id":"hoKKMoqj","type":"text"}],"updated":1669342606930,"link":null,"locked":false},{"type":"text","version":2696,"versionNonce":135477699,"isDeleted":false,"id":"hoKKMoqj","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-328.7813200409966,"y":-452.07274754709914,"strokeColor":"#5f3dc4","backgroundColor":"transparent","width":409,"height":48,"seed":1921704863,"groupIds":[],"strokeSharpness":"sharp","boundElements":[],"updated":1669342586279,"link":null,"locked":false,"fontSize":20,"fontFamily":3,"text":"Detect arrows and set the x-speed \nvariable","rawText":"Detect arrows and set the x-speed variable","baseline":44,"textAlign":"center","verticalAlign":"middle","containerId":"j46Q-mIB_RMtLqBuMi9Jo","originalText":"Detect arrows and set the x-speed variable"},{"type":"rectangle","version":2742,"versionNonce":310883427,"isDeleted":false,"id":"IoJwQQFPcnide1ayTmbpU","fillStyle":"solid","strokeWidth":2,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-301.7813200409966,"y":-368.63565331462917,"strokeColor":"#5f3dc4","backgroundColor":"#fd7e14","width":355,"height":58,"seed":2059266513,"groupIds":[],"strokeSharpness":"round","boundElements":[{"id":"KNDBm7n1","type":"text"},{"id":"BQTp2Km0sXOdqGU8mgJqd","type":"arrow"}],"updated":1669342631811,"link":null,"locked":false},{"type":"text","version":2895,"versionNonce":250518765,"isDeleted":false,"id":"KNDBm7n1","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-297.2813200409966,"y":-363.63565331462917,"strokeColor":"#5f3dc4","backgroundColor":"transparent","width":346,"height":48,"seed":130750399,"groupIds":[],"strokeSharpness":"sharp","boundElements":[],"updated":1669342631811,"link":null,"locked":false,"fontSize":20,"fontFamily":3,"text":"Keep x-speed below a maximum \nspeed","rawText":"Keep x-speed below a maximum speed","baseline":44,"textAlign":"center","verticalAlign":"middle","containerId":"IoJwQQFPcnide1ayTmbpU","originalText":"Keep x-speed below a maximum speed"},{"type":"rectangle","version":2688,"versionNonce":1182008749,"isDeleted":false,"id":"ABGizyKxq-GGhHL1bSIUj","fillStyle":"solid","strokeWidth":2,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-225.7813200409966,"y":-276.7620826530891,"strokeColor":"#5f3dc4","backgroundColor":"#fd7e14","width":203,"height":58,"seed":2145552305,"groupIds":[],"strokeSharpness":"round","boundElements":[{"id":"llvdtr75","type":"text"},{"id":"dKCsiULa4aCptAMA4JZvi","type":"arrow"},{"id":"BQTp2Km0sXOdqGU8mgJqd","type":"arrow"},{"id":"3kD_5vABuaYS-50Mz2okq","type":"arrow"}],"updated":1669342631811,"link":null,"locked":false},{"type":"text","version":2878,"versionNonce":83439619,"isDeleted":false,"id":"llvdtr75","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-221.2813200409966,"y":-271.7620826530891,"strokeColor":"#5f3dc4","backgroundColor":"transparent","width":194,"height":48,"seed":1261422559,"groupIds":[],"strokeSharpness":"sharp","boundElements":[],"updated":1669342631811,"link":null,"locked":false,"fontSize":20,"fontFamily":3,"text":"change x by \nx-speed","rawText":"change x by x-speed","baseline":44,"textAlign":"center","verticalAlign":"middle","containerId":"ABGizyKxq-GGhHL1bSIUj","originalText":"change x by x-speed"},{"type":"rectangle","version":2570,"versionNonce":783895363,"isDeleted":false,"id":"ZLp42ksZ46S107PNBhQAh","fillStyle":"solid","strokeWidth":2,"strokeStyle":"solid","roughness":2,"opacity":100,"angle":0,"x":-162.2813200409966,"y":-182.18015978307884,"strokeColor":"#5f3dc4","backgroundColor":"#fd7e14","width":76,"height":34,"seed":376990097,"groupIds":[],"strokeSharpness":"round","boundElements":[{"id":"7coyg3pg","type":"text"},{"id":"dKCsiULa4aCptAMA4JZvi","type":"arrow"},{"id":"3kD_5vABuaYS-50Mz2okq","type":"arrow"}],"updated":1669342631811,"link":null,"locked":false},{"type":"text","version":2713,"versionNonce":513853453,"isDeleted":false,"id":"7coyg3pg","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-148.7813200409966,"y":-177.18015978307884,"strokeColor":"#5f3dc4","backgroundColor":"transparent","width":49,"height":24,"seed":2060022783,"groupIds":[],"strokeSharpness":"sharp","boundElements":[],"updated":1669342631811,"link":null,"locked":false,"fontSize":20,"fontFamily":3,"text":"Fall","rawText":"Fall","baseline":20,"textAlign":"center","verticalAlign":"middle","containerId":"ZLp42ksZ46S107PNBhQAh","originalText":"Fall"},{"type":"arrow","version":2879,"versionNonce":751189613,"isDeleted":false,"id":"dKCsiULa4aCptAMA4JZvi","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-124.01397947517343,"y":-145.517117753767,"strokeColor":"#e67700","backgroundColor":"transparent","width":0.28874846551465794,"height":0.1462436558385889,"seed":166066513,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1669342631811,"link":null,"locked":false,"startBinding":{"elementId":"ZLp42ksZ46S107PNBhQAh","gap":3.1878291699105725,"focus":0.026503790986018495},"endBinding":{"elementId":"ZLp42ksZ46S107PNBhQAh","gap":1.0333333333333334,"focus":-0.03069383178984822},"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[-0.28874846551465794,-0.1462436558385889]]},{"type":"arrow","version":2373,"versionNonce":1973896387,"isDeleted":false,"id":"BXhvDQHmQzR-Mp2WdIDRD","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-124.56009098516891,"y":-397.85085198848293,"strokeColor":"#e67700","backgroundColor":"transparent","width":0,"height":27.782745361328125,"seed":1288981813,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1669342631811,"link":null,"locked":false,"startBinding":null,"endBinding":null,"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[0,27.782745361328125]]},{"type":"arrow","version":2412,"versionNonce":38172493,"isDeleted":false,"id":"BQTp2Km0sXOdqGU8mgJqd","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-124.96984034609525,"y":-310.1957663970771,"strokeColor":"#e67700","backgroundColor":"transparent","width":0.01183763971259566,"height":32.57754501158621,"seed":323426581,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1669342631811,"link":null,"locked":false,"startBinding":{"elementId":"IoJwQQFPcnide1ayTmbpU","focus":-0.0042626224508648895,"gap":3.15618896484375},"endBinding":{"elementId":"ABGizyKxq-GGhHL1bSIUj","focus":0.005809692111724222,"gap":3.2554103051411403},"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[0.01183763971259566,32.57754501158621]]},{"type":"arrow","version":1688,"versionNonce":251279267,"isDeleted":false,"id":"3kD_5vABuaYS-50Mz2okq","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"angle":0,"x":-124.95193707600501,"y":-216.8726133364072,"strokeColor":"#e67700","backgroundColor":"transparent","width":0.007373942970190228,"height":32.4190673828125,"seed":1637309077,"groupIds":[],"strokeSharpness":"round","boundElements":[],"updated":1669342631811,"link":null,"locked":false,"startBinding":{"elementId":"ABGizyKxq-GGhHL1bSIUj","focus":-0.0004688343721599147,"gap":3.3189400973726606},"endBinding":{"elementId":"ZLp42ksZ46S107PNBhQAh","focus":0.007914750444716614,"gap":2.51663852016722},"lastCommittedPoint":null,"startArrowhead":null,"endArrowhead":"arrow","points":[[0,0],[-0.007373942970190228,32.4190673828125]]}],"appState":{"theme":"dark","viewBackgroundColor":"transparent","currentItemStrokeColor":"#e67700","currentItemBackgroundColor":"transparent","currentItemFillStyle":"solid","currentItemStrokeWidth":1,"currentItemStrokeStyle":"solid","currentItemRoughness":1,"currentItemOpacity":100,"currentItemFontFamily":3,"currentItemFontSize":20,"currentItemTextAlign":"center","currentItemStrokeSharpness":"sharp","currentItemStartArrowhead":null,"currentItemEndArrowhead":"arrow","currentItemLinearStrokeSharpness":"round","gridSize":null,"colorPalette":{}},"files":{}};InitialData.scrollToContent=true;App=()=>{const e=React.useRef(null),t=React.useRef(null),[n,i]=React.useState({width:void 0,height:void 0});return React.useEffect(()=>{i({width:t.current.getBoundingClientRect().width,height:t.current.getBoundingClientRect().height});const e=()=>{i({width:t.current.getBoundingClientRect().width,height:t.current.getBoundingClientRect().height})};return window.addEventListener("resize",e),()=>window.removeEventListener("resize",e)},[t]),React.createElement(React.Fragment,null,React.createElement("div",{className:"excalidraw-wrapper",ref:t},React.createElement(ExcalidrawLib.Excalidraw,{ref:e,width:n.width,height:n.height,initialData:InitialData,viewModeEnabled:!0,zenModeEnabled:!0,gridModeEnabled:!1})))},excalidrawWrapper=document.getElementById("HatlightmoveLeftRight.excalidraw.md3");ReactDOM.render(React.createElement(App),excalidrawWrapper);})();</script>


The first 2 parts will be simple **myblocks**. 

> [!info] About myblocks
> Myblocks come in 2 parts, the definition block and the call block.
> To make a **simple definition myblock**:
> - In the block area, click `Make a Block`,
> - Fill in the name of the myblock (see the description below)
> - Decide if you want it to run with or without screen refresh. In our case we want them to run with screen refresh.
> - Click ok
> This will automatically create the definition block and put the call block in your block area (the area you get blocks from)
> - Find the call block in the block area,
> - This is what you actually use to call the myblock in your code.
> - Drag it into the stack

The last 2 are ordinary blocks. Here is the code:

```ad-scratch
title: hitbox, receive left/right
~~~scratchblock
when I receive [move left / right v]
set xspeed::custom
keep speed below max::custom
change x by (x speed)
broadcast [fall v]
~~~
```

Let's code two myblocks.

### Set xspeed myblock

Setting the xspeed has 2 steps. We start with an if/else block.
       - If no key is being held, then slow the speed down. 
       - How? There are 2 directions:
      	Let's say we are going **right**
	      	Our speed is +2. 
               The positive sign (+) tells us our direction is right.The 2 is how fast. 
               To slow down, we change the 2 to 1, but keep the +, since the direction is the same.
               In other words: +2 becomes +1. We **subtract 1**.
      	Let's say we are going **left**
      		Our speed is -2.  
      		How fast is still 2, but the negative sign (-) tells us the direction is left.
      		Slowing down means the 2 becomes a 1. But the direction stays the same, so we keep the negative sign.
      		In other words, -2 becomes -1. We **add 1**.
      	In other words: 
				*right* **-1**
				*left* **+1** 
			In other words:  
				(left) speed **less** (<) **than** 0 is **+1** 
				(right) speed **greater** (>) **than** 0 is **-1** 

```ad-scratch
title: hitbox, define set xspeed
~~~scratchblock
define set xspeed
if <<not <key [left arrow v] pressed?>> and <not <key [right arrow v] pressed?>>> then
left
if <(x speed) < (0)> then
      change (x speed) by (1)
      end
right
if <(x speed) > (0)> then
      change (x speed) by (-1)
      end
else
end
~~~
```

(Below, I have given a way to put all this in one line.[^2] One line, without the if, is faster, so in big games it is better.)

You are done for this class. Next is [[Digital Garden/Torchlight Platformer Part 1, Second Class|Torchlight Platformer Part 1, Second Class]]

---

##### Footnotes:

[^1]: The reason will become clear later.
[^2]: Add the two conditions together (left - right)  to get:
	```ad-scratch
	~~~scratchblock
	define set xspeed
	if <<not <key [left arrow v] pressed?>> and <not <key [right arrow v] pressed?>>> then
	  left - right
	  change [x speed v] by (<(x speed) \< [0]> - <(x speed) \> [0]>)
	else
	end
	~~~
	```
