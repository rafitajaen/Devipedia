# Controllers

When we Scaffold a DB, it automatically creates **classes** that has properties that models all the fields that we added to a table (Eg. : Authors Table) in our DB.

{% code title="Author.cs" %}
```csharp
using System;
using System.Collections.Generic;

namespace BookStoreApp.API.Data
{
    public partial class Author
    {
        public Author()
        {
            Books = new HashSet<Book>();
        }

        public int Id { get; set; }
        public string? FirstName { get; set; }
        public string? LastName { get; set; }
        public string? Bio { get; set; }

        public virtual ICollection<Book> Books { get; set; }
    }
}
```
{% endcode %}

{% hint style="info" %}
**partial class** ==> We can extends it anywhere within its namespace if we need to.
{% endhint %}

This **class** is a representation of a single record in our (Authors) Table that is actually a collection. (DBSet of Author items)

{% code title="BookStoreDbContext.cs " %}
```csharp
public virtual DbSet<Author> Authors { get; set; } = null!;
```
{% endcode %}

### Creating Controllers

Now, our task is create a controller that will allow requests to come in from any client to interact to the data that is being stored in our (Authors) table.

#### Step 1: Create controllers individually

_<mark style="color:blue;">**Solution Explorer > Controllers > Add New Controller > API Controller with actions using EF**</mark>_&#x20;

#### Step 2: Add Controllers to Services

{% code title="Program.cs" %}
```csharp
builder.Services.AddControllers();
```
{% endcode %}

#### CRUD

* Create ==> POST
* Read ==> GET
* Update ==> PUT
* Delete ==> DELETE

{% hint style="danger" %}
_If you get an error, just update all NuGet packages._
{% endhint %}

#### Response Methods

```csharp
Ok();
NotFound();
BadRequest();
NoContent();
```
