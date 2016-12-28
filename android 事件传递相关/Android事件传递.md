

原创作品，允许转载，转载时请务必以超链接形式标明文章 原始出处 、作者信息和本声明。否则将追究法律责任。http://lichen.blog.51cto.com/697816/1397112 

![pic](http://s3.51cto.com/wyfs02/M01/24/6E/wKiom1NPapfjW9obAAJTEMmddQc567.jpg)


事件经过主要的三层，分别是Activity、Layout(多个)、View




三者都拥有dispatchTouchEvent和onTouchEvent方法。

dispatchTouchEvent是用来控制事件分发的(隧道方式传递)。从源码的角度看，其逻辑控制等起主导作用；从使用角度看，在diapatchTouchEvent中用逻辑判断、设置Event的action是个好的方法，而改变其return值会让事件丢失。

onTouchEvent是用来处理、消费事件的。return true标志着事件已被消费；return false标志着事件未被消费，往Layout/Activity方向传递。





Layout除了拥有这两个方法，还独有onInterceptTouchEvent方法。

onInterceptTouchEvent是在事件由Layout分发到View之前的一个拦截机制。因为只通过Layout的dispatchTouchEvent操控只能让事件丢失。


如果onInterceptTouchEvent return true，表明拦截事件，事件就不会继续分发而是跳到Layout的onTouchEvent方法中去处理；return false则事件继续分发。




在众多分析事件机制的文章中，很难看到与onTouch、onClick关联起来的解释。开始时我也拿捏不好onTouch和onTouchEvent的关系。

事实上，onTouch是在onTouchEvent之前执行的。如果onTouch return true，表示事件已经被消费，不会调用onTouchEvent了。

而onClick呢，则是在onTouchEvent的ACTION_DOWN和ACTION_UP都执行完之后，才会触发onClick。也就是说，在此之前任意位置return了true，onClick都不会被调用。




至此，我产生了一个疑问：Android为什么要这么设计事件传递机制？

① onInterceptTouchEvent：是Layout特有的，是给予Layout对于Event的独立把控权，而不是傻傻的等待事件再冒泡传递回onTouchEvent。

② onTouch：区分于onTouchEvent，给开发者不破坏基础事件传递逻辑(比如 Button的onTouchEvent默认的Super.onTouchEvent()里面是有逻辑判断来决定return值)的情况下对事件有自己的把控操纵权。
