# for循环中的 i 是在哪声明的

```
 for(var i = 0; i < 10; i++){
  console.log(i)
 }
```
经常用到上面格式的for循环，却不是很了解 i 声明的位置。

它的执行过程是
```
var i;
{i = 0}
{i = 1}
{i = 2}
```
还是下面这样呢？
```
{var i = 0}
{var i = 1}
{var i = 2}
```
我们知道ES6中用let声明解决了for循环 i 泄漏的问题，可以推测，似乎是第二种解析方式。

但是真的是这样吗？

参考http://www.barretlee.com/ST/ES5.1/#sec-12.6.3 和 http://www.barretlee.com/ST/ES6/#sec-for-statement 可以发现：

ES5和ES6不一样，ES5的for循环只有静态语义，而ES6的for statement存在两种语义，格式不同语义不同，分为静态语义和动态语义。上面代码换成let能解决i值泄漏是因为block块具备动态语义。而 ES5 中 var VariableDeclarationListNoIn 是先声明，然后赋值。ES5 文档中没有做出特殊说明，可以看出 var 变量并不会多次声明。

对于这种原则性的问题，建议直接阅读 ES 文档。
