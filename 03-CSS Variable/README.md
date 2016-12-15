> [❤️ javascript30](https://javascript30.com/)是一系列的视频教程，旨在30天编写30个前端小项目。 这些项目不需要使用其他lib,不需要编译，不需要模板，回归最纯真的JavaScript；

🐶   🐶    🐶

> 🐚 这是这个系列的第三篇
- [1. Drum Kit](https://gold.xitu.io/editor/md/584fb3a48d6d8100545d56f5)
- [2.JS + CSS Clock](https://gold.xitu.io/post/5850e88d570c350069dde2b2)
- 3.CSS Variables

项目代码同步更新在[男同交友网](https://github.com/sulihuang/su-javascript30)

## 项目简介
学会使用CSS变量，通过进度条和颜色选择来控制变量的值触发JS事件，从而达到改变样式的效果

![](https://dn-mhke0kuv.qbox.me/a34702cb33b43b713e5d.png)

## 新知识点复习 🐶（附链接）

### CSS
 #### CSS Variables:
  > CSS 变量当前有两种形式：
  - 变量，就是拥有合法标识符和合法的值。可以被使用在任意的地方。可以使用var()函数使用变量。例如：`var(--example-variable)`会返回--example-variable所对应的值
  - 自定义属性。这些属性使用`--*where*`的特殊格式作为名字。例如--example-variable: 20px;即使一个css声明语句。意思是将20px赋值给--example-varibale变量。
 
`注意：在之前的标准中，自定义属性以var-作为前缀，后来才改成--前缀。Firefox 31和以后的版本遵循新标准`
MDN的🌰：
 ```
 :root {
  --main-bg-color: brown;
}

.one {
  color: white;
  background-color: var(--main-bg-color);
  margin: 10px;
  width: 50px;
  height: 50px;
  display: inline-block;
}
```
 [ISUX译我为css变量狂](https://isux.tencent.com/why-im-excited-about-native-css-variables.html)
 [引人瞩目的 CSS 变量（CSS Variable）](http://www.cnblogs.com/coco1s/p/6068522.html)
 
 
 Can I Use ?
![](https://dn-mhke0kuv.qbox.me/55046a223bae7e76d217)

- ### :root 
>   :root 伪类匹配文档树的根元素。应用到HTML，:root 即表示为元素，除了优先级更高外，相当于html标签选择器

语法：
```
:root { 样式属性 }
```
 `使用 CSS变量 的时候，声明全局CSS变量时 :root 非常实用`
 
 [结构性伪类选择器](http://www.cnblogs.com/coco1s/p/6067305.html)
 [:root | CSS属性参考](http://www.htmleaf.com/ziliaoku/qianduanjiaocheng/root.html)
 
 
### JS
 - document.documentElement [MDN -documentElement](https://developer.mozilla.org/zh-CN/docs/Web/API/Document/documentElement)
 - mousemove event [事件类型一览表-mousemove](https://developer.mozilla.org/zh-CN/docs/Web/Events/mousemove)
 
## 代码实践 ✅

设置和使用变量:
```
:root {
  --base: #ffc600;
  --spacing: 10px;
  --blur: 10px;
}
.hl {
  color: var(--base);
}
img {
  padding: var(--spacing);
  background: var(--base);
  filter: blur(var(--blur));
}
...
```

监听事件 😁，触发的时候改变变量值：
```
const selects = document.querySelectorAll('.content input');

function handleUpdate() {
  const suffix = this.dataset.sizing || '';
  document.documentElement.style.setProperty(`--${this.name}`, this.value + suffix);
}

selects.forEach(item => item.addEventListener('change', handleUpdate));
selects.forEach(item => item.addEventListener('mousemove', handleUpdate));
```

希望大家也多联系一下，虽然看起来很简单，但是每天花一点时间巩固一下基础也不错 ( ⊙ o ⊙ )！