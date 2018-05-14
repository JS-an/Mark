# transform 3D #
> （如一个体育馆）

1. 体育馆作为一个容器
1. 舞台作为一个容器
1. 舞台上的人是一个元素

> 所以格式如下：

    <div class="container">
		<div class="stage">
			<div class="performer"></div>
			...
		</div>
	</div>

## transform 3D 属性 ##
	1. 用在体育馆上

    perspective 规定我们看表演的距离（相当于我们坐在座位上看舞台的距离）
    perspective-origin 规定我们看表演的方向（相当于我们坐在同一排不同座位上看舞台的中心点）

	2. 用在舞台上
	
    transform-style 规定是平面还是3D（相当于舞台上是放电影，还是舞台剧表演）
    backface-visibility 规定背面是否可见