---
title: 'Limejs 中文指南 #1 The Timeline'
tags:
  - Javascript
  - js
  - lime
  - 游戏开发
url: 518.html
id: 518
categories:
  - 游戏制作
date: 2013-01-05 15:35:26
---

时间轴 Director 一切都从Director开始，Director是所有游戏都需要的基础对象，它把所有LimeJS的逻辑连接到了网页上的单独空间。如果你熟悉flash的话，你可以把它当作stage（舞台），如果你是cocos2d用户，你可以把它视为cocos2d自身的Director。如果你对两者都不熟悉，你就把它当成一个前端控制器。 每个游戏只有一个Director。它掌控了游戏的全局viewport（视点），并且控制哪个scenes（场景）是可见的。在建立游戏逻辑的开始，你需要创建一个Director实例。它的构造函数的参数包括DOM容器元素、stage（舞台）宽和高（像素）。 var director = new dfkit.Director(document.body,320,460); Scene Scene（场景）是一个包含可视元素的用于覆盖整个viewport（视点）的独立部分。这表示同一时间点上只有一个scene（场景）是激活的。例如：在一般的游戏逻辑里，你可能需要一个菜单场景，一个游戏结算的场景。通过调用 director.replaceScene(scene) 或者 director.pushScene(scene)来让一个场景可视。不同点是后者不会移除之前的scene（场景），只是将其隐藏方便之后通过director.popScene()激活。 var scene = new lime.Scene(); director.replaceScene(scene); Transitions 单纯用replaceScene()在场景间快速切换可能吸引不了眼球。为了做的更好些可以在调用replaceScene()时用 transition 和 duration 属性。transition定义了当前场景消失和新场景激活的动画效果。当前支持 Slide（滑动）和 Move（位移）以及 Dissolve（淡入）效果。 director.replaceScene(menuscene,lime.transition.SlideInRight); director.replaceScene(gamescene,lime.transition.Dissolve,2); ScheduleManager（调度管理） Lime中的所有东西都是基于repaint-dirty （重绘-不一致）模式。也就是说当你每次改变了某些东西，你的方法调用并不等于 DOM或者Canvas2dContext调用。你设置的属性将会被标记为dirty并在下一帧被重绘。这允许我们只更新一次，更新那些需要更新的内容、并无状态的保存所有内容。无状态保存更新允许我们在任何时候切换渲染方法。因为JS没有提供任何on-enter-frame事件，所以我们使用了一个静态的lime.sheduleManager对象来模拟。它提供以下方法： schedule(callback, context) – 在每一帧里调用一个方法。Context是this作用域。 unschedule(callback, context) – 清除之前的schedule方法。 scheduleWithDelay(callback, context, delay, opt_limit) – 和schedule类似，但是回调函数只有在超过delay（自上一次执行的延迟时间）秒数时候才会被调用。 callAfter(callback, context, delay) – 在delay指定的时间后调用一次回调函数。 不要在代理里使用JS自带的setTimeout()和setInterval()方法。lime.scheduleManager给你提供了能实现同一功能但却更丰富的方法。你的回调函数只有超过距离上次执行delay的时间后才会被再次执行。这使你能够让动画更加平滑，即使实在CPU性能急剧改变的情况下。 var velocity = 2; lime.scheduleManager.schedule(function(dt){ var position = this.getPosition(); position.x += velocity * dt; // if dt is bigger we just move more this.setPosition(position); },ball);   Pausing（暂停） 使用scheduleManager代替timer发放可以充分利用暂停功能。当你希望暂停游戏时，只需调用Director对象的setPaused(true)。这将会暂停所有计划中的方法和动画。一旦你调用setPaused(false)，所有的代码又会继续执行，就如同什么都没发生一般。当你的游戏暂停时，lime.PauseScene将会被激活。如果你想自定义暂停场景，你可以覆盖这个类的功能。 mygame.director.setPaused(true); Layers（层） 现在我们准备在屏幕上放点东西了。为了更好的管理你的显示对象，我们引入了lime.Layer对象，你可以把它想象成Photoshop里的图层。Layer可以用来装东西。它和其他的可视对象的行为相同，只是它没有body和尺寸，它们只能用来包含子对象。所以你只需创建好它们，添加到树中，设置合适的位置把子对象添加进去。必须申明的是，Layer不是必须的，你可以在场景中加入任何对象，Layer让你的生活更简单。 var layer = new lime.Layer().setPosition(100,100); scene.appendChild(layer); for(var i=0;i<5;i++){ var box = customMakeBoxFunc().setPosition(i*50,0); layer.appendChild(box); }