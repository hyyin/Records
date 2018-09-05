# Reservation site CI

issue:当site region 改变时，edit reservation item的时间后，save之后时区转换不正确：

reason，前台发送utc时间，server端重新转成local时间（这地方有风险，如果浏览器和server不是一个时区，则有问题，本质上，edit item页面的时间只是数字，跟着sharepoint region setting 走即可

[Converting Date and Time Values](https://docs.microsoft.com/en-us/previous-versions/office/developer/sharepoint-2010/ms197282(v%3doffice.14))

sharepoint column 时间赋值的逻辑非常迷乱

===========================================================

solution: 传递前端 年月日 时间，绕开浏览器时区和server时区之间的转换，直接构造时间

===================================================

Reservation site CI 处理方法：

激活publishing feature， 激活site collection column feature， 将term import到site collection 级别term store，将resoure termset id 添到configuration文件中再激活site 级别feature，

访问_layouts/15/Reservation/Pages/Reservation.aspx

==========================================

遇到一个term column串行问题，开发环境无法重现，无奈用jquery hack ，去掉样式解决


======================================================================

layouts page 版本url：https://insitedev.inpexcorp.com/sites/teamtest4/_layouts/15/Reservation/Pages/Reservation.aspx
page 版本url：https://insitedev.inpexcorp.com/sites/teamtest4/Sub/Pages/TestAgain.aspx
CA url：http://azjwfed01:9999/_admin/FarmServers.aspx
GAC 地址：C:\Windows\Microsoft.NET\assembly\GAC_MSIL\APPSSP2013Reservation\v4.0_1.0.0.0__db86ee054e93729b
外部访问url： http://csportaldwfe.cloudapp.net/sites/teamtest4/Sub/Pages/HomePage.aspx

用户名密码：
inpexone\system_sp_farm
InpexPortal!@

部署命令：

install-spsolution -identity 72549079-e08f-4d51-a0b1-5719f53a392c -GACDeployment -allwebapplications

layouts，master page，webpart 等是 site collection 级别feature 部署的

@@@@ 客户环境使用的是page版本，注意代码的坑

consider point： 编辑单个循环item， search逻辑，冲突逻辑可能都有问题

神坑！


==========================

feature和 meat site 冲突