# Flex box ([阮一峰的blog](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html?^%$))#

> Flex 是 Flexible Box 的缩写，意为"弹性布局"，用来为盒状模型提供最大的灵活性。
> 
> 任何一个容器都可以指定为 Flex 布局。

    .box{
      display: flex;
    }

> 行内元素也可以使用 Flex 布局

    .box{
      display: inline-flex;
    }

> Webkit 内核的浏览器，必须加上-webkit前缀

    .box{
      display: -webkit-flex; /* Safari */
      display: flex;
    }

> 注意，设为 Flex 布局以后，子元素的float、clear和vertical-align属性将失效。

## 容器的属性 ##

    flex-direction 项目的排列方向
    flex-wrap 属性定义，如果一条轴线排不下，如何换行
    flex-flow 属性是flex-direction属性和flex-wrap属性的简写形式
    justify-content 属性定义了项目在水平轴上的对齐方式
    align-items 属性定义项目在垂直轴上如何对齐
    align-content 属性定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用

## 项目（元素）的属性 ##

    order 属性定义项目的排列顺序。数值越小，排列越靠前，默认为0
    flex-grow 性定义项目的放大比例，默认为0，即如果存在剩余空间，也不放大
    flex-shrink 属性定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小
    flex-basis 属性定义了在分配多余空间之前，项目占据的主轴空间
    flex 属性是flex-grow, flex-shrink 和 flex-basis的简写
    align-self 属性允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性