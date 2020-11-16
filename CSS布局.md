# CSS布局

CSS 的布局应该是 CSS 体系中的重中之重了，目前PC端的常用的布局方式有 float 浮动布局、 flex 弹性布局、Grid网格布局，不论是工作还是面试都是非常重要的知识。

## float布局
步骤：
1. 子元素上加float：left和width
2. 父元素加上 .clearfix

**.clearfix** 的固定写法
```
.clearfix:after{
    content:"";
    display: block;
    clear: both;
}
```
注意：使用负margin可实现平局布局

场景：实现菜单导航栏
效果图：

![float](https://pic1.zhimg.com/80/v2-849d715b8584f58204420791a64d367c_720w.jpg)

代码实现
```
hmtl代码
  <header class="clearfix">
    <div class="logo">
      <img src="https://picsum.photos/50" alt="">
    </div>
    <div class="nav">
      <ul class="clearfix">
        <li>首页</li>
        <li>分类</li>
        <li>档案</li>
        <li>博客</li>
        <li>关于</li>
      </ul>
    </div>
  </header>
```

```
CSS代码
*{
  margin:0;
  padding:0;
  box-sizing:border-box;
}
ul li{
  list-style:none;
}

.clearfix:after{
  content:"";
  display: block;
  clear: both;
}
body{
  background:#fff;
}
header{
  height:100px;
  width:100%;
  padding-left:20px;
  background:#000;
}
.logo{
  float:left;
  margin-right:auto;
}
.logo>img{
  border-radius:50%;
  margin-top:25px
}
.nav{
  float:right;
}

ul>li{
  float:left;
  width:50px;
  line-height:100px;
  color:#fff
}
```
 ## flex布局（弹性布局）

定义：Flex 用来为盒状模型提供最大的灵活性。flex布局分为两个角色 1. flex contanier 容器  2.flex item 

### 如何让一个元素变成Flex容器

任何一个容器都可以指定为 Flex 布局。

让一个块级元素变成flex容器
```
.container{
    display:flex; /*display:inline-flex */
}
```
让一个行内元素变成flex容器
```
.container{
   display:inline-flex 
}
```
注意：当设为 Flex 布局以后，子元素的float、clear和vertical-align属性将失效。

### Flex 属性


有下面六种属性可以设置在容器上，它们分别是：

- flex-wrap
- flex-direction
- flex-flow
- justify-content
- align-items
- align-content

以下是本次练习的demo代码


```
html代码
 <div class="demo">
        <div class="item item1">item1</div>
        <div class="item item2">item2</div>
        <div class="item item3">item3</div>
        <div class="item item4">item4</div>
        <div class="item item5">item5</div>
    </div>   
```

```
CSS代码
 .demo {
        height:200px;
        width:80%;
        margin: 0 auto;
        margin-top: 20px;
        padding:10px;
        border:1px solid #888;
        border-radius:4px;
        display:flex;
    }  
    .item{
        height:100px;
        width:100px;
        line-height:100px;
        font-size: 12px;
        text-align:center;
        background:#eee;
        border-radius:4px;
        border: 1px dashed #aaa;
    }
```

#### flex-direction 改变items在主轴的流动方向

用来定义container里面 flex items 的排序方向，它默认值是row（横向）
```
.container{
    flex-direction:row|row-reverse|column|column-reverse;
}
```
如图：
![flex-direction](https://pic2.zhimg.com/80/v2-e3500c0dc5d4750055b1058318310495_720w.jpg)

flex-direction：row
- main-axis（主轴）是row
- cross-axis（交叉轴）是cloumn

flex-direction：column

- main-axis（主轴）是column
- cross-aixs（交叉轴）是row

!

####   justify-content 主轴的对齐方式
```
.container{
    justify-content:flex-start|flex-end|center|space-between|space-around
}
```
- justify-content:flex-start
  ![flex-start](https://pic4.zhimg.com/80/v2-05ad415dbc963929b910826b4b17ab4b_720w.jpg)
- justify-content:flex-end
  ![flex-end](https://pic2.zhimg.com/80/v2-9a699351b3c4bad1aaf431e9980e1b8d_720w.jpg)
- justify-content:center
  ![flex-center](https://pic2.zhimg.com/80/v2-eeb024a637ebcfb9375272b31129902d_720w.jpg)
- justify-content:space-between
  ![flex-between](https://pic2.zhimg.com/80/v2-eeb024a637ebcfb9375272b31129902d_720w.jpg)
- justify-content:space-around
  ![flex-around](https://pic4.zhimg.com/80/v2-c083c69587ab3cb5cc8c9c1039d39a5f_720w.jpg)

#### flex-wrap 改变折行
默认情况下，项目都排在一条线上。
```
.container{
    flex-wrap:nowrap|wrap|warp-reverse;
}
```

- flex-wrap:nowrap
  ![flex-nowrap](https://pic4.zhimg.com/80/v2-cdc06eacc69562c1ddcb7eade0ea8907_720w.jpg)
- flex-wrap:wrap
  ![flex-wrap](https://pic3.zhimg.com/80/v2-d8075b803fa1002c8e2e3949ea1e004a_720w.jpg)
- flex-wrap:wrap-reverse
  ![flex-wrap-reverse](https://pic1.zhimg.com/80/v2-bcf5448023599991881f555113fac11c_720w.jpg)

#### align-items 交叉轴的对齐方式
```
.container{
    align-items:flex-start|flex-end|center|stretch
}
```
- align-items:flex-start
  ![flex-align-start](https://pic2.zhimg.com/80/v2-bbd23cf532c5b62a601885a0134e29b1_720w.jpg)
- align-items:flex-end
  ![flex-align-end](https://pic4.zhimg.com/80/v2-cea58263aab3dfc527a4633ba9873793_720w.jpg)
- align-items:center
  ![flex-align-center](https://pic3.zhimg.com/80/v2-4bb7c5e34dce902b7893ec74dbf53bde_720w.jpg)

flex item 属性

1. item上加order,定义项目的排列顺序。数值越小，排列越靠前，默认为0。
```
  .item2{
        order:-1;
    }
    如图，item2的order改为-1后，item2的顺序就排在了第一位。
```
![flex-item-order](https://pic1.zhimg.com/80/v2-bd0c403e0f1e5ddf0dcfc3e32e8789c8_720w.jpg)

2. item上加flex-grow,定义项目的放大比例，默认为0，即如果存在剩余空间，也不放大。

原始状态
![flex-item-shrink](https://pic2.zhimg.com/80/v2-df90db2cf35b724080338a6647bbeb21_720w.jpg)
添加以下代码后，只有item3没有变大，因为只有item3没有设置flex-grow：1。
```
.item1,.item2,.item4,.item5{
    flex-grow: 1;
} 
```
![flex-item-shrink](https://pic4.zhimg.com/80/v2-76f00be1f9a3b6dffcebf875d6314d27_720w.jpg)


3. item上加flex-shrink 控制如何变瘦 （一般写flex-shrink：0 防止变瘦，默认是1）

原始状态
![flex-item-shrink](https://pic3.zhimg.com/80/v2-5acf0bdb80f27584b90c93a966db3bc2_720w.jpg)
添加以下代码
```
.item3{
    flex-shrink: 0;
}
```
压缩后，可以看item3并没有变瘦
![flex-item-shrink-0](https://pic2.zhimg.com/80/v2-aca2fa50dd11591c995a28d5d8b83d39_720w.jpg)

4. item上加flex-basis 控制基准宽度 （默认是auto）
5. align-self定制align-items
  添加以下代码，可以看到item3的变化
```
 .item3{
      align-self:flex-end ;
  }
```
![flex-align-slef](https://pic2.zhimg.com/80/v2-9b672b1f1759d13a7cac998cdcf48a31_720w.jpg)


 ## Grid布局（网格布局）
 概念：CSS Grid(网格) 布局（又称为 “Grid(网格)” ），是一个二维的基于网格的布局系统，它的目标是完全改变我们基于网格的用户界面的布局方式。

**grid布局demo代码**
```
html代码
<div class="grid">
       <div class="cell cell1">1</div>
       <div class="cell cell2">2</div>
       <div class="cell cell3">3</div>
       <div class="cell cell4">4</div>
       <div class="cell cell5">5</div>
       <div class="cell cell6">6</div>
       <div class="cell cell7">7</div>
       <div class="cell cell8">8</div>
       <div class="cell cell9">9</div>
   </div>
```

 ### 如何让一个元素变成grid容器
```
.grid{
  display:grid;
}
```
注意:设置为Grid布局后，容器子元素（项目）的float、display: inline-block、display: table-cell、vertical-align等设置都将失效。

### grid-template-columns 属性，grid-template-rows 属性

定义好grid容器,就开始设置容器的行和列。grid-template-columns属性定义每一列的列宽，grid-template-rows属性定义每一行的行高，设定值用空格隔开。
```
.grid{
  display:grid;
  grid-template-rows：100px 100px 100px; 
  grid-template-columns：100px 100px 100px ; 
}
```
上面定义的是3行3列的网格，如图
![grid](https://pic3.zhimg.com/80/v2-e2537440e019b5032bfc030c0d5dfdb6_720w.jpg)

### grid-row, grid-column、 grid-template-area和grid-area属性

**grid-row、grid-column、grid-area属性**
```
  grid-row:1/3; 
  grid-column:1/3;
```
grid-area是grid-row和grid-column的组合写法
grid-area的第一个数grid-row的第一个数，第二个数是grid-column的第一个数，
第三个数是grid-row的第二个数，第四个数是grid-column的第二个数。

**gird-template-areas属性**

网格布局允许指定"区域"（area），一个区域由单个或多个单元格组成。grid-template-areas属性用于定义区域。

```
gird-template-areas："header header header header"  
                  "nav main main main" 
                  "nav main main main"  
                  " . footer footer  .";
. 表示空格,写法.的两边都有空格，否则无效。
```

场景：实现系统首页布局
效果图：
![grid](https://pic4.zhimg.com/80/v2-16809ebadd0eb1e4d88952023291af5f_720w.jpg)

以下两组代码都可以得出以上面的效果图
```
.cell-1{
    grid-row:1/3; 
    grid-column:1/3;
}
.cell1{
    background-color: #7c99b4;
    grid-row: 1/2; /*or grid-row：1/span 2  span是延申的意思 */
    grid-column: 1/5;
}
.cell2{
  background-color: #8eb8e5;
  grid-row: 2/4;
  grid-column: 1/2; 
}
.cell3{
    background-color: #6b7f82;
    grid-row: 2/4;
    grid-column: 2/5;  
}
  .cell4{
    background-color: #F4A261; 
    grid-area:4/1/5/5;
}
```
或
```
 .grid{
  margin:  20px;
  display:grid;
  grid-template-rows:100px 100px 100px 100px  ;
  grid-template-columns:100px 100px 100px 100px; 
  grid-template-areas: "header header header header"
                      "aside main main main"
                      "aside main main main"
                      "footer footer footer footer";
}
.cell1{
  background-color: #7c99b4;
  grid-area: header;
}
.cell2{
  background-color: #8eb8e5;
  grid-area: aside;
}
.cell3{
  background-color: #6b7f82;
  grid-area: main;
}
.cell4{
  background-color: #F4A261;
  grid-area: footer; 
}
```

**如何设定gird-lines的名字：**

在grid每个设定值的中间，使用方括号加上Grid lines的名字：在grid每个设定值的中间，使用方括号加上Grid

```
grid-template-rows：[X1] 100px [X2] 100px [X3] 100px [X4] ; 
grid-template-columns：[Y1] 100px [Y2] 100px [Y3] 100px [Y4] ;
```
定义好grid-lines名称后，gird-row:1/3 可以写成 grid-row：X1/X3。

**fr关键字**
1fr 表示一份的意思。
`grid-template-rows：3fr 1fr 1fr 1fr 1fr;`
等同于 
`grid-template-rows：3fr repeat（4，1fr）;`
repeat（X，Y）第一个参数表示重复多少次，第二个参数表示重复些什么；
repeat不适用与grid-template-areas
