[TOC]

# 50道css基础面试题

## css选择器有哪些 

* div+p:选择每个紧跟在div后面的p元素
* a[href="xxxx"]:选择href为xxxx的a元素
* 伪类选择器：（a:hover）
* 标签选择器

## 哪些属性可以继承
* 可继承
1. font-size
2. font-family
3. color
* 不可继承属性
1. width
2. height
3. padding
4. border

## css优先级
* !import优先级最高
* 选择器优先级 ：ID选择器 > 类选择器 | 属性选择器 | 伪类选择器 > 元素选择器>浏览器缺省
* css权重
1. 内联：1000
2. id选择器：100
3. class选择器：10
4. 属性选择器：1
* 如果优先级相同，则选择最后出现的样式。

## css3新增伪类
* p:first-of-type/ p:last-of-type：父元素的第一个/最后一个p元素
* p:only-of-type：当所有子元素中只有一个p时
* p:only-child 

## css3新属性
* background-origin:content-box/border-box/padding-box:背景图片相对于什么来定位。
* background-position:相对于 background-origin的情况下的定位。
* word-wrap:normal/break-word
1. normal:在词间不允许换行
2. break-word：在词间允许换行
* @font-face:自定义样式
```css
@font-face
{
	font-family: myFirstFont;
	src: url('Sansation_Light.ttf')
}
```

## flexbox
* flexbox布局指提供一个更加有效的方法制定，调整和分布一个容器里的项目布局，即使他们的大小是位置或者是动态的。
* flex布局中有两个非常重要的概念：**Flex容器和flex项目**
### flex容器
属性|值|含义
-|-|-
flex-derection |row/column/row-reverse/column-reverse|控制Flex项目沿着主轴（Main Axis）的排列方向
flex-wrap|wrap/nowrap/wrap-reverse	|控制Flex项目是否换行显示
flex-flow|row wrap/row nowrap/column wrap/column nowrap|flex-direction和flex-wrap两个属性的组合速记属性
justify-content|flex-start/flex-end/center/space-between/space-around|控制 Flex项目在Main-Axis上的对齐方式
align-items|flex-start/flex-end/center/stretch/baseline|控制Flex项目在Cross-Axis对齐方式
align-content|flex-start/flex-end/center/stretch|用于多行的Flex容器，控制Flex项目在Cross-Axis对齐方式

#### flex-direction
* 项目沿主轴方向的排列方式（默认row）
1. row/row-reverse：主轴水平，起点分别为左端和右端。（1，2，3/3，2，1）
2. cloumn/cloumn-reverse:主轴垂直向下/向上

#### flex-wrap
* 项目是否换行显示（默认no-wrap）
1. wrap/nowrap：换行/不换行
2. wrap-reverse：先换行，上下顺序颠倒显示。

#### flex-flow
* flex-direction和flex-wrap两个属性的组合速记属性

#### justify-content
* 项目在主轴上的对齐方式（默认flex-start）
1. flex-start/flex-end/center：主轴开始/结束/中间
2. space-between：让项目两端对齐。
3. space-around：让项目之间有相同的空间

#### align-items
* 项目在Cross-Axis对齐方式（默认stretch）
1. flex-start\flex-end/centet
2. strenth:让所有flex高度和容器高度一样
3. baseline：让项目在Cross-Axis上沿着他们自己的基线(文字最下面)对齐。

### flex项目
属性|值|含义
-|-|-
order|数字|根据order重新排序
flex-grow|0/positive numser|控制flex项目在容器有多余空间时如何放大
flex-shrink|0/positive|控制flex在容器没有额外空间时如何缩小
flex-basis|auto/ %/ em /rem/ px|制定flex项目的初始大小
align-self|auto /flex-start/ flex-end / center /baseline / stretch|控制单个flex项目在cros-axis的对齐方式

#### order
* 根据order的值从低到高排序（默认为0）
#### flex-grow
* 控制在容器有多余的空间如何放大（默认0）
* 放大方式：可用空间/item的和，然后得到单位分配空间，如果一个item的grow为6，则需要在主轴上延伸6*单位分配空间的大小。

#### flex-shrink

* 控制在容器没有有多余的空间如何缩小（默认1：即空间不足时，都缩小）
* 怎么缩小
1. 将所有项目，按照flex-shrink*item—size的方式加起来，得到一个加权和。
2. 计算出每一份item的shrink比例 = flex-shrink * item-size / 之前的总和。
3. 最后每一个item减去这个shrink比例 * 负可用空间。


#### flex-basis
* 制定flex元素在主轴方向的初始大小。（默认auto:根据auto大小来定）
* flex-basis和width/height的优先级
1. flex-basis不是默认值时，优先级比width/heght高。
2. width/height auto优先级等于 flex-basis，取两者中的最大值。

#### align-self
1. 控制单个项目沿着corss-axis的对齐方式（默认值为auto：表示继承氟元素的align-items属性）

#### flex
* flex时flex-grow，flex-shrink和flex-basis的所有，默认值为0,1,auto，后两个属性可选
* 该属性有两个快捷值：
1. auto：（1 1 auto）
2. none：（0 0 auto）

## css实现三角形
```css
div{
	width:0;
	height:0;
	border-top:30px solid transparent;
	border-right:30px solid transparent;
	border-left:30px solid transparent;
	border-borrom:30px solid blud;
}
```

