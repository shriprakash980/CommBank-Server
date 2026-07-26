# CommBank Server

A modern full-stack application for CommBank's Goal Tracker platform, enabling users to set, track, and manage financial goals with icon support.

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [Development](#development)
- [Testing](#testing)
- [API Documentation](#api-documentation)
- [Contributing](#contributing)
- [License](#license)

## 🎯 Overview

CommBank Server is the backend component of the Goal Tracker solution, a financial goal management system. This project provides RESTful APIs for managing user goals with support for icons, categories, progress tracking, and more.

The application is built with modern technologies and follows industry best practices for security, scalability, and maintainability.

## ✨ Features

- **Goal Management**: Create, read, update, and delete financial goals
- **Icon Support**: Assign custom icons to goals for better visual organization
- **Progress Tracking**: Monitor goal progress with real-time updates
- **User Authentication**: Secure user management and authentication
- **Data Persistence**: Reliable database storage with proper migrations
- **API-First Design**: RESTful API endpoints for seamless frontend integration
- **Unit Testing**: Comprehensive test coverage using xUnit
- **Code Quality**: Automated formatting and linting with Prettier

## 🛠️ Tech Stack

- **Runtime**: .NET Core / .NET 6+
- **Language**: C#
- **Framework**: ASP.NET Core
- **Database**: [SQL Server / Your DB]
- **ORM**: Entity Framework Core
- **Testing**: xUnit
- **API Design**: RESTful API
- **Code Formatting**: Prettier
- **Version Control**: Git

## 📁 Project Structure

```
CommBank-Server/
├── src/
│   ├── CommBank.API/              # API layer
│   │   ├── Controllers/           # API endpoints
│   │   ├── Models/                # API request/response models
│   │   └── Program.cs             # Application entry point
│   ├── CommBank.Core/             # Business logic
│   │   ├── Entities/              # Domain entities
│   │   ├── Services/              # Business services
│   │   └── Interfaces/            # Service contracts
│   ├── CommBank.Data/             # Data access layer
│   │   ├── Context/               # Database context
│   │   ├── Repositories/          # Repository pattern implementation
│   │   └── Migrations/            # Database migrations
│   └── CommBank.Shared/           # Shared utilities
│       ├── Constants/
│       ├── Enums/
│       └── Exceptions/
├── tests/
│   ├── CommBank.API.Tests/        # API layer tests
│   ├── CommBank.Core.Tests/       # Business logic tests
│   └── CommBank.Data.Tests/       # Data access tests
├── .gitignore
├── .prettierrc                     # Code formatting config
├── package.json                    # Node dependencies
├── package-lock.json
├── README.md
└── CommBank.sln                    # Visual Studio solution file
```

## 🚀 Getting Started

### Prerequisites

- **.NET 6.0 SDK or later** - [Download](https://dotnet.microsoft.com/download)
- **Visual Studio 2022** (recommended) or **VS Code** with C# extension
- **SQL Server** (LocalDB or full version)
- **Git**
- **Node.js** (for code formatting tools)

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/shriprakash980/CommBank-Server.git
   cd CommBank-Server
   ```

2. **Install dependencies**
   ```bash
   # Install .NET dependencies
   dotnet restore
   
   # Install Node dependencies for formatting tools
   npm install
   ```

3. **Configure the database**
   ```bash
   # Update connection string in appsettings.json
   # Then run migrations
   dotnet ef database update
   ```

4. **Build the solution**
   ```bash
   dotnet build
   ```

5. **Run the application**
   ```bash
   cd src/CommBank.API
   dotnet run
   ```

The API will be available at `https://localhost:5001`

## 💻 Development

### Running the Development Server

```bash
dotnet run --project src/CommBank.API
```

### Code Formatting

Maintain consistent code style with Prettier:

```bash
# Format all code files
npm run format

# Or using dotnet format
dotnet format
```

### Database Migrations

```bash
# Create a new migration
dotnet ef migrations add MigrationName -p src/CommBank.Data -s src/CommBank.API

# Apply migrations
dotnet ef database update -p src/CommBank.Data -s src/CommBank.API

# Revert last migration
dotnet ef database update PreviousMigrationName
```

## 🧪 Testing

### Run All Tests

```bash
dotnet test
```

### Run Specific Test Project

```bash
dotnet test tests/CommBank.Core.Tests
```

### Run Tests with Code Coverage

```bash
dotnet test /p:CollectCoverage=true /p:CoverageFormat=opencover
```

### Testing Guidelines

- Use **xUnit** for all unit tests
- Follow **Arrange-Act-Assert** pattern
- Aim for >80% code coverage
- Write descriptive test names
- Use mocking for external dependencies

Example test:

```csharp
[Fact]
public void CreateGoal_WithValidData_ReturnsSuccessResult()
{
    // Arrange
    var goalService = new GoalService(mockRepository);
    var goalDto = new CreateGoalDto { Title = "Save $1000", Icon = "piggy-bank" };
    
    // Act
    var result = goalService.CreateGoal(goalDto);
    
    // Assert
    Assert.NotNull(result);
    Assert.Equal("Save $1000", result.Title);
}
```

## 📚 API Documentation

### Base URL
```
https://localhost:5001/api
```

### Core Endpoints

#### Goals

- **GET** `/goals` - List all goals
- **GET** `/goals/{id}` - Get goal details
- **POST** `/goals` - Create a new goal
- **PUT** `/goals/{id}` - Update a goal
- **DELETE** `/goals/{id}` - Delete a goal
- **PATCH** `/goals/{id}/icon` - Update goal icon

### Example Request

```bash
curl -X POST https://localhost:5001/api/goals \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Save for Vacation",
    "description": "Save $5000 for summer vacation",
    "targetAmount": 5000,
    "currentAmount": 1200,
    "icon": "plane"
  }'
```

### Response Format

```json
{
  "id": "550e8400-e29b-41d4-a716-446655440000",
  "title": "Save for Vacation",
  "description": "Save $5000 for summer vacation",
  "targetAmount": 5000,
  "currentAmount": 1200,
  "icon": "plane",
  "createdAt": "2024-01-15T10:30:00Z",
  "updatedAt": "2024-01-15T10:30:00Z"
}
```

## 🔧 Configuration

### appsettings.json

```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Server=(localdb)\\mssqllocaldb;Database=CommBankDb;Trusted_Connection=true;"
  },
  "Logging": {
    "LogLevel": {
      "Default": "Information"
    }
  }
}
```

### Environment Variables

Create `.env` file in the root:

```bash
ASPNETCORE_ENVIRONMENT=Development
ConnectionString=your_connection_string
```

## 🔐 Security

- Use **Entity Framework Core** for SQL injection prevention
- Implement **JWT authentication** for API security
- Validate all user inputs
- Use **HTTPS** in production
- Keep dependencies updated: `dotnet outdated`

## 📦 Dependencies

Key NuGet packages:

```xml
<ItemGroup>
  <PackageReference Include="Microsoft.EntityFrameworkCore" Version="7.0.0" />
  <PackageReference Include="Microsoft.EntityFrameworkCore.SqlServer" Version="7.0.0" />
  <PackageReference Include="xunit" Version="2.4.2" />
  <PackageReference Include="Moq" Version="4.18.0" />
</ItemGroup>
```

## 🚢 Deployment

### Build for Production

```bash
dotnet publish -c Release -o ./publish
```

### Docker Deployment

```dockerfile
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /app
COPY . .
RUN dotnet publish -c Release -o out

FROM mcr.microsoft.com/dotnet/aspnet:6.0
WORKDIR /app
COPY --from=build /app/out .
ENTRYPOINT ["dotnet", "CommBank.API.dll"]
```

Build and run:

```bash
docker build -t commbank-server .
docker run -p 5001:5001 commbank-server
```

## 🤝 Contributing

1. **Fork the repository**
2. **Create a feature branch**: `git checkout -b feature/your-feature`
3. **Make your changes** and commit: `git commit -m 'Add your feature'`
4. **Format code**: `npm run format`
5. **Run tests**: `dotnet test`
6. **Push to branch**: `git push origin feature/your-feature`
7. **Create a Pull Request**

### Commit Message Guidelines

- Use clear, descriptive messages
- Start with action verb: `Add`, `Fix`, `Update`, `Remove`, `Refactor`
- Example: `Add icon support to Goal model`

## 📋 Code Style

- Follow **C# coding conventions**
- Use **PascalCase** for class/method names
- Use **camelCase** for local variables
- Use **UPPER_SNAKE_CASE** for constants
- Keep methods small and focused
- Add XML documentation comments

## 🐛 Troubleshooting

### Database Connection Issues
```bash
# Clear and recreate database
dotnet ef database drop
dotnet ef database update
```

### Build Errors
```bash
# Clean solution
dotnet clean
dotnet build
```

### Test Failures
```bash
# Run specific test with verbose output
dotnet test --logger:console --verbosity:detailed
```

## 📞 Support & Contact

- **Issues**: Use GitHub Issues for bug reports and feature requests
- **Discussions**: Start a GitHub Discussion for questions
- **Email**: [Your contact email]

## 📄 License

This project is licensed under the ISC License - see the LICENSE file for details.

## 🙏 Acknowledgments

- CommBank team for project guidance
- Tech Lead Tagg for mentorship
- All contributors and team members

---

**Happy coding! 🚀 Let's build something great together.**
