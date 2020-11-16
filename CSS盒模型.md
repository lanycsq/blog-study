# CSS盒模型

## **1.什么是css模型？**

css的盒模型由里到外包括：content,padding,border,margin4部分,如图所示。

css的盒模型有两种：**IE盒模型和标准盒模型**。

## **2.两种盒模型的区别**

- W3C标准盒子模型(content-box)：内容就是盒子的边界。
- W3C标准盒子模型(content-box)： width=
- IE盒子模型(border-box)：边框才是盒子的边界。
- IE盒子模型(border-box)： width=content（内容宽度）+padding+border

## **3.如何设置两种盒模型**

 在不设置box-sizing的情况下，box-sizing默认是content-box。

 ```
/* 标准模型 */
box-sizing:content-box;

 /*IE模型*/
box-sizing:border-box;
 ```

## **4.margin合并**

margin合并：如果两个box都设置了外边距，那么在垂直方向上，两个box的外边距会发生重叠，以绝对值大的那个为最终结果显示在页面上。

**哪些情况会发生margin合并**

父子margin合并

如果子元素设置了外边距，在没有把父元素变成BFC的情况下，父元素也会产生外边距，给父元素添加 overflow：hidden 这样父元素就变为 BFC，不会随子元素产生外边距，但是父元素的高会变化。

兄弟margin合并 

同级（兄弟）元素在垂直方向上外边距会出现重叠情况，最后外边距的大小取两者绝对值大的那个

注意：行内元素没有margin-top或margin-bottom，也就是说，在行内元素上设置margin-top或margin-bottom是不起作用的。

## **5.BFC**
 BFC(Fomatting Context)是块级格式化上下文的意思。它是 CSS 2.1 规范中的一个概念，它决定了元素如何对其内容进行定位，以及与其他元素的关系和相互作用。

 **触发BFC的条件**
   - 浮动元素(float除了node以外的值)
   - 定位元素(position: absolute/ fixed)
   - display(值为inline-block/ table-cell/- table-caption/ flex/ inline-flex)
   - overflow(值为hidden/atuo/srcoll)
        设置有这些属性的box，都会产生BFC

 **BFC特性**
 - 内部的盒子在垂直方向上一个接一个地放置
 - 垂直方向上地距离由margin决定，在同一个BFC的box中，相邻的两个box边距会重叠
 - BFC的区域不会与float box重叠
 - 计算BFC的高度时，浮动元素也参与计算
 - BFC就是一个独立的容器，里面的子元素不受外面的元素影响  

 **BFC的作用**

 **1.解决margin重叠问题（添加独立BFC）**

 看下面例子

 未设置BFC之前
 ```
 CSS代码
 .child{
    width: 100px;
    height: 100px;
    background-color: orange;
    margin: 30px;
}

html代码
<div class="child"></div>
<div class="child"></div>
 ```
设置BFC后
 ```
 CSS代码
.child{
    width: 100px;
    height: 100px;
    background-color: orange;
    margin: 30px;
}
.bfc{
    overflow: hidden;
}

html代码
<div class="child"></div>
<div class="bfc">
    <div class="child"></div>
</div>
 ```
 设置BFC后，第一个child的margin-bottom不会和第二个child的margin-top重叠，这也是BFC元素的另一个原则，不会影响到外边的box，是一个独立的区域。

效果图对比

2.解决浮动高度塌陷问题（在父元素添加overflow：hidden）

 当我们不给父元素设置高度，子元素设置了浮动的时候，会发生高度塌陷，代码和效果图如下。

效果图：

```
CSS代码
.father {
    border: 5px solid rgb(91, 243, 30);
    width: 460px;
    
}
.child{
    width: 200px;
    height: 200px;
    border:5px solid orange;
    float: left;
}

html代码
<div class="father">
    <div class="child"></div>
    <div class="child"></div>
</div>
```

当我们在父元素的样式中加入overflow：hidden，就能解决float高度塌陷问题。

```
CSS代码
.father {
    border: 5px solid rgb(91, 243, 30);
    width: 460px;
    overflow: hidden;
}
.child{
    width: 200px;
    height: 200px;
    border:5px solid orange;
    float: left;
}

html代码
<div class="father">
    <div class="child"></div>
    <div class="child"></div>
</div>
```
效果图就会发生变化





