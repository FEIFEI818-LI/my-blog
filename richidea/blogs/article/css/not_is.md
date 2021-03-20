---
title: css伪类选择器
date: 2021-03-20
sidebar: auto
tags:
 - css
categories:
 - 推荐文章
---
## 彻底搞懂css伪类选择器
### :not()
---
单从字面意思就是不包括、排除括号内元素。<br />
最简单的例子，用CSS将div内，在不改变html的前提下，除了P标签，其它的字体颜色变成红色。
```html
<div>
    <span>我是蓝色</span>
    <p>我是黑色</p>
    <h1>我是红色</h2>
    <h2>我是红色</h2>
</div>
```
之前写法
```css
div span,div h1,div h2,{
  color: red;
}
```
not写法
```css
div:not(p){
  color: red;
}
```
### :is()
---
在说is前，需要先了解一下matches

matches跟is是什么关系？
matches是is的前世，但是本质上确实一个东西，用法完全一样。

matches这个单词意思跟它的作用非常匹配，但是它跟not作用恰好相反，作为not的对立面，matches这个次看起来确实格格不入，而且单词不够简洁，所以它被改名了，这里还有一个issue https://github.com/w3c/csswg-drafts/issues/3258，也就是它改名的源头。

好了，现在知道matches和is其实是一个东西，那么is的用法是怎样的呢？
举例：将header和main下的p标签，在鼠标hover时文字变蓝色。
```html
<header>
  <ul>
    <li><p>鼠标放上去变蓝色</p></li>
    <li><p>鼠标放上去变蓝色</p></li>
  </ul>
  <p>正常字体</p>
</header>
<main>
  <ul>
    <li><p>鼠标放上去变蓝色</p></li>
    <li><p>鼠标放上去变蓝色</p></li>
    <p>正常字体</p>
  </ul>
</main>
<footer>
  <ul>
    <li><p>正常字体</p></li>
    <li><p>正常字体</p></li>
  </ul>
</footer>
```
之前写法
```css
header ul p:hover,main ul p:hover{
  color: blue;
}
```
is写法
```css
:is(header, main) ul p:hover{
  color: blue;
}
```
从上面的例子大概能看出is的左右，但是并没有完全体现出is的强大之处,但是当选择的内容变多之后，特别是那种层级较多的，会发现is的写法有多简洁。
比如MDN的例子
之前写法
```css
/* Level 0 */
h1 {
  font-size: 30px;
}
/* Level 1 */
section h1, article h1, aside h1, nav h1 {
  font-size: 25px;
}
/* Level 2 */
section section h1, section article h1, section aside h1, section nav h1,
article section h1, article article h1, article aside h1, article nav h1,
aside section h1, aside article h1, aside aside h1, aside nav h1,
nav section h1, nav article h1, nav aside h1, nav nav h1 {
  font-size: 20px;
}
```
is写法
```css
/* Level 0 */
h1 {
  font-size: 30px;
}
/* Level 1 */
:is(section, article, aside, nav) h1 {
  font-size: 25px;
}
/* Level 2 */
:is(section, article, aside, nav)
:is(section, article, aside, nav) h1 {
  font-size: 20px;
}
```
可以看出，嵌套的层级越多，就越能体现is优势。
### :any()
---
看完了is，那就必须认识一下any,前面说到is是matches的替代者。

any跟is又是什么关系呢？
是的，is也是any的替代品，它解决了any的一些弊端，比如浏览器前缀、选择性能等。

any作用跟is完全一样，唯一不同的是它需要加浏览器前缀，用法如下：
```css
:-moz-any(.b, .c) {
}
:-webkit-any(.b, .c) {
}
```
所以现如今一般用is来替代any。