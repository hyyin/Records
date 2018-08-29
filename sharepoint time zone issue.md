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