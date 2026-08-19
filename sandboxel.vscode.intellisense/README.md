# Sandboxels VS Code Auto-Complete & IntelliSense

A comprehensive TypeScript declaration file (`.d.ts`) that brings smart code completion, type checking, and documentation for **550+ sandbox elements** and game APIs directly into VS Code.

## 🚀 How to Enable Auto-Complete

To activate IntelliSense in your mod, simply add this triple-slash reference to the **very first line** of your mod's `.js` file:

```javascript
/// <reference path="./sandboxel.d.ts" />
```

> ⚠️ **Important Requirement:** This works only if both your mod file (e.g., `mod.js`) and `sandboxel.d.ts` are located in the **same folder** (on the same directory level).

### 💡 Solution for Different Folders
If you want to keep `sandboxel.d.ts` in a separate folder, specify the relative path to it in the reference link. For example:

```javascript
/// <reference path="../types/sandboxel.d.ts" />
```

> **ProTip!** Enter `//@ts-check` at the first line of file to let the VS Code turn on the semantic testing. This helps you with errors in arguments, and validated other value types.

> **Warning** VS Code can't remember that you changed the JSON key. Sorry, but the suggestions will not work. e.g.
```js
/// <reference path="./sandboxel.d.ts" />
(()=>{
    /**
     * Neighbors: [x,y,liveWeight?,deadWeight?]
     */
    var lifeRules = {live:{live:[2,3]},dead:{live:[3]},neighbors:[[1,1],[1,-1],[-1,1],[-1,-1],[1,0],[-1,0],[0,1],[0,-1]]};
    elements.alive = {
        color:'#eeeeee',
        name:'Alive cell'
    }
    elements.dead = {
        color:'#888888',
        name:'Dead cell'
    }
    runEveryTick(()=>{
        const old = [...pixelMap];
        for(let i = 0; i < old.length; i++)
        for(let j = 0; j < old[i].length; j++) {
            let nCount = 0;
            for(let n of lifeRules.neighbors) {
                nCount += (outOfBounds(i+n[0],j+n[1])||(old[i+n[0]][j+n[1]]?.element=='alive')?(n[3]??0):(n[2]??1));
            }
            //@ts-ignore
            if(old[i][j]?.element==='alive' && !lifeRules.live.live.includes(nCount)) changePixel(old[i][j],"")
        };
    }
);})();
```
> It will be not suggested. VS Code will tell you about 'alive' is not in elements. Don't worry, continue writing!
