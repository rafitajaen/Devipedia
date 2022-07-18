# Identity

We don't want every and anybody have acces to the API. EVen if it's an "open" API, we still want to have some restrictions.

**Authentication** means that we verify that the user have access.

**Authorization** means that we verify the user has the permission to do what he is attempting to do.

We will use Microsoft Identity library to implement JWT authentication (Standard for stateless apps)

{% hint style="success" %}
**NuGet packages to download**

* Microsoft.AspNetCore.Identity.EntityFrameworkCore _by Microsoft_
{% endhint %}

**Step 1: Add Identity Configuration**

Probably, you will have multiple DBs in a single project, but you must have all the users in one single DB. That is because Identity Configuration ask for de DbContext where the users data lives.

{% code title="Program.cs" %}
```csharp
using Microsoft.AspNetCore.Identity;
// Add Identity Configuration
builder.Services.AddIdentityCore<StoreUser>() //Default: <IdentityUser>
    .AddRoles<IdentityRole>()
    .AddEntityFrameworkStores<StoreDbContext>();
```
{% endcode %}

**Step 2: Extend IdentityUser**

{% code title="StoreUser.cs" %}
```csharp
using Microsoft.AspNetCore.Identity;

public class StoreUser : IdentityUser
{
    public string FirstName { get; set; }
    public string LastName { get; set; }
}
```
{% endcode %}

**Step 3: Extend DB Context**

{% code title="StoreDbContext.cs" %}
```csharp
using Microsoft.AspNetCore.Identity.EntityFrameworkCore;
public partial class StoreDbContext : IdentityDbContext<StoreUser>
{
    protected override void OnModelCreating(ModelBuilder modelBuilder) 
    {
        // Call the parent constructor to create the model with Identity
        base.OnModelCreating(modelBuilder);
        ...
    }
}
```
{% endcode %}

**Step 4: Seed Test Users and Roles**

{% hint style="success" %}
**GUID Generator**

* [https://www.guidgenerator.com/](https://www.guidgenerator.com/)
{% endhint %}

{% code title="StoreDbContext.cs" %}
```csharp
// Initialize a hasher
var hasher = new PasswordHasher<StoreUser>();

// Seed Users and Roles

modelBuilder.Entity<IdentityRole>().HasData(
    new IdentityRole { Name = "Admin", NormalizedName = "ADMIN", Id = "ae7b95c0-5c9d-4741-a0c9-f06b5a444226" },
    new IdentityRole { Name = "User", NormalizedName = "USER", Id = "3b4cf07b-29c6-4ba2-b46b-3573071b65a4" }
    );

modelBuilder.Entity<StoreUser>().HasData(
    new StoreUser { Email = "admin@storex.com", NormalizedEmail = "ADMIN@STOREX.COM", UserName = "administrator", NormalizedUserName = "ADMINISTRATOR", Id = "308be62b-2394-4821-9c86-25f52ff9cd63", FirstName = "System", LastName = "Admin", PasswordHash = hasher.HashPassword(null, "P@assword1") },
    new StoreUser { Email = "user@storex.com", NormalizedEmail = "user@STOREX.COM", UserName = "user", NormalizedUserName = "USER", Id = "e7f59035-a52d-4cd7-b39f-fae76fe33c6c", FirstName = "Basic", LastName = "User", PasswordHash = hasher.HashPassword(null, "P@assword2") }
    );

modelBuilder.Entity<IdentityUserRole<string>>().HasData(
    new IdentityUserRole<string>
    {
        RoleId = "ae7b95c0-5c9d-4741-a0c9-f06b5a444226",
        UserId = "308be62b-2394-4821-9c86-25f52ff9cd63"
    },
    new IdentityUserRole<string>
    {
        RoleId = "3b4cf07b-29c6-4ba2-b46b-3573071b65a4",
        UserId = "e7f59035-a52d-4cd7-b39f-fae76fe33c6c"
    }
);
```
{% endcode %}

{% hint style="info" %}
Don't forget to <mark style="color:red;">`add-migration`</mark> and <mark style="color:red;">`update database`</mark> after the configuration of the Identity.
{% endhint %}

#### Step 5: Setup Authentication Controllers

We also need API endpoints for the user authentication.

Create UserDto + Register Mappings for UserDto + Create AuthController

{% code title="Models / StoreUserDto.cs" %}
```csharp
public class LoginUserDto
{
    [Required]
    [EmailAddress]
    public string Email { get; set; }
    [Required]
    public string Password { get; set; }
}
 
public class StoreUserDto : LoginUserDto
{
    [Required]
    public string UserName { get; set; }

    public string FirstName { get; set; } = string.Empty;

    public string LastName { get; set; } = string.Empty;
}   
    
```
{% endcode %}

{% code title="MapperConfig.cs" %}
```csharp
CreateMap<StoreUserDto, StoreUser>().ReverseMap();
```
{% endcode %}

{% code title="AuthController.cs" %}
```csharp
[Route("api/[controller]")]
[ApiController]
public class AuthController : ControllerBase
{
    private readonly ILogger<AuthController> logger;
    private readonly IMapper mapper;
    private readonly UserManager<StoreUser> userManager;

    public AuthController(ILogger<AuthController> logger, IMapper mapper, UserManager<StoreUser> userManager)
    {
        this.logger = logger;
        this.mapper = mapper;
        this.userManager = userManager;
    }

    [HttpPost]
    [Route("register")]
    public async Task<IActionResult> Register(StoreUserDto userDto)
    {
        logger.LogInformation($"Registration Attempt for {userDto.Email}");

        try
        {
            if (userDto == null)
            {
                return BadRequest("Insufficent Data Provided");
            }

            var user = mapper.Map<StoreUser>(userDto);
            var result = await userManager.CreateAsync(user, userDto.Password);

            if (!result.Succeeded)
            {
                foreach (var error in result.Errors)
                {
                    ModelState.AddModelError(error.Code, error.Description);
                }
                return BadRequest(ModelState);
            }

            // Auto-assign User Role to new Registrations
            await userManager.AddToRoleAsync(user, "User");

            return Accepted();
        }
        catch (Exception ex)
        {
            logger.LogError(ex, $"Something went worng in the {nameof(Register)}");

            return Problem($"Something went worng in the {nameof(Register)}", statusCode: 500);
        }
    }

    [HttpPost]
    [Route("login")]
    public async Task<IActionResult> Login(LoginUserDto userDto)
    {
        logger.LogInformation($"Login Attempt for {userDto.Email}");

        try
        {
            var user = await userManager.FindByEmailAsync(userDto.Email);
            var isPassValid = await userManager.CheckPasswordAsync(user, userDto.Password);

            if (user == null || !isPassValid)
            {
                return NotFound();
            }

            return Accepted();

        }
        catch (Exception ex)
        {
            logger.LogError(ex, $"Something went worng in the {nameof(Login)}");

            return Problem($"Something went worng in the {nameof(Login)}", statusCode: 500);
        }
    }
```
{% endcode %}
