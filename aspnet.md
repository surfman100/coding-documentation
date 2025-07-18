# ASP NET tips

## Data Transfer Object

Encapsulate information back from calls using a standard model that can return data, messages and more

```
public class DataTransferObject
{
  public List<DTOMessage> Messages {get;set;}
  public dynamic Result {get;set;}
}
```

```
public class DTOMessage
{
    public DTOMessage()
    { }

    public DTOMessage(DTOMessageTypeEnum type, String message)
    {
        this.Type = type;
        this.Message = message;
    }

    public DTOMessageTypeEnum Type { get; set; }
    public String Message { get; set; }
}
```

```
public enum DTOMessageTypeEnum
{
    Success = 1,
    Info = 2,
    Warning = 3,
    Error = 4
}
```

## Logging

If you want to see the logging messages from dependant assemblies you must reference them directly from Top Project. Its not enough to have them referenced by another dependency

## IIS Logging
1. create "logs" folder under IIS application direction
2. grant everyone permissions on this folder
3. update web.config: stdoutLogEnabled="true" 

## ViewComponents in a seperate assembly
1. Define the ViewComponent in the library assembly e.g. MyTestViewComponent
2. When using the ViewComponent in the calling application, remember to omit the "ViewComponent" in the name!
e.g. @await Component.InvokeAsync("MyTest",null)

## NET Cookie Authentication
```
 public class AccountController : Controller
    {   
        /// <summary>
        /// Login method called by Cookie authentication code
        /// </summary>
        /// <param name="returnUrl"></param>
        /// <returns></returns>
        /// <remarks>
        /// App Centre applications are setup to use Cookie based authentication
        /// When a user first navigates to an application, the authenication logic see that they are not logged in yet
        /// and calls the default controller action "Account\Login"
        /// </remarks>
        [HttpGet]
        [AllowAnonymous]
        public async Task<IActionResult> Login(string returnUrl = "")
        {
```

add roles to the claimsidentity

```
 #region build core claims list to be used in token and on identity
            string applicationName = _config.GetSection("Security")["ApplicationName"];
            List<Claim> coreClaims = new List<Claim>
            {
                new Claim(ClaimTypes.Name, loggedOnUser.FullName),
                new Claim("application", applicationName)
            };
            #endregion

            #region start building identity
            var identity = new ClaimsIdentity(CookieAuthenticationDefaults.AuthenticationScheme);
            foreach(Claim claim in coreClaims)
            {
                identity.AddClaim(claim);
            }
            identity.AddClaim(new Claim(ClaimTypes.GivenName, loggedOnUser.FirstName));
            identity.AddClaim(new Claim(ClaimTypes.Surname, loggedOnUser.LastName));
            identity.AddClaim(new Claim(ClaimTypes.Email, loggedOnUser.Email));
            identity.AddClaim(new Claim(ClaimTypes.OtherPhone, loggedOnUser.Phone));
            identity.AddClaim(new Claim(ClaimTypes.MobilePhone, loggedOnUser.MobileNumber));
            #endregion
```

finally, sign in

```
      #region create token and add to identity
      var token = _tokenService.GenerateToken(coreClaims.ToArray(), DateTime.Now);
      identity.AddClaim(new Claim("api_token", token));
      #endregion

      var principal = new ClaimsPrincipal(identity);
      await HttpContext.SignInAsync(CookieAuthenticationDefaults.AuthenticationScheme, principal);
```

oh, and finally finally, in the target project Program.cs
```
//adds cookie authentication
builder.Services.AddAuthentication(CookieAuthenticationDefaults.AuthenticationScheme).AddCookie();
```

## Application Parts
Very handy for sucking in methods etc in other assemblies
```
//this section hooks up the security service
var assembly1 = typeof(MyProject.Namespace.Controller1).Assembly;
var assembly2 = typeof(MyProject.Namespace.APIController2).Assembly;
ApplicationPartManager manager = builder.Services.AddControllersWithViews(config =>
{
    var policy = new AuthorizationPolicyBuilder()
                        .RequireAuthenticatedUser()
                        .RequireRole(builder.Configuration.GetSection("Security")["DefaultRequiredRole"])
                        .Build();
    config.Filters.Add(new AuthorizeFilter(policy));
}).PartManager;

builder.Services.AddControllers().AddJsonOptions(options =>
{
    options.JsonSerializerOptions.PropertyNamingPolicy = null;
});

manager.ApplicationParts.Add(new AssemblyPart(assembly1));
manager.ApplicationParts.Add(new AssemblyPart(assembly2));
```

