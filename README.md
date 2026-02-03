# AGENT-PANEL-task
AGENT 
# 🎮 Agent Panel - Day 1 Complete Implementation

## 📋 Project Overview
Full-stack Agent Panel Management System with ASP.NET Core Web API backend and Angular frontend.

## 🛠️ Tech Stack

### Backend
- **Framework**: ASP.NET Core Web API (.NET 6/7/8)
- **Database**: SQL Server / Entity Framework Core
- **Authentication**: JWT (JSON Web Tokens)
- **Password Hashing**: BCrypt.Net
- **API Documentation**: Swagger/OpenAPI
- **Architecture**: Clean Architecture (Core, Infrastructure, API)

### Frontend
- **Framework**: Angular (v15+)
- **Styling**: Tailwind CSS
- **HTTP Client**: Angular HttpClient
- **Forms**: Reactive Forms
- **Routing**: Angular Router with Guards

---

## 📁 Project Structure

```
AgentPanel/
├── AgentPanel.API/                 # Web API Layer
│   ├── Controllers/
│   │   └── AuthController.cs      # Authentication endpoints
│   ├── Middleware/
│   │   └── ErrorHandlingMiddleware.cs
│   ├── Program.cs                 # Application entry point
│   └── appsettings.json           # Configuration
│
├── AgentPanel.Core/                # Domain Layer
│   ├── Entities/
│   │   ├── Agent.cs
│   │   ├── User.cs
│   │   ├── Commission.cs
│   │   └── Withdrawal.cs
│   ├── DTOs/
│   │   ├── LoginRequestDto.cs
│   │   ├── LoginResponseDto.cs
│   │   └── RegisterRequestDto.cs
│   └── Interfaces/
│       ├── IAuthService.cs
│       └── ITokenService.cs
│
├── AgentPanel.Infrastructure/      # Data Access Layer
│   ├── Data/
│   │   ├── ApplicationDbContext.cs
│   │   └── DbSeeder.cs            # Sample data seeder
│   └── Services/
│       ├── AuthService.cs
│       └── TokenService.cs
│
└── angular-frontend/               # Angular Application
    └── src/app/
        ├── components/
        │   └── login/
        ├── guards/
        │   └── auth.guard.ts
        ├── interceptors/
        │   └── auth.interceptor.ts
        └── services/
            └── auth.service.ts
```

---

## 🚀 BACKEND SETUP

### Prerequisites
- .NET 6/7/8 SDK
- SQL Server (LocalDB/Express/Full)
- Visual Studio 2022 / VS Code / Rider

### Step 1: Clone and Restore
```bash
# Navigate to project directory
cd AgentPanel

# Restore NuGet packages
dotnet restore
```

### Step 2: Update Database Connection String
Edit `AgentPanel.API/appsettings.json`:

```json
"ConnectionStrings": {
  "DefaultConnection": "Server=localhost;Database=AgentPanelDB;Trusted_Connection=True;TrustServerCertificate=True"
}
```

**For SQL Server Authentication:**
```json
"ConnectionStrings": {
  "DefaultConnection": "Server=localhost;Database=AgentPanelDB;User Id=sa;Password=YourPassword;TrustServerCertificate=True"
}
```

### Step 3: Create Database Migration
```bash
# Navigate to API project
cd AgentPanel.API

# Add initial migration
dotnet ef migrations add InitialCreate

# Update database
dotnet ef database update
```

### Step 4: Run Backend
```bash
# Run the API
dotnet run

# OR with watch mode (auto-reload)
dotnet watch run
```

The API will start at:
- **HTTPS**: `https://localhost:7001`
- **HTTP**: `http://localhost:5001`
- **Swagger UI**: `https://localhost:7001` (opens by default)

---

## 🚀 FRONTEND SETUP

### Prerequisites
- Node.js (v16+)
- Angular CLI (`npm install -g @angular/cli`)

### Step 1: Create Angular Project
```bash
# Create new Angular project
ng new angular-frontend --routing --style=css

cd angular-frontend
```

### Step 2: Install Tailwind CSS
```bash
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init
```

Edit `tailwind.config.js`:
```javascript
module.exports = {
  content: [
    "./src/**/*.{html,ts}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

Edit `src/styles.css`:
```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

### Step 3: Copy Project Files
Copy all the Angular files provided above into your project structure.

### Step 4: Update API URL
Edit `src/app/services/auth.service.ts`:
```typescript
private apiUrl = 'https://localhost:7001/api/auth'; // Update port if different
```

### Step 5: Run Frontend
```bash
# Start development server
ng serve

# OR on custom port
ng serve --port 4200
```

Frontend will be available at: `http://localhost:4200`

---

## 🗄️ DATABASE SCHEMA

### Tables Created
1. **Agents** - Agent account information
2. **Users** - Players managed by agents
3. **Commissions** - Commission records
4. **Withdrawals** - Withdrawal requests and history

### Sample Seed Data
The database is automatically seeded with:
- ✅ 2 Agent accounts
- ✅ 40 Users (25 for Agent 1, 15 for Agent 2)
- ✅ 14 Commission records (7 days each agent)
- ✅ 4 Withdrawal records

---

## 🔐 DEMO CREDENTIALS

### Test Agent Account
```
Email: agent@test.com
Password: password123
```

### Second Agent
```
Email: sarah.agent@test.com
Password: password123
```

---

## 🧪 TESTING THE API

### Using Swagger UI
1. Navigate to `https://localhost:7001`
2. Expand **Auth** endpoints
3. Try **POST /api/auth/login**
4. Use demo credentials
5. Copy the JWT token from response
6. Click **Authorize** button (🔓 icon)
7. Enter: `Bearer <your-token>`
8. Test protected endpoints

### Using Postman

#### 1. Login Request
```http
POST https://localhost:7001/api/auth/login
Content-Type: application/json

{
  "email": "agent@test.com",
  "password": "password123"
}
```

#### 2. Response
```json
{
  "success": true,
  "message": "Login successful",
  "data": {
    "agentId": 1,
    "fullName": "John Doe",
    "email": "agent@test.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "expiresAt": "2025-02-01T10:30:00Z"
  }
}
```

#### 3. Use Token in Headers
```http
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
```

---

## 📝 API ENDPOINTS (Day 1)

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| POST | `/api/auth/login` | Agent login | ❌ No |
| POST | `/api/auth/register` | Agent registration | ❌ No |
| POST | `/api/auth/forgot-password` | Password reset (dummy) | ❌ No |

---

## ✅ DAY 1 DELIVERABLES COMPLETED

- [x] Backend project structure (Clean Architecture)
- [x] Database models (Agent, User, Commission, Withdrawal)
- [x] Entity Framework Core setup
- [x] JWT authentication implementation
- [x] Password hashing with BCrypt
- [x] Auth API endpoints (Login, Register)
- [x] Database migrations
- [x] Seed data with 40+ records
- [x] Swagger documentation
- [x] Error handling middleware
- [x] Angular project setup
- [x] Login component with validation
- [x] Auth service
- [x] Auth guard
- [x] HTTP interceptor for JWT
- [x] Routing configuration
- [x] Tailwind CSS styling
- [x] Responsive login UI

---

## 🐛 Troubleshooting

### Backend Issues

**Issue**: Database connection fails
```bash
# Solution 1: Check SQL Server is running
# Solution 2: Update connection string
# Solution 3: Trust server certificate
TrustServerCertificate=True
```

**Issue**: Migration fails
```bash
# Delete Migrations folder and recreate
dotnet ef migrations add InitialCreate --force
dotnet ef database update
```

**Issue**: Port already in use
```bash
# Change port in Properties/launchSettings.json
"applicationUrl": "https://localhost:7002;http://localhost:5002"
```

### Frontend Issues

**Issue**: CORS error
```bash
# Backend already has CORS configured for http://localhost:4200
# Ensure Angular runs on port 4200
ng serve --port 4200
```

**Issue**: API connection refused
```bash
# Check backend is running
# Update API URL in auth.service.ts
# Verify SSL certificate is trusted
```

---

## 📚 Next Steps (Day 2)

Tomorrow we'll implement:
- Dashboard with statistics
- 7-day earnings chart
- User count, revenue, balance display
- Protected dashboard route
- Chart.js integration

---

## 📞 Support

If you encounter any issues:
1. Check the error logs in console
2. Verify all packages are installed
3. Ensure database is running
4. Check API and Frontend URLs match

---

## 📄 License
This is a technical assessment project.

---

**✅ Day 1 Status: COMPLETE** 🎉
**Next: Day 2 - Dashboard Implementation**
