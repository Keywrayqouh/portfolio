<script setup>
import { onMounted, watch } from 'vue'
import { Application, Texture, Container, Sprite, Rectangle } from 'pixi.js';

onMounted(async () => {

 const canvasModel = {
        width: 1200,
        height: 815
      }

    const body = document.querySelector('#app')

    const app = new Application({
      width: window.innerWidth - 20,
      height: window.innerHeight,
      // backgroundColor: 0x000000
    })

    const stage = new Container()

    const landscapeTexture = Texture.from('bg.jpg');
    console.log(app);
    
    
    // const texture2 = new Texture(landscapeTexture, new Rectangle(0, 100, 960, 50));
    
    // new sprite
    const background = new Sprite(landscapeTexture);
    
    background.width =window.innerWidth - 20
    background.height =window.innerHeight - 20

  background.anchor.x = 0;
  background.anchor.y = 0;

  background.position.x = 0;
  background.position.y = 0;

  stage.addChild( background );

  app.stage.addChild(stage)


  body.appendChild(app.view)
})


</script>

<template>
  <div class="badugi-inner">
  </div>
</template>

