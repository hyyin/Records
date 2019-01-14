# Identity server 认证流程

oidc-client getUser（从storage），如果没有，request identity-server auth endpoint，auth endpoint 跳转至login（哪配的不知道），return url赋值callback endpoint，callback endpoint跳转至sa callback.html


* known issue： 某种情况下会写不进去cookie，重启chrome解决



====================================================

* localstorage 权限问题
* chrome 插件拦截 common 服务器 js 问题

========================================================================

多个节点问题， 访问userinfo toekn结点 401

================================

localstorage 没有权限，但是没有报错

================================================================

<meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />

callback 页面


==============================================================================

如何解释 登出后，之前的session不受影响

usermanamger 用的是session storage, oidcclient用的是global storage, don't know why


==================================

simulate case:

window.sessionStorage.setItem("cf:simulated", window.localStorage.getItem("cf:simulated"));

window.CommonUtil.isSimulated = function () {
    //very important
    return window.sessionStorage.getItem("cf:simulated") == "true";
}

确保第一次登陆的时候，同步当前simulate状态，但，其他session，stop simualate时，置localstorage值不会影响其他session simulate状态，避免bug。

window.commonUtil.Simulate(userName)
window.commonUtil.CancelSimulate()
window.commonUtil.isSimulated()

================================================

跨版本认证

https://stackoverflow.com/questions/39642715/asp-net-mvc-4-5-2-connecting-to-identityserver4


http://bitoftech.net/2014/10/27/json-web-token-asp-net-web-api-2-jwt-owin-authorization-server/

owin版本

用 identity server 3解决

            app.UseIdentityServerBearerTokenAuthentication(
                new IdentityServer3.AccessTokenValidation.IdentityServerBearerTokenAuthenticationOptions()
                {
                    Authority = "http://localhost:12508",
                    ValidationMode = IdentityServer3.AccessTokenValidation.ValidationMode.Local,
                    RequiredScopes = new[] { "lcmsAPI" }
                });

 https://stackoverflow.com/questions/40443170/identityserver3-accesstokenvalidation-api-and-identityserver4