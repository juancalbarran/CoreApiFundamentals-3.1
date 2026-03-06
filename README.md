# CoreApiFundamentals

A RESTful API built with **ASP.NET Core 3.1** that manages code camps, talks, and speakers. This project demonstrates core Web API concepts including routing, versioning, data access with Entity Framework Core, and object mapping with AutoMapper.

## Features

- CRUD operations for **Camps**, **Talks**, and **Speakers**
- API versioning (v1.0 and v1.1)
- Entity Framework Core with SQL Server
- AutoMapper for model/entity mapping
- Nested resource routing (talks scoped under camps)

## Prerequisites

- [.NET Core SDK 3.1](https://dotnet.microsoft.com/download/dotnet/3.1)
- SQL Server or SQL Server LocalDB

## Getting Started

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd CoreApiFundamentals-3.1
   ```

2. **Configure the database connection**

   Update the connection string in `src/appsettings.json`:
   ```json
   "ConnectionStrings": {
     "CodeCamp": "Data Source=<your-server>;Initial Catalog=PSCodeCamp;Integrated Security=True;"
   }
   ```

3. **Apply migrations**
   ```bash
   cd src
   dotnet ef database update
   ```

4. **Run the application**
   ```bash
   dotnet run --project src/CoreCodeCamp.csproj
   ```

## API Endpoints

### Camps

| Method | Route | Description |
|--------|-------|-------------|
| GET | `/api/camps` | Get all camps |
| GET | `/api/camps/{moniker}` | Get a camp by moniker |
| GET | `/api/camps/search?theDate=<date>` | Search camps by event date |
| POST | `/api/camps` | Create a new camp |
| PUT | `/api/camps/{moniker}` | Update a camp |
| DELETE | `/api/camps/{moniker}` | Delete a camp |

### Talks

| Method | Route | Description |
|--------|-------|-------------|
| GET | `/api/camps/{moniker}/talks` | Get all talks for a camp |
| GET | `/api/camps/{moniker}/talks/{id}` | Get a specific talk |
| POST | `/api/camps/{moniker}/talks` | Create a talk |
| PUT | `/api/camps/{moniker}/talks/{id}` | Update a talk |
| DELETE | `/api/camps/{moniker}/talks/{id}` | Delete a talk |

## API Versioning

The API supports versioning via the `api-version` query parameter or request header. The default version is **1.1**.

Example:
```
GET /api/camps/ATL2018?api-version=1.0
GET /api/camps/ATL2018?api-version=1.1
```

## Project Structure

```
src/
├── Controllers/        # API controllers
│   ├── CampsController.cs
│   ├── TalksController.cs
│   └── Camps2Controller.cs
├── Data/               # Data access layer
│   ├── Entities/       # EF Core entity models
│   ├── Migrations/     # EF Core migrations
│   ├── CampContext.cs
│   └── CampRepository.cs
├── Models/             # DTOs / API models
├── Startup.cs
└── Program.cs
```

## Technologies

- ASP.NET Core 3.1
- Entity Framework Core 3.1 (SQL Server)
- AutoMapper 8.x
- Microsoft.AspNetCore.Mvc.Versioning 5.x
