# angular的双向数据绑定原理
> 1. angular是不存在双向数据绑定的
> 2. angular对常用的dom操作，xhr事件进行封装，在里面触发angular的digest流程。
> 3. 在digest流程中，会从rootscope开始遍历，查找所有的watcher。

谈起angular的脏检查机制，很多人误以为他是定时检查modal是否变更。其实，ng只有在指定事件触发时，才会进入$digest cycle:
> 1. DOM事件，比如用户输入文本，点击按钮等；
> 2. XHR响应事件
> 3. 浏览器location变更事件
> 4. timer($interval,$timeout)
> 5. 执行$digest()或$apply()
