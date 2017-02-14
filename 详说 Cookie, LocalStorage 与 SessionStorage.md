# 详说 Cookie, LocalStorage 与 SessionStorage

### cookie
> cookie非常小，它的大小限制为4KB左右。它的主要用途是保存用户登录信息，比如你登录某个网站看到“记住密码”，这通常就是通过在 Cookie 中存入一段辨别用户身份的数据来实现的。

### sessionStorage
> 与locaStorage相似，但保存数据的生命周期不同。sessionStorage 只是可以将一部分数据在当前会话中保存下来，刷新页面数据依旧存在。但当页面关闭后，sessionStorage 中的数据就会被清空。

### localStorage
> HTML5标准新加入的技术，支持Ie8及以上浏览器。

##三者的差异

特性 | cookie | localStorage | sessionStorage
---- | -----  | -----------  | ---
数据的生命周期
