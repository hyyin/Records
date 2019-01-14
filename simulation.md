需求：

simulation下只能view，edit api 抛特定异常，暂时不控制前台按钮

simulate时记录simulate前的url，退出simulate时返回./ 在另一个instance上登陆时需要keep simulate状态么 [状态存在localstorage里？]

ajax请求时带一个simulate状态，替换user的token，

----

实现，localstorage存当前user是否是simulate的，sessionstorage赋值防止其他session影响localstorage状态

---

role和role之间能不能互相simulate：

role level----- role level









