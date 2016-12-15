# Drum Kit
> [❤️ javascript30](https://javascript30.com/)是一系列的视频教程，旨在30天编写30个前端小项目。 这些项目不需要使用其他lib,不需要编译，不需要模板，回归最纯真的JavaScript；

🐶   🐶    🐶

> 🐚 写在前面： 我是从NodeJs转向前端开发的，并且才半年时间左右，而且这半年更多的是进行React和Angular相关的开发，所以有很多前端基础知识，比如HTML5和CSS3的新特性使用的并不好，通过这个系列的学习，可以更好的掌握基础知识；

## 项目简介

Drum Kit项目是在相应用户的键盘事件，改变对应的样式和播放不同的audio，并且在完成后重置样式；

## 知识点复习（附我学习的链接）
**HTML**
 - `<audio>`标签  [使用 JavaScript 控制Audio对象](https://msdn.microsoft.com/zh-cn/library/gg589489.aspx)
 - `<kdd>`标签 用于表示用户输入的标签 [MDN-kdd](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/kbd)
 
**CSS**
- flex布局 [一个完整的Flexbox指南](http://www.w3cplus.com/css3/a-guide-to-flexbox-new.html)， [A Complete Guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
- background-size [MDN-background-size](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-size)
- transition [MDN-transition](https://developer.mozilla.org/zh-CN/docs/Web/CSS/transition)
- transform [MDN-transform](https://developer.mozilla.org/zh-CN/docs/Web/CSS/transform)
- letter-spacing [MDN-letter-spacing](https://developer.mozilla.org/zh-CN/docs/Web/CSS/letter-spacing)
- rem [移动web适配利器-rem](http://www.alloyteam.com/2016/03/mobile-web-adaptation-tool-rem/), [了解真实的『REM』手机屏幕适配](https://github.com/hbxeagle/rem/blob/master/README.md)
- vh: 1vh 等于1/100的视口高度。 [7个你可能不认识的CSS单位](https://github.com/simaQ/cssfun/issues/1)， [谈谈CSS3的长度单位（vh、vw、rem）](http://ghmagical.com/article/page/id/XMzbRAPw6rba)

**JS**
- Element.classList [MDN-Element.classList](https://developer.mozilla.org/zh-CN/docs/Web/API/Element/classList)
- document.querySelector(), document.querySelectorAll() [[译]你所不了解的querySelector](http://blog.lxjwlt.com/front-end/2015/09/01/u-dont-know-queryselector.html)
- transitionend event: transitionend 事件会在 CSS transition 结束后触发  [MDN-transitionend](https://developer.mozilla.org/zh-CN/docs/Web/Events/transitionend)
- `NodeList.forEach()`:  [英MDN-NodeList](https://developer.mozilla.org/en-US/docs/Web/API/NodeList)

## 代码实践
编写html:

![](https://dn-mhke0kuv.qbox.me/6c102ebd0215788a14e1.gif)

这里使用emmet插件快速编写html代码，感兴趣的朋友可以去了解一下emmet；

监听键盘事件:
```
function play(e) {
  const audio = document.querySelector(`audio[data-key="${e.keyCode}"]`)
  const key = document.querySelector(`.key[data-key="${e.keyCode}"]`)
  
  if (!audio) return
  audio.currentTime = 0; // 重置
  audio.play();
  key.classList.add('playing');
}
window.addEventListener('keydown', play);
```
监听transitionend事件:

```
function removeTransition(e) {
  console.log('ee:', e)
  if (e.propertyName !== 'transform') return; // 如果不是transform完成过渡，则忽略
  this.classList.remove('playing');
}
const keys = document.querySelectorAll('.key')
// 这里按我以前的知识，总觉得它会错
keys.forEach(key => key.addEventListener('transitionend', removeTransition));

```

.playing的样式如下：
```
.playing {
  transform: scale(1.2);
  border-color: #ffc600;
  box-shadow: 0 0 10px #ffc600;
}
```

### 遇到的坑
大家应该都知道一个类数组（array like）的概念， 上面代码中`const keys = document.querySelectorAll('.key')` 得到的keys就是一个类数组;

然后我印象中看过很多类数组相关的材料，类数组的定义如下：
- 拥有length属性，其它属性（索引）为非负整数(TO_NUMBER之后);
- 不具有如 push 、 forEach等数组对象具有的方法

那么为什么keys是NodeList,明明是类数组，为什么有`forEach`方法？这里先展示俩个截图：

![](https://dn-mhke0kuv.qbox.me/c426556b91712475a8ec.png)
![](https://dn-mhke0kuv.qbox.me/e62cad7b3519edbe4cd3.png)

![](https://dn-mhke0kuv.qbox.me/3f9536b14298381f0959)


原来NodeList虽然是类数组对象，但是提供了forEach方法，但是中文的文档中却没有更新！

NodeList还提供了keys, values等方法！
