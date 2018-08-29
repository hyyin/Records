# SA permission checker 报此错误

后经排查，确定，正常情况下，一个context一个_userService, 一个dbcontext，但前台多次并发请求同一个action时，则取出同一userService实例

 _userService = (IUserService)context.HttpContext.RequestServices.GetService(typeof(IUserService));

 =============================================

 ILSpy：

 https://github.com/icsharpcode/ILSpy/releases

 .net core assembly 地址：

 C:\Program Files\dotnet\shared\Microsoft.NETCore.App\2.0.5

 .net core nuget assembly 地址：

 C:\Users\yinha\.nuget\packages\microsoft.entityframeworkcore\2.1.1\lib\netstandard2.0



 ================================================================

  using (var scope = SAServiceProvider.ServiceProvider.CreateScope())
                    {
                        _userService = (IUserService)scope.ServiceProvider.GetService(typeof(IUserService));
                        _closureMappingService = (IClosureMappingService)scope.ServiceProvider.GetService(typeof(IClosureMappingService));

 //_userService = (IUserService)SAServiceProvider.ServiceProvider.GetService(typeof(IUserService));
                        //_closureMappingService = (IClosureMappingService)SAServiceProvider.ServiceProvider.GetService(typeof(IClosureMappingService));

无论是哪种方式，都有几率取出相同的service instance， 更诡异的是，就算service instance都不相同，在context底层也会出现同样的错误，和addscope，addtransit 无关。和autofactor有关？

最后无奈，加锁解决


============================================= 