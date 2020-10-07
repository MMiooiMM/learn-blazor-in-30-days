Microsoft.Extensions.Http

Nuget = Microsoft.AspNetCore.Components.WebAssembly.Authentication


```csharp
@using Microsoft.AspNetCore.Components.Authorization
<AuthorizeView>
    <Authorized>
        <h1>Hello, @context.User.Identity.Name!</h1>
        <p>You can only see this content if you're authenticated.</p>
    </Authorized>
    <Authorizing>
        <h1>Authentication in progress</h1>
        <p>You can only see this content while authentication is in progress.</p>
    </Authorizing>
</AuthorizeView>
```

* https://docs.microsoft.com/zh-tw/aspnet/core/blazor/security/?view=aspnetcore-3.1#authorizeview-component

* https://docs.microsoft.com/zh-tw/aspnet/core/blazor/security/webassembly/hosted-with-identity-server?view=aspnetcore-3.1&tabs=visual-studio

* https://docs.microsoft.com/zh-tw/aspnet/core/blazor/security/?view=aspnetcore-3.1