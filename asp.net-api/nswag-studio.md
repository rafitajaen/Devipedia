# NSwag Studio

{% embed url="https://github.com/RicoSuter/NSwag/wiki/NSwagStudio" %}

{% hint style="success" %}
**NuGet packages**

Microsoft.AspNetCore.Mvc.NewtonSoftJson _by Microsoft_
{% endhint %}

{% hint style="success" %}
NuGet packages for WASM

AutoMapper.Extensions.Microsoft.DependencyInjection by Jimmy Bogard

System.IdentityModel.Tokens.J


{% endhint %}

**Step 1: Get OpenAPI .json file**

Open Swagger and Download file

**Step 2: Configure NSwagStudio**

Runtime > Net60

Specification URL > [https://localhost:44342/swagger/v1/swagger.json](https://localhost:44342/swagger/v1/swagger.json) > Create local copy

Outputs > CSharp Client > Active

Outputs > CSharp Client > Namespace > StoreX.Shared.Services.Base

Outputs > CSharp CLient > Generate interfaces for Client classes > Active

Setup Target Directory > C:\Users\RaFiTa\Desktop\API\StoreX\Shared\Services\Base\ServiceClient.cs
