# Identity server 认证流程

oidc-client getUser（从storage），如果没有，request identity-server auth endpoint，auth endpoint 跳转至login（哪配的不知道），return url赋值callback endpoint，callback endpoint跳转至sa callback.html


* known issue： 某种情况下会写不进去cookie，重启chrome解决



====================================================

* localstorage 权限问题
* chrome 插件拦截 common 服务器 js 问题
