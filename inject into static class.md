https://stackoverflow.com/questions/37329354/how-to-use-ihttpcontextaccessor-in-static-class-to-set-cookies

public static void addReplaceCookie(string cookieName, string cookieValue)
{

    if ((HttpContext.Current.Request.Cookies(cookieName) == null))
    {
        // add cookie
        HttpCookie s = new HttpCookie(cookieName);
        s.Value = cookieValue;
        s.Expires = DateTime.Now.AddDays(7);
        HttpContext.Current.Response.Cookies.Add(s);
    }
    else {
        // ensure cookie value is correct 
        HttpCookie existingSchoolCookie = HttpContext.Current.Request.Cookies(cookieName);
        existingSchoolCookie.Expires = DateTime.Now.AddDays(7);
        existingSchoolCookie.Value = cookieValue;
        HttpContext.Current.Response.Cookies.Set(existingSchoolCookie);
    }

}

===================================================================================================

public class MyStaticHelperClass {
    private static IHttpContextAccessor httpContextAccessor;
    public static void SetHttpContextAccessor(IHttpContextAccessor  accessor) {
        httpContextAccessor = accessor;
    }

    public static void addReplaceCookie(string cookieName, string cookieValue) {
        var HttpContext = httpContextAccessor.HttpContext;
        if (HttpContext.Request.Cookies(cookieName) == null) {
            // add cookie
            HttpCookie s = new HttpCookie(cookieName);
            s.Value = cookieValue;
            s.Expires = DateTime.Now.AddDays(7);
            HttpContext.Response.Cookies.Add(s);
        } else {
            // ensure cookie value is correct 
            HttpCookie existingSchoolCookie = HttpContext.Request.Cookies(cookieName);
            existingSchoolCookie.Expires = DateTime.Now.AddDays(7);
            existingSchoolCookie.Value = cookieValue;
            HttpContext.Response.Cookies.Set(existingSchoolCookie);
        }
    }
}
You would configure your class during start up

public IServiceProvider ConfigureServices(IServiceCollection service) {
    services.AddTransient<IMyService, MyService>();
    services.AddMvc();

    //this would have been done by the framework any way after this method call;
    //in this case you call the BuildServiceProvider manually to be able to use it
    var serviceProvider = services.BuildServiceProvider();

    //here is where you set you accessor
    var accessor = serviceProvider.GetService<IHttpContextAccessor>()
    MyStaticHelperClass.SetHttpContextAccessor(accessor);

    return serviceProvider;
}
Now with that done. I would still strongly advise converting your static class into a service whose concrete implementation would use the IHttpContextAccessor as a dependency that can be injected via its constructor.

public interface ICookieService {
    void AddReplaceCookie(string cookieName, string cookieValue);
}

public class CookieService : ICookieService {
    IHttpContextAccessor httpContextAccessor;
    public CookieService(IHttpContextAccessor httpContextAccessor) {
        this.httpContextAccessor = httpContextAccessor;
    }
    public void AddReplaceCookie(string cookieName, string cookieValue) {
        var HttpContext = httpContextAccessor.HttpContext;
        if (HttpContext.Request.Cookies(cookieName) == null) {
            // add cookie
            HttpCookie s = new HttpCookie(cookieName);
            s.Value = cookieValue;
            s.Expires = DateTime.Now.AddDays(7);
            HttpContext.Response.Cookies.Add(s);
        } else {
            // ensure cookie value is correct 
            HttpCookie existingSchoolCookie = HttpContext.Request.Cookies(cookieName);
            existingSchoolCookie.Expires = DateTime.Now.AddDays(7);
            existingSchoolCookie.Value = cookieValue;
            HttpContext.Response.Cookies.Set(existingSchoolCookie);
        }
    }
}
...that could then be registered with the Services collection...

public void ConfigureServices(IServiceCollection service) {
    services.AddTransient<ICookieService, CookieService>();
    services.AddMvc();
}
...and be available for injection into classes that have need of it's use.

public class SomeClassThatNeedCookieServicesController : Controller {
    ICookieService cookieService;

    public SomeClassThatNeedCookieServicesController(ICookieService cookieService) {
        this.cookieService = cookieService;
    }
}