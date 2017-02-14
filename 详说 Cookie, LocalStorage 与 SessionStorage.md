# 详说 Cookie, LocalStorage 与 SessionStorage

## cookie
> 一般由服务器生成，可设置失效时间。如果在浏览器端生成Cookie，默认是关闭浏览器后失效。cookie 确实非常小，它的大小限制为4KB左右。与服务器端通信	每次都会携带在HTTP头中，如果使用cookie保存过多数据会带来性能问题

## sessionStorage
> 仅在当前会话下有效，关闭页面或浏览器后被清除。一般为5MB
