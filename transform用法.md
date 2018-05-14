# transform的用法 #

    transform: matrix(a,b,c,d,e,f)
     （e,f）为偏移量（x,y）相当于translate（）
     只缩放时：改变（a,d）
     只旋转时：旋转角度为（a=cosθ,b=sinθ,c=-sinθ,d=cosθ,0,0)
     只倾斜时：(tanθy,tanθx)

> 可用另一种写法代替
   
     transform:translate(px,px) rotate(deg) skew(deg) scale(倍数)