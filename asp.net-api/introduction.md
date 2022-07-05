# Introduction

### Installation

[Visual Studio 2022](https://visualstudio.microsoft.com/downloads/)

* ASP.NET
* Azure Development
* Node.js Development
* .NET Desktop Development

[SQL Server 2019 (Express) ](https://www.microsoft.com/es-es/sql-server/sql-server-downloads)

[Microsoft SQL Server Management Studio (SSMS)](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms)

[Postman](https://www.postman.com/downloads/) (Create Workspace > HTTP Request)

(apipheny.io/free-api)

### How to Start

1. Create a Blank Solution in VS2022
2. Create ASP.NET Core Web API (BookstoreApp.API)

### Project Structure and Files

Solution (.sln) : (One Problem --> One Solution). Folder to register of all projects.

&#x20; \| - Project (XML) : Configuration File

&#x20;         \| - Conected Services

&#x20;         \| - Dependencies

&#x20;         \| - Properties : JSON Configuration File. Details about app behaviour.

&#x20;         \| - Controllers : Controlls Web traffic. One for every endpoint or behaviour in our API.

&#x20;         \| - appsettings.json: Database connection string + static configuration.

&#x20;         \| - Program.cs : To configure Services + App.

&#x20;         \| - DataModel.cs
