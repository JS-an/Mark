# var let const的理解 #

> 简单来说：
> 
> 使用var声明的变量，其作用域为该语句所在的函数内function，且存在变量提升现象；
> 使用let声明的变量，其作用域为该语句所在的代码块内{}，不存在变量提升；
> 使用const声明的是常量，在后面出现的代码中不能再修改该常量的值（值里可以改。例如：对象，数组）；

[我用了两个月的时间才理解 let--方应杭](https://zhuanlan.zhihu.com/p/28140450)

    var liList = document.querySelectorAll('li') // 共5个li
    for( var i=0; i<liList.length; i++){
      liList[i].onclick = function(){
    console.log(i)
      }
    }

上面执行相当于

    var i = 0
      liList[0].onclick = function(){
    console.log(i)
      }

    var i = 1
      liList[1].onclick = function(){
    console.log(i)
      }

    var i = 2
      liList[2].onclick = function(){
    console.log(i)
      }

    var i = 3
      liList[3].onclick = function(){
    console.log(i)
      }

    var i = 4
      liList[4].onclick = function(){
    console.log(i)
      }

    var i = 5

> 因存在变量提升现象，该例子来说作用域与`var liList`为同一作用域，所以当for运行后，后面的`i`会覆盖掉前面的`i`，不管点击哪个`consle.log`都为5

如改为`let`

    let i = 0
      liList[0].onclick = function(){
    console.log(0)
      }

    let i = 1
      liList[1].onclick = function(){
    console.log(1)
      }

    let i = 2
      liList[2].onclick = function(){
    console.log(2)
      }

    let i = 3
      liList[3].onclick = function(){
    console.log(3)
      }

    let i = 4
      liList[4.onclick = function(){
    console.log(4)
      }

    let i = 5

> 每一个块级作用域都有一个`i`

> for{} 里面的过程：
> 
> 1:找到所有用 let 声明的变量，在环境中「创建」这些变量
> 
> 2:开始执行代码（注意现在还没有初始化）
> 
> 3:执行 i = 0，将 i 「初始化」为 1（这并不是一次赋值，如果代码是 let i，就将 i 初始化为 undefined）

>point： let 确实存在提升。只不过由于暂时死区的限制，你不能在 let i 之前使用 let