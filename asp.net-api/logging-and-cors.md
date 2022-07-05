# Logging and CORS

### Logging using SeriLog

We will use for tracking issues, performance and debugging.

{% hint style="success" %}
**NuGet packages to download**

* Serilog.AspNetCore _by Microsoft_
* Serilog.Expressions _by Serilog_
* Serilog.Sinks.Seq _by Serilog_
{% endhint %}

#### Step 1: Register SeriLog in the app builder

{% code title="Program.cs" %}
```csharp
using Serilog;

// ctx = Context
// lc = Log Config
builder.Host.UseSerilog((ctx, lc) => 
    lc.WriteTo.Console().ReadFrom.Configuration(ctx.Configuration));
```
{% endcode %}

#### Step 2: Add SeriLog Config

{% code title="appsettings.json" %}
```json
"Serilog": {
    "MinimumLevel": {
      "Default": "Information",
      "Override": {
        "Microsoft": "Warning",
        "Microsoft.Hosting.Lifetime": "Information"
      }
    },
    "WriteTo": [
      {
        "Name": "File",
        "Args": {
          "path": "./logs/log-.txt",
          "rollingInterval": "Day"
        }
      },
      {
        "Name": "Seq",
        "Args": { "serverUrl": "http://localhost:5341" }
      }
    ]
  }
```
{% endcode %}

{% code title="appsettings.Development.jsonn" %}
```
{}
```
{% endcode %}

#### Setp 3: Download Seq (Logging Interface)

{% embed url="https://datalust.co/seq" %}

### CORS Policy Configuration

Restrict the machines that are allowed to access to our API.

Blacklist feature: Allow or reject certain request from certain sources.

{% code title="Program.cs" %}
```csharp
builder.Services.AddCors( options => {
    options.AddPolicy("AllowAll", 
        b => b.AllowAnyMethod()
        .AllowAnyHeader()
        .AllowAnyOrigin());
});

app.UseCors("AllowAll");
```
{% endcode %}
