# angular的双向数据绑定原理
> 1. angular是不存在双向数据绑定的
> 2. angular对常用的dom操作，xhr事件进行封装，在里面触发angular的digest流程。
> 3. 在digest流程中，会从rootscope开始遍历，查找所有的watcher。

谈起angular的脏检查机制，很多人误以为他是定时检查modal是否变更。其实，ng只有在指定事件触发时，才会进入$digest cycle:
1. DOM事件，比如用户输入文本，点击按钮等；

2. XHR响应事件

3. 浏览器location变更事件

4. timer($interval,$timeout)

5. 执行$digest()或$apply()

## $digest和$apply
在Angular中，有$apply和$digest两个函数，我们刚才是通过$digest来让这个数据应用到界面上。那么，它们的差异是什么呢？

>最直接的差异，$apply可以带参数，它可以接受一个函数，在应用数据之后调用这个函数。
>对于$digest来说，在父作用域和子作用域上调用是有差别的，但是，对于$apply来说，这两者一样。当调用$digest的时候，只触发当前作用域和它的子作用域上的监控，但是当调用$apply的时候，会触发作用域树上的所有监控。
