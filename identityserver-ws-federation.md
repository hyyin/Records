# IdentityServer4 federation

* [WSFederation overview](https://docs.microsoft.com/en-us/dotnet/framework/security/wsfederation-authentication-module-overview)
* [Demo](https://github.com/IdentityServer/IdentityServer4.WsFederation)
* Key words: WSS, WS-Federation, SAML, SOAP, ADFS, ADFS management ...

* [Authenticate users with WS-Federation in ASP.NET Core](https://docs.microsoft.com/en-us/aspnet/core/security/authentication/ws-federation?view=aspnetcore-2.1)

* [Introduction to Identity on ASP.NET Core](https://docs.microsoft.com/en-us/aspnet/core/security/authentication/identity?view=aspnetcore-2.1&tabs=visual-studio#next-steps)

---
思路：
* [signin_external_providers](https://identityserver4.readthedocs.io/en/release/topics/signin_external_providers.html)

identity server 端作为federation gateway，redirect 认证请求 至 adfs server



10.1.53.226
.\administrator
averp12#$
1qaz2wsxE

张健彬(Robin Zhang) 8-13 10:09:36
https://adfs.rp.aveqa.online/adfs/ls/wia?wa=wsignin1.0&wtrealm=https://localhost:44334/&wreply=https://localhost:44334/External/Callback

yang_qiao@rp.aveqa.online
1qaz2wsxE
adfs.rp.aveqa.online 10.1.167.38

张健彬(Robin Zhang) 8-13 10:17:51
https://myleo.rp.edu.sg/corebase

张健彬(Robin Zhang) 8-13 10:18:42
https://perf-lams.rp.aveqa.online/CoreBase

张健彬(Robin Zhang) 8-13 10:27:21
https://github.com/IdentityServer/IdentityServer4.git



Cutting Edge - Cookies, Claims and Authentication in ASP.NET Core

https://msdn.microsoft.com/en-us/magazine/mt842501.aspx



adfs 部署 ： https://docs.microsoft.com/en-us/windows-server/identity/active-directory-federation-services

adfs 2.0 sdk:


https://docs.microsoft.com/en-us/previous-versions/adfs-2.0/ee895355(v%3dmsdn.10)



https://adfs.rp.aveqa.online/adfs/ls/?wtrealm=https://IdentityServer/&wa=wsignin1.0&wreply=http://localhost:12508/signin-wsfed&wctx=CfDJ8EyL2crB3O5Ok23SQAEoSSHdMkXkAx4pmq61o61x8Ipq1EAAN_eNaYSWQ6OWAl2_XJ-wxID1Jf-c14vtIlAOE4J5CAnkF5oJTAAR-VUF3ANnXyRGoHpbcqQf1DvyNagOzFxZK3ooElVW8VnH6_2Vi9-ejSiPm0--oup4xVKU7AboDIcFenzWy9cJLE8V56hwCUImLq-TULvuxwfpK8DSD1M8_kEYpCchVZmKdPeMVYUgC-jHclIpKQgq5LMxXHPaYGz0E2MmhUfzPjgIYUTfihY


主动模式线索：  http://www.it1352.com/13220.html

https://blogs.msdn.microsoft.com/besidethepoint/2012/10/17/request-adfs-security-token-with-powershell/

