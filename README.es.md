# ApiEcommerce — API REST con ASP.NET Core

API RESTful construida con **.NET 9**, **ASP.NET Core**, **SQL Server**, **Entity Framework Core** y **autenticación JWT**.  
Incluye gestión de productos y categorías, registro/login de usuarios, versionado de API (v1/v2), documentación Swagger, caché de respuestas y soporte para Docker.

---

## 🚀 Características

- **ASP.NET Core Identity** + **JWT Bearer** para autenticación
- **API Versioning** (v1 y v2)
- **Swagger / OpenAPI** con soporte para token Bearer
- **Entity Framework Core** con SQL Server y migraciones
- **Patrón Repository** con interfaces e inyección de dependencias
- **AutoMapper** para mapeo de entidad ↔ DTO
- **Response Caching** y **CORS** configurados
- **Imágenes de productos** servidas desde `wwwroot`
- **Docker Compose** listo

---

## 🛠️ Stack Tecnológico

| Tecnología | Versión | Uso |
|------------|---------|-----|
| .NET | 9.0 | Framework |
| ASP.NET Core | 9.0 | Web API |
| C# | 12 | Lenguaje |
| SQL Server | — | Base de datos |
| Entity Framework Core | 9.0 | ORM / Migraciones |
| ASP.NET Core Identity | 9.0 | Usuarios y roles |
| JWT Bearer | 9.0 | Autenticación |
| AutoMapper | 16.2 | Mapeo de objetos |
| Swashbuckle (Swagger) | 10.2 | Documentación API |
| Asp.Versioning | 8.1 | Versionado de API |
| BCrypt.Net-Next | 4.2 | Hash de contraseñas |

---

## 📋 Requisitos Previos

- [.NET 9 SDK](https://dotnet.microsoft.com/download)
- SQL Server (LocalDB, Express o Docker)
- Docker (opcional, para base de datos en contenedor)

---

## 📦 Instalación

```bash
# 1. Clonar el repositorio
git clone https://github.com/dannizj/dotnet-ecommerce-api.git
cd dotnet-ecommerce-api

# 2. Restaurar dependencias
dotnet restore

# 3. Configurar la base de datos
# Editar appsettings.json y actualizar la cadena de conexión:
# "ConexionSql": "Server=localhost;Database=ApiEcommerceNET9;User ID=SA;Password=TuPassword;TrustServerCertificate=true;..."

# 4. Aplicar migraciones
dotnet ef database start
dotnet ef database update

# 5. Ejecutar la API
dotnet run
```

La API estará disponible en: `http://localhost:5000` o `https://localhost:5001`  
Swagger UI: `http://localhost:5000/swagger`

---

## ⚙️ Variables de Entorno

Crear o editar `appsettings.json`:

```json
{
  "ApiSettings": {
    "SecretKey": "TU_CLAVE_SECRETA_LARGA_Y_ALEATORIA_AQUI"
  },
  "ConnectionStrings": {
    "ConexionSql": "Server=localhost;Database=ApiEcommerceNET9;User ID=SA;Password=TuPassword;TrustServerCertificate=true;MultipleActiveResultSets=true"
  }
}
```

> ⚠️ Nunca subas secretos reales a GitHub. Usa variables de entorno o User Secrets en producción.

---

## 🔗 Endpoints de la API

### Autenticación

| Método | Endpoint | Descripción |
|--------|----------|-------------|
| `POST` | `/api/user/login` | Autenticar y obtener token JWT |
| `POST` | `/api/user/register` | Registrar un nuevo usuario |

### Usuarios (Protegidos)

| Método | Endpoint | Descripción |
|--------|----------|-------------|
| `GET` | `/api/user/profile/{id}` | Obtener perfil de usuario |
| `PUT` | `/api/user/update` | Actualizar datos de usuario |

### Productos (Protegidos)

| Método | Endpoint | Descripción |
|--------|----------|-------------|
| `GET` | `/api/product/items/{page}` | Listar productos (paginado) |
| `GET` | `/api/product/item/{id}` | Obtener producto por ID |
| `POST` | `/api/product/save` | Crear un producto |
| `PUT` | `/api/product/update/{id}` | Actualizar un producto |
| `DELETE` | `/api/product/delete/{id}` | Eliminar un producto |
| `POST` | `/api/product/upload/{id}` | Subir imagen de producto |

### Categorías (Públicas y Protegidas)

| Método | Endpoint | Versión | Descripción |
|--------|----------|---------|-------------|
| `GET` | `/api/v1/categories` | v1 | Listar categorías |
| `GET` | `/api/v2/categories` | v2 | Listar categorías (v2) |

---

## 🔐 Autenticación (JWT)

1. Llama a `POST /api/user/login` con email y contraseña.
2. Recibirás un token JWT.
3. Inclúyelo en las solicitudes:

```
Authorization: Bearer <tu-token>
```

---

## 📁 Estructura del Proyecto

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

## 📄 Licencia

Licencia MIT.

---

## 👨‍💻 Autor

**Danni ZJ**  
Backend Developer — .NET, SQL Server, ASP.NET Core, APIs REST

- GitHub: [@dannizj](https://github.com/dannizj)
- Repositorio: [dotnet-ecommerce-api](https://github.com/dannizj/dotnet-ecommerce-api)

---

## 📌 Versión

**v1.0.0** — Lanzamiento inicial con autenticación JWT, versionado de API, Swagger y CRUD completo.
