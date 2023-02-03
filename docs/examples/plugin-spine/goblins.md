---
hide_table_of_contents: true
---

# Goblin

```js playground
import * as PIXI from 'pixi.js';

const app = new PIXI.Application<HTMLCanvasElement>({ resizeTo: window });
document.body.appendChild(app.view);

// load spine data
app.loader
    .add('goblins', 'https://v2-pixijs.com/assets/pixi-spine/goblins.json')
    .load(onAssetsLoaded);

app.stage.interactive = true;
app.stage.cursor = 'pointer';

function onAssetsLoaded(loader, res) {
    const goblin = new PIXI.spine.Spine(res.goblins.spineData);

    // set current skin
    goblin.skeleton.setSkinByName('goblin');
    goblin.skeleton.setSlotsToSetupPose();

    // set the position
    goblin.x = 400;
    goblin.y = 600;

    goblin.scale.set(1.5);

    // play animation
    goblin.state.setAnimation(0, 'walk', true);

    app.stage.addChild(goblin);

    app.stage.on('pointertap', () => {
    // change current skin
        const currentSkinName = goblin.skeleton.skin.name;
        const newSkinName = (currentSkinName === 'goblin' ? 'goblingirl' : 'goblin');
        goblin.skeleton.setSkinByName(newSkinName);
        goblin.skeleton.setSlotsToSetupPose();
    });
}
```