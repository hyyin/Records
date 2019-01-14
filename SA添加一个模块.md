Startup:

app.UseCustomAuthentication();

UseCommonMiddleware();

UseCors();

services.AddCustomAPIIdentity(Configuration, ApiResourceConstants.LCMSAPI);

添加 authscope

添加 api resource

修改 identity server api resource + GetApiResources

添加 authtest controller

修改 guicommon common constants

guicommon.js 中： getTargetUrlPrefix



