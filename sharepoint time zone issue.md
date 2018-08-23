# Reservation site CI

issue:当site region 改变时，edit reservation item的时间后，save之后时区转换不正确：

reason，前台发送utc时间，server端重新转成local时间（这地方有风险，如果浏览器和server不是一个时区，则有问题，本质上，edit item页面的时间只是数字，跟着sharepoint region setting 走即可

[Converting Date and Time Values](https://docs.microsoft.com/en-us/previous-versions/office/developer/sharepoint-2010/ms197282(v%3doffice.14))

sharepoint column 时间赋值的逻辑非常迷乱

