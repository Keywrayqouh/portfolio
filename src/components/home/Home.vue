<script setup>
import { onMounted, watch } from 'vue'
import { Application, Texture, Container, Sprite, Text, Graphics } from 'pixi.js';
import gsap from "gsap";

onMounted(async () => {
  const body = document.querySelector('.badugi-inner')

  const app = new Application({
    width: window.innerWidth - 20,
    height: window.innerHeight,
    backgroundColor: 0x3ba8a1
  })

  const stage = new Container()

  // const bgTexture = Texture.from('bg.jpg');
  // const background = new Sprite(bgTexture);
  // background.width =window.innerWidth - 20
  // background.height =window.innerHeight - 20
  // stage.addChild( background );

  const headerContainer = new Container()
  headerContainer.width = window.innerWidth - 20
  headerContainer.height = 50
  stage.addChild( headerContainer )

  const graphics = new Graphics();
  graphics.beginFill(0xFFFFFF);
  graphics.drawRect(0, 0, window.innerWidth - 20 ,50);
  headerContainer.addChild( graphics)

  const titleName = new Text('Mellyne Grace Nadela', {
    fontFamily: 'Arial',
    fontSize: 24,
    fill: 0x000000,
    align: 'center',
    fontWeight: 'bold'
  });
  headerContainer.addChild( titleName)
  titleName.x = 100
  titleName.y = (headerContainer.height - titleName.height) / 2
  gsap.from(titleName, {duration: 2, y: 0, ease: "myBounce"});
  gsap.to(titleName, {duration: 2, scaleX: 1.8, scaleY: 0.6, ease: "myBounce-squash", transformOrigin: "center bottom"});


  const menus = new Container()
  menus.x = titleName.width + titleName.x
  const menuList = [
    { name: 'Home'},
    { name: 'About'},
    { name: 'Portfolio'},
    { name: 'Resume'},
    { name: 'Contact'},
  ]

  for (let menu = 0; menu < menuList.length; menu++) {
    const element = menuList[menu];

    const itemContainer = new Container()
    menus.addChild( itemContainer )

    const itemText = new Text(element.name, {
      fontFamily: 'Arial',
      fontSize: 16,
      fill: 0x000000,
      align: 'center',
      fontWeight: 'bold',
    })
    itemText.x = (itemContainer.width - itemText.width) / 2
    itemText.y = (headerContainer.height - itemText.height) / 2
    itemContainer.addChild( itemText )

    itemContainer.x = (100 * menu) + (menu ? 40 : 50)

    console.log(itemContainer.x);

    gsap.from(itemContainer, {duration: 1, y: -200, ease: "myBounce"});
    gsap.to(itemContainer, {duration: 1, scaleX: 1.4, scaleY: 0.6, ease: "myBounce-squash", transformOrigin: "center bottom"});
  }
  headerContainer.addChild( menus )

  app.stage.addChild(stage)
  body.appendChild(app.view)
})


</script>

<template>
  <div class="badugi-inner">
  </div>
</template>

