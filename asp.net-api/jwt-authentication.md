---
description: https://jwt.io/
---

# JWT Authentication

{% hint style="success" %}
**NuGet packages**

* Microsoft.AspNetCore.Authentication.JwtBearer _by Microsoft_
{% endhint %}

**Step 1: Extend app settings**

{% code title="appsettings.json" %}
```json
"JwtSettings": {
    "Issuer": "StoreX",
    "Audience": "StoreXClient",
    "Duration": 1
  }
```
{% endcode %}

**Step 2: Create a secret to store JWT Key**

StoreX.Server > Manage User Secrets

{% code title="secrets.json" %}
```csharp
"JwtSettings": {
    "Key": "b69d3017-89be-4215-af9f-ce9fc19a1539"
  }
```
{% endcode %}

**Step 3: Add configuration to Program.cs**

{% code title="Program.cs" %}
```csharp
using Microsoft.AspNetCore.Authentication.JwtBearer;
using Microsoft.IdentityModel.Tokens;
using System.Text;

// Add Authentication to Services
builder.Services.AddAuthentication(options =>
{
    options.DefaultAuthenticateScheme = JwtBearerDefaults.AuthenticationScheme;
    options.DefaultChallengeScheme = JwtBearerDefaults.AuthenticationScheme;
})
    .AddJwtBearer(options =>
    {
        options.TokenValidationParameters = new TokenValidationParameters
        {
            ValidateIssuerSigningKey = true,
            ValidateIssuer = true,
            ValidateAudience = true,
            ValidateLifetime = true,
            ClockSkew = TimeSpan.Zero,
            ValidIssuer = builder.Configuration["JwtSettings:Issuer"],
            ValidAudience = builder.Configuration["JwtSettings:Audience"],
            IssuerSigningKey = new SymmetricSecurityKey(Encoding.UTF8.GetBytes(builder.Configuration["JwtSettings:Key"]))
        };
    });
  
// Use Authorization and Authentication
app.UseAuthentication();
app.UseAuthorization();
```
{% endcode %}

**Step 4: Create GenerateTokens Method to AuthController**

{% code title="AuthController.cs" %}
```csharp
private async Task<string> GenerateToken(StoreUser user)
{
    var securitykey = new SymmetricSecurityKey(Encoding.UTF8.GetBytes(configuration["JwtSettings:Key"]));
    var credentials = new SigningCredentials(securitykey, SecurityAlgorithms.HmacSha256);

    var roles = await userManager.GetRolesAsync(user);
    var roleClaims = roles.Select(q => new Claim(ClaimTypes.Role, q)).ToList();

    var userClaims = await userManager.GetClaimsAsync(user);

    var claims = new List<Claim>
    {
        new Claim(JwtRegisteredClaimNames.Sub, user.UserName),
        new Claim(JwtRegisteredClaimNames.Jti, Guid.NewGuid().ToString()),
        new Claim(JwtRegisteredClaimNames.Email, user.Email),
        new Claim("uid", user.Id)
    }
    .Union(userClaims)
    .Union(roleClaims);

    var token = new JwtSecurityToken(
        issuer: configuration["JwtSettings:Issuer"],
        audience: configuration["JwtSettings:Audience"],
        claims: claims,
        expires: DateTime.UtcNow.AddHours(Convert.ToInt32(configuration["JwtSettings:Duration"])),
        signingCredentials: credentials
    );

    return new JwtSecurityTokenHandler().WriteToken(token);
}
```
{% endcode %}

**Step 5: Add it to Login Endpoint**

{% code title="AuthController.cs" %}
```csharp
[HttpPost]
[Route("login")]
public async Task<ActionResult<AuthResponseDto>> Login(LoginUserDto userDto)
{
    logger.LogInformation($"Login Attempt for {userDto.Email}");

    try
    {
        var user = await userManager.FindByEmailAsync(userDto.Email);
        var isPassValid = await userManager.CheckPasswordAsync(user, userDto.Password);

        if (user == null || !isPassValid)
        {
            return Unauthorized(userDto);
        }
        
        // Generate Token
        string tokenString = await GenerateToken(user);

        var response = new AuthResponseDto
        {
            Email = userDto.Email,
            Token = tokenString,
            UserId = user.Id,
        };

        return response;

    }
    catch (Exception ex)
    {
        logger.LogError(ex, $"Something went worng in the {nameof(Login)}");

        return Problem($"Something went worng in the {nameof(Login)}", statusCode: 500);
    }
}
```
{% endcode %}

**Step 6: Create a Model for AuthResponse**

{% code title="AuthResponseDto.cs" %}
```csharp
public class AuthResponseDto
{
    public string UserId { get; set; }
    public string Token { get; set; }
    public string Email { get; set; }
}
```
{% endcode %}

