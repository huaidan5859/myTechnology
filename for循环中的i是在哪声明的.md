# for循环中的i是在哪的

```
 for(var i = 0; i < 10; i++){
  console.log(i)
 }
```
经常用到上面格式的for循环，却不是很了解i声明的位置。

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
