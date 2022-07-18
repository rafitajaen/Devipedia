# Identity and JWT Auth

We don't want every and anybody have acces to the API. EVen if it's an "open" API, we still want to have some restrictions.

**Authentication** means that we verify that the user have access.

**Authorization** means that we verify the user has the permission to do what he is attempting to do.

We will use Microsoft Identity library to implement JWT authentication (Standard for stateless apps)

{% hint style="success" %}
**NuGet packages to download**

* Microsoft.AspNetCore.Identity.EntityFrameworkCore _by Microsoft_
{% endhint %}

Step 1: Add Identity Configuration

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

Step 2: Extend IdentityUser

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

Step 3: Extend DB Context

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

Step 4: Seed Test Users and Roles

{% hint style="success" %}
**GUID Generator**

* [https://www.guidgenerator.com/](https://www.guidgenerator.com/)
{% endhint %}

{% hint style="info" %}
Don't forget to add-migration and update database after the configuration of the Identity.
{% endhint %}
