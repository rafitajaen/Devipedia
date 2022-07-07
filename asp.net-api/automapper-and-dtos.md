# AutoMapper and DTOs

{% hint style="info" %}
**DTO** ==> Data Transfer Object
{% endhint %}

We will create an abstraction of what we want to store and show to the user only what really needs to interact with the DB.

{% hint style="success" %}
**NuGet Packages to download**

AutoMapper.Extensions.Microsoft.DependencyInjection _by Jimmy Bogard_
{% endhint %}

#### Step 0: Create Mapper Config

_<mark style="color:blue;">**Solution Explorer > New Folder Configurations > New File**</mark>_&#x20;

{% code title="MapperConfig.cs" %}
```csharp
using AutoMapper;

namespace BookStoreApp.API.Configurations
{
    public class MapperConfig : Profile
    {
        public MapperConfig()
        {
            //Create a Map for every action in a controller
            CreateMap<AuthorReadOnlyDto, Author>().ReverseMap();
            
        }
    }
}
```
{% endcode %}

#### Step 1: Add Mappers Profile to Services

We Add Mappers to Services to be able to inject that config wherever we need.

{% code title="Program.cs" %}
```csharp
builder.Services.AddAutoMapper(typeof(MapperConfig));
```
{% endcode %}

#### Step 2: Create DTOs

{% hint style="info" %}
If you have a `BaseEntity` Model you must to create a DTO for it.
{% endhint %}

_<mark style="color:blue;">**Solution Explorer > New Folder Models (or DTOs) > New Folder Author > New File**</mark>_

{% code title="Author/AuthorCreateDto.cs" %}
```csharp
using System.ComponentModel.DataAnnotations;

namespace BookStoreApp.API.Models.Author
{
    public class AuthorCreateDto
    {
        [Required]
        [StringLength(50)]
        public string FirstName { get; set; }

        [Required]
        [StringLength(50)]
        public string LastName { get; set; }

        [StringLength(250)]
        public string? Bio { get; set; }
    }
}
```
{% endcode %}

#### Step 3: Inject DTO in Controllers

{% code title="AuthorsController.cs" %}
```csharp
using AutoMapper;

using BookStoreApp.API.Data;
using BookStoreApp.API.Models.Author;

    private readonly BookStoreDbContext _context;
    private readonly IMapper mapper;
    private readonly ILogger<AuthorsController> logger;

    public AuthorsController(BookStoreDbContext context, IMapper mapper, ILogger<AuthorsController> logger))
    {
        _context = context;
        this.mapper = mapper;
        this.logger = logger;
    }

public async Task<ActionResult<AuthorCreateDto>> PostAuthor(AuthorCreateDto authorDto)
{
    var author = mapper.Map<Author>(authorDto);
    await authorsRepository.AddAsync(author);

    return CreatedAtAction(nameof(GetAuthor), new { id = author.Id }, author);  
}
```
{% endcode %}

```csharp
// Equivalent code from above to understand why Mappers are created.

public async Task<ActionResult<Author>> PostAuthor(Author authorComplete)
{
    var authorDto = new Author 
    {
        Bio = authorComplete.Bio,
        FirstName = authorComplete.FirstName,
        LastName = authorComplete.LastName
    };
    await authorsRepository.AddAsync(authorDto);
    
    return CreatedAtAction(nameof(GetAuthor), new { id = authorDto.Id }, authorDto);
}
```
