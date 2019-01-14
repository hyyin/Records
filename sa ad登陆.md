https://stackoverflow.com/questions/49682644/asp-net-core-2-0-ldap-active-directory-authentication

ASP.NET Core 2.0 LDAP Active Directory Authentication


楚垚(Matt Chu) 10-9 10:47:31
C:\Codes\trunk\Features\CB\CoreBase.Web\Controllers\LoginController.cs
ADLogin()  这个方法是处理login信息，连AD验证user的；
ADAutoLogin() 这个方法是AD Server验证通过了，去连db做auth并且初始化token的。
最后会调ServiceFactory.AuthenticationService.Login(identity)，来set当前登录user信息。

楚垚(Matt Chu) 10-9 10:47:51
看一遍，提取下这几个步骤就行了。


==============================================

10.1.167.36 rp.aveqa.online  QA域

averp12#$


=============================================

https://msdn.microsoft.com/en-us/library/ms180835

getting started in system.directory services


https://docs.microsoft.com/en-us/windows-server/identity/identity-and-access

https://docs.microsoft.com/en-us/windows-server/identity/ad-fs/operations/configure-ad-fs-to-authenticate-users-stored-in-ldap-directories

ws-trust active


  private static GenericXmlSecurityToken GetToken(string username, string password, string url, string audienceUrl)
    {
        var factory = new WSTrustChannelFactory(new Microsoft.IdentityModel.Protocols.WSTrust.Bindings.UserNameWSTrustBinding(SecurityMode.TransportWithMessageCredential), new EndpointAddress(url));
        factory.Credentials.UserName.UserName = username;
        factory.Credentials.UserName.Password = password;

        factory.Credentials.ServiceCertificate.Authentication.CertificateValidationMode = X509CertificateValidationMode.None;
        factory.TrustVersion = TrustVersion.WSTrust13;
        WSTrustChannel channel = null;

        var rst = new RequestSecurityToken
        {
            RequestType = WSTrust13Constants.RequestTypes.Issue,
            AppliesTo = new EndpointAddress(audienceUrl),
            KeyType = WSTrust13Constants.KeyTypes.Bearer,
        };
        channel = (WSTrustChannel)factory.CreateChannel();
        return channel.Issue(rst) as GenericXmlSecurityToken;
    }


    
4
down vote
Although this is an old question, I couldn't find any non-third-party answer on the internet, so here it is:

To replace UserNameWSTrustBinding in .NET 4.5, use the following:

var binding = new WS2007HttpBinding(SecurityMode.{what it was before});
binding.Security.Message.ClientCredentialType = MessageCredentialType.UserName;






public class UserNameWSTrustBinding : WS2007HttpBinding
{
    public UserNameWSTrustBinding()
    {
        Security.Mode = SecurityMode.TransportWithMessageCredential;
        Security.Message.EstablishSecurityContext = false;
        Security.Message.ClientCredentialType = MessageCredentialType.UserName;
    }
}



https://stackoverflow.com/questions/29481611/authentication-in-c-sharp-with-active-directory
================
string endpointUri = string.Format("https://{0}/adfs/services/trust/13/usernamemixed", _serverName);

var factory = new WSTrustChannelFactory(new UserNameWSTrustBinding(), endpointUri)
    {
        TrustVersion = TrustVersion.WSTrust13
    };

factory.Credentials.UserName.UserName = "UserName";
factory.Credentials.UserName.Password = "password";

var rst = new RequestSecurityToken
{
    RequestType = RequestTypes.Issue,
    AppliesTo = new EndpointReference(_relyingPartyUri),
    KeyType = KeyTypes.Symmetric
};

var channel = factory.CreateChannel();

return channel.Issue(rst);

https://docs.microsoft.com/en-us/powershell/module/adfs/get-adfsendpoint?view=win10-ps   :: get-endpoint





https://www.codeproject.com/Questions/1078915/Implementing-active-authentication-using-adfs








