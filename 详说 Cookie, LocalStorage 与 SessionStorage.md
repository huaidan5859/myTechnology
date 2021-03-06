# 详说 Cookie, LocalStorage 与 SessionStorage

### cookie
> cookie非常小，它的大小限制为4KB左右。它的主要用途是保存用户登录信息，比如你登录某个网站看到“记住密码”，这通常就是通过在 Cookie 中存入一段辨别用户身份的数据来实现的。

### sessionStorage
> 与locaStorage相似，但保存数据的生命周期不同，它是会话级的本地存储。sessionStorage 只是可以将一部分数据在当前会话中保存下来，刷新页面数据依旧存在。但当页面关闭后，sessionStorage 中的数据就会被清空。

### localStorage
> HTML5标准新加入的技术，支持Ie8及以上浏览器。它是一种持久化的本地存储，非主动删除则数据永久存在

##三者的差异

特性 | cookie | localStorage | sessionStorage
---- | -----  | -----------  | ---
数据的生命周期 |   一般为服务器设置，可设置失效时间。如果在浏览器端生成cookie，浏览器关闭后立即失效 | 除非被清除，否则永久存在 | 仅在当前会话下有效，关闭页面或浏览器后被清除*（不同浏览器标签页即使为同一个页面也不能共享session数据）*
存放数据大小 | 限制为4KB左右 浏览器可能还限制了用户计算机存储的cookie数量（如允许每个站点最多存储20个cookies，超过则删除旧的；有些浏览器还对所有站点的cookie总数作出限制，如300 | 一般为5MB | 一般为5MB
与服务器通信 | 每次都会携带在HTTP头中，如果使用cookie保存数据过多会带来性能问题 | 仅在客户端或浏览器中保存，不与服务器通信 | 仅在客户端或浏览器中保存，不与服务器通信

此外，Web Storage拥有setItem,getItem,removeItem,clear等方法，不像cookie需要前端开发者自己封装setCookie，getCookie。
## 安全性考虑

需要注意的是，不是什么数据都适合放在 Cookie、localStorage 和 sessionStorage 中的。使用它们的时候，需要时刻注意是否有代码存在 XSS 注入的风险。因为只要打开控制台，你就随意修改它们的值，也就是说如果你的网站中有 XSS 的风险，它们就能对你的 localStorage 肆意妄为。所以千万不要用它们存储你系统中的敏感数据。

## 关于cookie删除
**如果cookie存入时携带了domain信息，删除时一定要设定domain和path才能正确删除。**

## web storage
storage提供了storage事件来监听本地存储数据变化；
```
if(window.addEventListener){
    window.addEventListener("storage",handle_storage,false);
}else if(window.attachEvent){
    window.attachEvent("onstorage",handle_storage);
}
function handle_storage(e){
    if(!e){e=window.event;}
}
```
