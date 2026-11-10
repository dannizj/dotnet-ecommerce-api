# ApiEcommerce — ASP.NET Core Web API

RESTful API built with **.NET 9**, **ASP.NET Core**, **SQL Server**, **Entity Framework Core**, and **JWT authentication**.  
Includes product and category management, user registration/login, API versioning (v1/v2), Swagger documentation, response caching, and Docker support.

---

## 🚀 Features

- **ASP.NET Core Identity** + **JWT Bearer** authentication
- **API Versioning** (v1 and v2)
- **Swagger / OpenAPI** documentation with Bearer token support
- **Entity Framework Core** with SQL Server and migrations
- **Repository pattern** with interfaces and dependency injection
- **AutoMapper** for entity ↔ DTO mapping
- **Response Caching** and **CORS** configured
- **Product images** served from `wwwroot`
- **Docker Compose** ready

---

## 🛠️ Tech Stack

| Technology | Version | Purpose |
|------------|---------|---------|
| .NET | 9.0 | Framework |
| ASP.NET Core | 9.0 | Web API |
| C# | 12 | Language |
| SQL Server | — | Database |
| Entity Framework Core | 9.0 | ORM / Migrations |
| ASP.NET Core Identity | 9.0 | Users & roles |
| JWT Bearer | 9.0 | Authentication |
| AutoMapper | 16.2 | Object mapping |
| Swashbuckle (Swagger) | 10.2 | API docs |
| Asp.Versioning | 8.1 | API versioning |
| BCrypt.Net-Next | 4.2 | Password hashing |

---

## 📋 Requirements

- [.NET 9 SDK](https://dotnet.microsoft.com/download)
- SQL Server (LocalDB, Express, or Docker)
- Docker (optional, for containerized DB)

---

## 📦 Installation

```bash
# 1. Clone the repository
git clone https://github.com/dannizj/dotnet-ecommerce-api.git
cd dotnet-ecommerce-api

# 2. Restore dependencies
dotnet restore

# 3. Configure the database
# Edit appsettings.json and update the connection string:
# "ConexionSql": "Server=localhost;Database=ApiEcommerceNET9;User ID=SA;Password=YourPassword;TrustServerCertificate=true;..."

# 4. Apply migrations
dotnet ef database start
dotnet ef database update

# 5. Run the API
dotnet run
```

The API will be available at: `http://localhost:5000` or `https://localhost:5001`  
Swagger UI: `http://localhost:5000/swagger`

---

## ⚙️ Environment Variables

Create or edit `appsettings.json`:

```json
{
  "ApiSettings": {
    "SecretKey": "YOUR_LONG_RANDOM_SECRET_KEY_HERE"
  },
  "ConnectionStrings": {
    "ConexionSql": "Server=localhost;Database=ApiEcommerceNET9;User ID=SA;Password=YourPassword;TrustServerCertificate=true;MultipleActiveResultSets=true"
  }
}
```

> ⚠️ Never commit real secrets to GitHub. Use environment variables or User Secrets in production.

---

## 🔗 API Endpoints

### Authentication

| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | `/api/user/login` | Authenticate and get JWT token |
| `POST` | `/api/user/register` | Register a new user |

### Users (Protected)

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/api/user/profile/{id}` | Get user profile |
| `PUT` | `/api/user/update` | Update user data |

### Products (Protected)

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/api/product/items/{page}` | List products (paginated) |
| `GET` | `/api/product/item/{id}` | Get product by ID |
| `POST` | `/api/product/save` | Create a product |
| `PUT` | `/api/product/update/{id}` | Update a product |
| `DELETE` | `/api/product/delete/{id}` | Delete a product |
| `POST` | `/api/product/upload/{id}` | Upload product image |

### Categories (Public & Protected)

| Method | Endpoint | Version | Description |
|--------|----------|---------|-------------|
| `GET` | `/api/v1/categories` | v1 | List categories |
| `GET` | `/api/v2/categories` | v2 | List categories (v2) |

---

## 🔐 Authentication (JWT)

1. Call `POST /api/user/login` with email and password.
2. Receive a JWT token.
3. Include it in requests:

```
Authorization: Bearer <your-token>
```

---

## 📁 Project Structure

```
ApiEcommerce/
├── Controllers/
│   ├── V1/
│   │   └── CategoriesController.cs
│   ├── V2/
│   │   └── CategoriesController.cs
│   ├── ProductsController.cs
│   └── UserController.cs
├── Data/
│   ├── ApplicationDbContext.cs
│   └── DataSeeder.cs
├── Migrations/
├── Models/
│   ├── ApplicationUser.cs
│   ├── Category.cs
│   ├── Product.cs
│   └── Dtos/
├── Repository/
│   ├── IRepository/
│   │   ├── ICategoryRepository.cs
│   │   ├── IProductRepository.cs
│   │   └── IUserRepository.cs
│   ├── CategoryRepository.cs
│   ├── ProductRepository.cs
│   └── UserRepository.cs
├── Mapping/
│   ├── CategoryProfile.cs
│   ├── ProductProfile.cs
│   └── UserProfile.cs
├── Constants/
│   ├── CacheProfiles.cs
│   └── PolicyNames.cs
├── Views/
├── wwwroot/
├── Program.cs
├── appsettings.json
├── docker-compose.yaml
└── ApiEcommerce.csproj
```

---

## 🐳 Docker

```bash
docker-compose up -d
```

---

## 📄 License

MIT License.

---

## 👨‍💻 Author

**Danni ZJ**  
Backend Developer — .NET, SQL Server, ASP.NET Core, REST APIs

- GitHub: [@dannizj](https://github.com/dannizj)
- Repository: [dotnet-ecommerce-api](https://github.com/dannizj/dotnet-ecommerce-api)

---

## 📌 Version

**v1.0.0** — Initial release with JWT auth, API versioning, Swagger, and full CRUD.
