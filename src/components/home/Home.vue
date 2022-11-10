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
    // backgroundColor: 0x3ba8a1
  })

  const stage = new Container()

  const bgTexture = Texture.from('sample.jpg');
  const background = new Sprite(bgTexture);
  background.width =window.innerWidth - 20
  background.height =window.innerHeight
  stage.addChild( background );

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
    wordWrapWidth: 500
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

  const getApp = new Container()
  getApp.y = leftDescription.y + (leftDescription.height * 3)
  getApp.x = 100
  mainContainer.addChild(getApp)

  const appGraphics = new Graphics()
  appGraphics.beginFill(0xffffff);
  appGraphics.lineStyle(1, 0x000000)
  appGraphics.drawRoundedRect (0, 0, 350, 50, 300);

  getApp.addChild( appGraphics )
  
  const placeholder = new Text('Enter your mobile number', {
    align: 'center',
    fontSize: 16,
  })
  placeholder.x = 20
  placeholder.y = (appGraphics.height - placeholder.height) / 2
  getApp.addChild( placeholder )

  const appGraphics1 = new Graphics()
  appGraphics1.beginFill(0x000000);
  appGraphics1.lineStyle(1, 0x000000)
  appGraphics1.drawRoundedRect(0, 0, 100, 50, 300);
  appGraphics1.x = appGraphics.width - appGraphics1.width
  getApp.addChild( appGraphics1 )

  const appGraphic2 = new Graphics()
  appGraphic2.beginFill(0x000000);
  appGraphic2.drawRect(0, 0, 40, 50);
  appGraphic2.x = appGraphics1.x
  getApp.addChild( appGraphic2 )

  const buttonText = new Text('GET APP', {
    align: 'center',
    fontSize: 16,
    fill: 0xffffff
  })
  buttonText.x = 260
  buttonText.y =  (appGraphics.height - buttonText.height) /2
  getApp.addChild( buttonText )

  const mainRightContainer = new Container()
  mainRightContainer.x = mainLeftContainer.width
  mainRightContainer.y = 50
  mainContainer.addChild(mainRightContainer)

  
  const rightTexture = Texture.from('girl.png');
  const rightBackground = new Sprite(rightTexture);
  rightBackground.width = 500
  rightBackground.height = 600
  mainRightContainer.addChild( rightBackground );

  app.stage.addChild(stage)
  body.appendChild(app.view)
})


</script>

<template>
  <div class="badugi-inner">
  </div>
</template>

