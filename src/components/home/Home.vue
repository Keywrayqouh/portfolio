<script setup>
import { onMounted, watch } from 'vue'
import { Application, Texture, Container, Sprite, Text, Graphics, TextStyle } from 'pixi.js';
import gsap from "gsap";

onMounted(async () => {
  const body = document.querySelector('.badugi-inner')
  const padding = 300

  const appConfig = {
    width: window.innerWidth - 20,
    height: window.innerHeight,
  }

  const app = new Application({
    width: appConfig.width,
    height: appConfig.height,
    backgroundColor: 0x3ba8a1
  })

  const stage = new Container()

  // const bgTexture = Texture.from('bg.jpg');
  // const background = new Sprite(bgTexture);
  // background.width =window.innerWidth - 20
  // background.height =window.innerHeight - 20
  // stage.addChild( background );

  const headerContainer = new Container()
  headerContainer.width = appConfig.width
  headerContainer.height = 50
  stage.addChild( headerContainer )

  const graphics = new Graphics();
  graphics.beginFill(0xFFFFFF);
  graphics.drawRect(0, 0, window.innerWidth - 20 ,50);
  headerContainer.addChild( graphics)

  const style = new TextStyle({
    fill: [
        "#026674",
        "#2ec2c0"
    ],
    fontFamily: "Comic Sans MS",
    fontSize: 30,
    fontWeight: "bolder",
    stroke: "#0b4a65",
    strokeThickness: 4,
});

  const titleName = new Text('Mellyne Grace', style);
  headerContainer.addChild( titleName)
  titleName.x =  padding
  titleName.y = (headerContainer.height - titleName.height) / 2 - 7
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
    itemContainer.x = (itemContainer.width - itemText.width) / 2
    itemContainer.y = (headerContainer.height - itemText.height) / 2
    itemContainer.addChild( itemText )

    itemContainer.x = (100 * menu) + (menu ? 40 : 50)

    console.log(itemContainer.x);

    gsap.from(itemContainer, {duration: 1, y: -200, ease: "myBounce"});
    gsap.to(itemContainer, {duration: 1, scaleX: 1.4, scaleY: 0.6, ease: "myBounce-squash", transformOrigin: "center bottom"});
  }
  headerContainer.addChild( menus )


  // main container

  const mainContainer = new Container
  mainContainer.y = headerContainer.height
  mainContainer.x = padding
  stage.addChild( mainContainer )

  const mainBg = new Graphics();
  mainBg.beginFill(0xFFFFFF);
  mainBg.drawRoundedRect (0, 0, appConfig.width - (padding * 2), appConfig.height - headerContainer.height, 30);
  mainContainer.addChild( mainBg)


  const mainLeftContainer = new Container()
  mainLeftContainer.x = 100
  mainLeftContainer.y = 50
  mainContainer.addChild(mainLeftContainer)

  const leftStyle = new TextStyle({
    fontFamily: "\"Palatino Linotype\", \"Book Antiqua\", Palatino, serif",
    fontSize: 64,
    padding: 5,
    textBaseline: "middle",
    align: "left",
    breakWords: true,
    fontWeight: 'bold',
    padding: 20,
    wordWrap: true,
    wordWrapWidth: mainContainer.width / 3
  });

  const leftText = new Text(`Youre journey to better credit starts here`, leftStyle);
  mainLeftContainer.addChild(leftText)

  const descStyle = new TextStyle({
    align: "center",
    breakWords: true,
    dropShadowAlpha: 40,
    dropShadowAngle: 12.9,
    dropShadowDistance: 10,
    fontSize: 24,
    fontWeight: "bold",
    lineHeight: "",
    padding: 5,
    textBaseline: "middle",
    wordWrap: true,
    wordWrapWidth: 680,
    align: "left",
  })

  const leftDescription = new Text(`Think the credit system is stacked against you? So do we, We'll help you get the credit you deserve.`, descStyle)
  leftDescription.y = leftText.height + 20
  mainLeftContainer.addChild(leftDescription)

  app.stage.addChild(stage)
  body.appendChild(app.view)
})


</script>

<template>
  <div class="badugi-inner">
  </div>
</template>

