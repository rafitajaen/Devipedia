# Database Creation

There are 2 different approaches to create your Database:

* DB First.
* Code First : (More aligned with agile development). You build onto the DB in accordance with the app development.

We will use **Entity Framework Core** that is a modern object-database mapper for .NET. It supports LINQ queries, change tracking, updates, and schema migrations. EF Core works with many databases, including SQL Database (on-premises and Azure), SQLite, MySQL, PostgreSQL, and Azure Cosmos DB.

{% hint style="success" %}
**NuGet packages to download**

* Microsoft.EntityFrameworkCore.SqlServer _by Microsoft_
* Microsoft.EntityFrameworkCore.Tools _by Microsoft_
* Microsoft.EntityFrameworkCore.Design _by Microsoft_
{% endhint %}

### Database First WorkFlow

Create DB > Create Tables > Scaffold

#### Connect to an existing Database

VS2022 > Server Explorer > Connect to DB > MS SQL Server > localhost\sqlexpress

#### Create a brand new DB

VS2022 > Server Explorer > Create New SQL DB > .\sqlexpress > "BookStoreDb"

#### Add a Simple Table to a DB

Server Explorer > BookStoreDb > Add New Table > CODE > Update > Update DB

```sql
CREATE TABLE [dbo].[Authors]
(
    [Id] INT NOT NULL PRIMARY KEY IDENTITY,
    [FirstName] NVARCHAR(50) NULL,
    [LastName] NVARCHAR(50) NULL,
    [Bio] NVARCHAR(250) NULL
)
```

#### Add a Table with a Foreign Key

BookStoreDb > Add New Table > CODE > Update > Update DB > CODE 2 > Update&#x20;

```sql
CREATE TABLE [dbo].[Books]
(
    [Id] INT NOT NULL PRIMARY KEY IDENTITY,
    [Title] NVARCHAR(50) NULL,
    [Year] INT NULL,
    [ISBN] NVARCHAR(50) NOT NULL UNIQUE,
    [Summary] NVARCHAR(250) NULL,
    [Image] NVARCHAR(50) NULL,
    [Price] DECIMAL(18, 2) NULL,
    [AuthorId] INT NULL    
)
```

```sql
//Add Foreign Key after Update DB previously
CONSTRAINT [FK_Books_ToTable] FOREIGN KEY ([AuthorId]) REFERENCES [Authors]([Id])
```

#### Scaffold Database

We need to let our app know that it should be able to connect to a DB. In order to do that, we need to tell EntityFramework where to look for the DB.

{% code title="appsettings.json" %}
```json
"ConnectionStrings": {
    "BookStoreAppDbConnection": "Server=localhost\\sqlexpress;Database=BookStoreDb;Trusted_Connection=True;MultipleActiveResultSets=true"
  }
```
{% endcode %}

{% code title="Tools > Package Manager" %}
```bash
PM > Scaffold-DbContext 'Server=localhost\\sqlexpress;Database=BookStoreDb;Trusted_Connection=True;MultipleActiveResultSets=true' Microsoft.EntityFrameworkCore.SqlServer -ContextDir Data -OutputDir Data
```
{% endcode %}

```csharp
using Microsoft.EntityFrameworkCore;

//Update next line with your own DbContext
using BookStoreApp.API.Data;

// Adding services to the container.
var connString = builder.Configuration.GetConnectionString("BookStoreAppDbConnection");
builder.Services.AddDbContext<BookStoreDbContext>(options => options.UseSqlServer(connString));
```

### Code First WorkFlow

Create Model > Edit DbContext with that model > add-migration (in Package Manager)
