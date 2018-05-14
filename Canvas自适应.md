# canvas自适应 #
> canvas相当于一张图片，如果先创建的元素，再通过JS改变宽高，则会拉伸元素，内容也会拉伸。
## 方法一 ##
    var w = document.body.clientWidth,
        h = document.body.clientHeight,
        Canvas = "<canvas id='mCanvas' width = " + w + " height = " + h + "></canvas>"
    document.body.insertAdjacentHTML("beforeEnd", Canvas)
## 方法二 ##
    var Canvas = document.createElement("canvas");
    Canvas.setAttribute("width", document.body.clientWidth);
    Canvas.setAttribute("height", document.body.clientHeight);
    Canvas.setAttribute("id", "Canvas");
    document.body.appendChild(Canvas);
> 以上两种方法是通过元素添加进DOM之前设置属性