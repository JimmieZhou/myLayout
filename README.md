<!--
 * @Descripttion: 
 * @version: 1.0.0
 * @Author: jimmiezhou
 * @Date: 2019-10-28 11:33:21
 * @LastEditors: jimmiezhou
 * @LastEditTime: 2019-10-28 13:57:20
 -->
# myLayout
最近闲来无事，决定将页面布局这块东西做一个总结。前面三节都是比较简单的parent+son的页面结构，所以就不贴代码了，自行补脑吧。

## 一、水平居中
### 1.1 文本/行内元素/行内块级元素
> 原理：text-align只控制行内内容(文字、行内元素、行内块级元素)如何相对他的块父元素对齐
```css
#parent{
    text-align: center;
}
```
- 优点：简单快捷，容易理解，兼容性非常好
- 缺点：只对行内内容有效；属性会继承影响到后代行内内容；如果子元素宽度大于父元素宽度则无效，只有后代行内内容中宽度小于设置text-align属性的元素宽度的时候，才会水平居中
### 1.2 单个块级元素
> 原理：根据规范介绍得很清楚了，有这么一种情况：在margin有节余的同时如果左右margin设置了auto，将会均分剩余空间。另外，如果上下的margin设置了auto，其计算值为0
```css
#son{
    width: 100px; /*必须定宽*/
    margin: 0 auto;
}
```
- 优点：简单；兼容性好
- 缺点：必须定宽，并且值不能为auto；宽度要小于父元素，否则无效
### 1.3 多个块级元素
> 原理：text-align只控制行内内容(文字、行内元素、行内块级元素)如何相对他的块父元素对齐
```css
#parent{
    text-align: center;
}
.son{
    display: inline-block; /*改为行内或者行内块级形式，以达到text-align对其生效*/
}
```
- 优点：简单，容易理解，兼容性非常好
- 缺点：只对行内内容有效；属性会继承影响到后代行内内容；块级改为inline-block换行、空格会产生元素间隔
### 1.4 使用绝对定位实现
> 原理：子绝父相，top、right、bottom、left的值是相对于父元素尺寸的，然后margin或者transform是相对于自身尺寸的，组合使用达到水平居中的目的
```css
#parent{
    height: 200px;
    width: 200px;  /*定宽*/
    position: relative;  /*父相*/
    background-color: #f00;
}
#son{
    position: absolute;  /*子绝*/
    left: 50%;  /*父元素宽度一半,这里等同于left:100px*/
    transform: translateX(-50%);  /*自身宽度一半,等同于margin-left: -50px;*/
    width: 100px;  /*定宽*/
    height: 100px;
    background-color: #00ff00;
}
```
- 优点：使用margin-left兼容性好；不管是块级还是行内元素都可以实现
- 缺点：代码较多；脱离文档流；使用margin-left需要知道宽度值；使用transform兼容性不好（ie9+）
### 1.5 任意个元素（flex）
> 原理：就是设置当前主轴对齐方式为居中。说不上为什么，flex无非就是主轴侧轴是重点，然后就是排列方式的设置，可以去看看文末的flex阅读推荐
```css
#parent{
    display: flex;
    justify-content: center;
}
```
- 优点：功能强大；简单方便；容易理解
- 缺点：PC端兼容性不好，移动端（Android4.0+）
## 本章小结
- 对于水平居中，我们应该先考虑，哪些元素有自带的居中效果，最先想到的应该就是$\color{red}{text-align:center}$了，但是这个只对行内内容有效，所以我们要使用 <label style="color:#f88">text-align:center</label>就必须将子元素设置为<label style="color:#f88"> display: inline; </label>或者<label style="color:#f88"> display: inline-block;</label>
- 其次就是考虑能不能用<label style="color:#f88">margin: 0 auto;</label>，因为这都是一两句代码能搞定的事，实在不行就是用绝对定位去实现了。
- 移动端能用<label style="color:#f88">flex</label>就用<label style="color:#f88">flex</label>，简单方便，灵活并且功能强大，无愧为网页布局的一大利器！<font face="黑体" color=green size=5>我是黑体，绿色，尺寸为5</font>

