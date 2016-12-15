# Clock
> [❤️ javascript30](https://javascript30.com/)是一系列的视频教程，旨在30天编写30个前端小项目。 这些项目不需要使用其他lib,不需要编译，不需要模板，回归最纯真的JavaScript；

🐶   🐶    🐶

> 🐚 写在前面： 我是从NodeJs转向前端开发的，并且才半年时间左右，而且这半年更多的是进行React和Angular相关的开发，所以有很多前端基础知识，比如HTML5和CSS3的新特性使用的并不好，通过这个系列的学习，可以更好的掌握基础知识；
这是这个系列的第二篇
- [1.JavaScript30 - 1.Drum Kit](https://gold.xitu.io/editor/md/584fb3a48d6d8100545d56f5)
- 2.JS + CSS Clock

项目代码同步更新在[男同交友网](https://github.com/sulihuang/su-javascript30)

## 项目简介
使用原生的JS和CSS，完成如下的时钟效果

![](https://dn-mhke0kuv.qbox.me/aa5d109ae67a0c4111fe.png)

## 新知识点复习（附链接）

**CSS**
 - border-radius [MDN-border-radius](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-radius)
 - box-shadow [MDN-https://developer.mozilla.org/zh-CN/docs/Web/CSS/box-shadow](https://developer.mozilla.org/zh-CN/docs/Web/CSS/https://developer.mozilla.org/zh-CN/docs/Web/CSS/box-shadow)
 - transform-origin [MDN-transform-origin](https://developer.mozilla.org/zh-CN/docs/Web/CSS/https://developer.mozilla.org/zh-CN/docs/Web/CSS/transform-origin)
 - transition-timing-function: cubic-bezier(0.1, 2.7, 0.58, 1); [transition-timing-function](https://developer.mozilla.org/zh-CN/docs/Web/CSS/transition-timing-function)
 
 **JS**
 - Date [JavaScript Date时间对象详解](https://my.oschina.net/sakmon/blog/393943)
   - getHours
   - getMinutes
   - getSeconds
 - setInterval [你所不知道的setInterval](http://www.jeffjade.com/2016/01/10/2016-01-10-javaScript-setInterval/)
 
## 代码实践

这个项目的核心在与算时针、分针和秒针的角度
> 这里我发现了作者提供的代码中的一些不足,视频中算分针和时针偏移的时候应该是出现了一些错误；

我修改后的版本：
- 秒针的度数就等于当前秒数

```
const now = new Date();
const seconds = now.getSeconds();

// +90表示0秒时，秒针指向的为90度
const secondsDegrees = ((seconds / 60) * 360) + 90;
```

- 分针的度数等于当前分钟数加上秒数的偏移量

```
const mins = now.getMinutes();
const minsDegrees = ((mins / 60 + seconds / (60 * 60)) * 360) + 90;
```

- 时针的度数 等于当前小时数加上分钟和秒钟的偏移量

```
const hour = now.getHours();
const hourDegrees = ((hour / 12 + mins/720 + seconds /(12 * 60 * 60)) * 360) + 90;
```

完整代码:
```
const secondHand = document.querySelector('.second-hand');
const minsHand = document.querySelector('.min-hand');
const hourHand = document.querySelector('.hour-hand');

function setDate() {
  const now = new Date();
  console.log(now)
  const seconds = now.getSeconds();
  const secondsDegrees = ((seconds / 60) * 360) + 90;
  secondHand.style.transform = `rotate(${secondsDegrees}deg)`;

  const mins = now.getMinutes();
  const minsDegrees = ((mins / 60 + seconds / (60 * 60)) * 360) + 90;
  minsHand.style.transform = `rotate(${minsDegrees}deg)`;

  const hour = now.getHours();
  const hourDegrees = ((hour / 12 + mins/720 + seconds /(12 * 60 * 60)) * 360) + 90;
  hourHand.style.transform = `rotate(${hourDegrees}deg)`;
}

setInterval(setDate, 1000);
```

 