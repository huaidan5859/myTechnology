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

我们知道var声明变量是可以变量提升的 那么即使是第二种解析方式其实也是
```
var i;
{i=0}
{i=1}
{i=2}
```
那么我们把var换成let，将会如何解析呢？首先我们通过babel转换一下。
```
 for(var i = 0; i < 10; i++){
  console.log(i)
 }
```
我们发现解析成es5,得到的仍然是for循环；那么什么原因使它能够解决i值泄漏的问题呢。我们再做一个实验。
```
 for(let i = 0; i < 3; console.log('in expression',i),i++){
  let i;
  console.log('in block',i);
 }
 
 //result
 in block undefined
 in expression 0
 in block undefined
 in expression 1
 in block undefined
in expression 2
```
首先没有报错，说明两个i并不是同一个作用域。
```
 for(let i = 0; i < 3; console.log('in expression',i),i++){
 //作用域a
  {
  //作用域b 
   let i;
   console.log('in block',i);
  }
 }
```
let解决了i值泄漏的问题 说明每次循环块都是重新声明的i值。但是这样的话，i值又是怎么传递给下一轮循环的呢？那么我们是不是可以这样理解
```
{ 
 let i;
  i = 0;
  __status = {i};
}
{ let {i} = __status;
  if (i < 10)  __status = {i};
}   
{ let {i} = __status;
  i++;
  if (i < 10)
      setTimeout(()=>console.log("i:",i), 1000);
      __status = {i};
}
    //...
```
在ES标准中，有一段是关于CreatePerIterationEnvironment，也就是for语句每次循环所要建立环境的步骤，里面有提及有关词法环境的相关步骤(LexicalEnvironment)，这与使用let时会有关。所以，如果你使用了let而不是var，let的变量除了作用域是在for区块中，而且会为每次循环执行建立新的词法环境(LexicalEnvironment)，拷贝所有的变量名称与值到下个循环执行。以最简单的方式改写原先的问题中的代码，相当于下面这样写:
```
{ 
 let i;
 for(i=0;i<10;i++){
  let _i = i;
  console.log(_i);
  i++;
 }
}
```
