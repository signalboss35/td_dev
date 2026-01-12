# Team Management System

เว็บแอปพลิเคชันสำหรับจัดการทีม Developer ด้วย Agile/Scrum methodology ที่สร้างด้วย Next.js, TypeScript, PostgreSQL และ DBeaver

## 🚀 Features

- ✅ Authentication System (Login/Logout)
- ✅ Dashboard with Statistics
- ✅ User Profile Management
- ✅ Telegram Hub Integration
- ✅ Knowledge Management (KM) Website
- ✅ Google Drive Integration
- ✅ External Platforms (TW30, TWP, Data Service)
- ✅ Apple-inspired Clean & Minimal Design
- ✅ Responsive Tailwind CSS
- ✅ Protected Routes with Middleware
- ✅ ESLint Configuration

## 📋 Prerequisites

- Node.js 18+ 
- PostgreSQL 15+
- DBeaver Community (for database management)
- macOS (instructions optimized for Mac)

## 🛠️ Installation Steps

### 1. Install Dependencies (MacOS)

```bash
# Install Homebrew (if not installed)
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Install Node.js and PostgreSQL
brew install node
brew install postgresql@15

# Start PostgreSQL service
brew services start postgresql@15

# Install DBeaver
brew install --cask dbeaver-community
```

### 2. Create Next.js Project

```bash
# Create project
npx create-next-app@latest team-management --typescript --eslint --tailwind --app --src-dir --import-alias "@/*"

cd team-management

# Install dependencies
npm install pg bcryptjs jsonwebtoken
npm install -D @types/pg @types/bcryptjs @types/jsonwebtoken
```

### 3. Setup Database with DBeaver

1. เปิด DBeaver
2. คลิก "New Database Connection" (ไอคอน ⚡)
3. เลือก "PostgreSQL"
4. กรอกข้อมูล:
   - Host: localhost
   - Port: 5432
   - Database: postgres
   - Username: postgres
   - Password: your_password
5. คลิก "Test Connection" แล้วคลิก "Finish"
6. Right-click connection > Create > Database
7. ตั้งชื่อ: `team_management`
8. เปิด SQL Editor และรัน SQL script จาก `database/schema.sql`

### 4. Create Admin User

```bash
# สร้าง folder scripts
mkdir scripts

# Run script to generate admin password hash
node scripts/create-admin.js

# Copy SQL output และรันใน DBeaver
```

### 5. Environment Variables

สร้างไฟล์ `.env.local`:

```env
DB_HOST=localhost
DB_PORT=5432
DB_NAME=team_management
DB_USER=postgres
DB_PASSWORD=your_password_here
JWT_SECRET=your-super-secret-jwt-key-change-this
NEXT_PUBLIC_API_URL=http://localhost:3000
```

### 6. Run Development Server

```bash
npm run dev
```

เปิดเบราว์เซอร์ไปที่: http://localhost:3000

## 🔐 Default Login Credentials

- **Username:** admin
- **Password:** P51fa@b5

## 📁 Project Structure

```
team-management/
├── src/
│   ├── app/
│   │   ├── api/
│   │   │   ├── auth/
│   │   │   │   ├── login/route.ts
│   │   │   │   └── logout/route.ts
│   │   │   ├── dashboard/route.ts
│   │   │   └── profile/route.ts
│   │   ├── dashboard/page.tsx
│   │   ├── profile/page.tsx
│   │   ├── telegram/page.tsx
│   │   ├── km/page.tsx
│   │   ├── drive/page.tsx
│   │   ├── platforms/page.tsx
│   │   ├── login/page.tsx
│   │   └── page.tsx
│   ├── components/
│   │   └── Sidebar.tsx
│   ├── lib/
│   │   ├── db.ts
│   │   └── auth.ts
│   └── middleware.ts
├── scripts/
│   └── create-admin.js
├── .env.local
├── .eslintrc.json
├── package.json
├── tailwind.config.ts
└── tsconfig.json
```

## 🎨 Design Philosophy

ออกแบบตาม Apple's Design Principles:

- **Clean & Minimal** - เน้นความเรียบง่าย ไม่ซับซ้อน
- **Typography** - ใช้ฟอนต์ที่อ่านง่าย มีลำดับชั้นชัดเจน
- **Whitespace** - ใช้ระยะห่างที่เหมาะสม ไม่แน่นเกินไป
- **Rounded Corners** - มุมโค้งมน ดูทันสมัย
- **Subtle Shadows** - เงาเบา ๆ เพิ่มความลึก
- **Consistent Colors** - ใช้สี slate scale เป็นหลัก

## 🔒 Security Features

- JWT Token Authentication
- HTTP-only Cookies
- Password Hashing (bcrypt)
- Protected Routes (Middleware)
- Logout clears session completely
- No back navigation after logout

## 📊 Database Schema

### Users Table
- id, username, password, name, surname
- position, tel, email, line, role
- created_at, updated_at

### Projects Table
- id, name, description, status
- start_date, end_date, created_by
- created_at, updated_at

### Tasks Table
- id, project_id, title, description
- status (todo/doing/done), assigned_to, priority
- created_at, updated_at

### Sprints Table
- id, project_id, name
- start_date, end_date, goal, status
- created_at

## 🚦 Available Scripts

```bash
npm run dev          # Start development server
npm run build        # Build for production
npm run start        # Start production server
npm run lint         # Run ESLint
npm run type-check   # TypeScript type checking
```

## 🔧 Troubleshooting

### PostgreSQL Connection Issues
```bash
# Check if PostgreSQL is running
brew services list

# Restart PostgreSQL
brew services restart postgresql@15

# Check PostgreSQL logs
tail -f /usr/local/var/log/postgresql@15.log
```

### Port Already in Use
```bash
# Find and kill process on port 3000
lsof -ti:3000 | xargs kill -9
```

## 📝 ESLint Rules

Project follows Next.js + TypeScript best practices:
- No unused variables (warnings)
- Strict type checking
- Console statements allowed (warn/error only)
- React hooks rules enforced

## 🌐 External Integrations

1. **KM Website**: https://km-td.hii.or.th/km_dev/
2. **Google Drive**: Shared folder access
3. **Platform TW30**: ThaiWater 3.0 Backoffice
4. **ThaiWater Platform**: Main portal
5. **Data Service**: HII Data Service

## 📱 Responsive Design

- ✅ Desktop (1920px+)
- ✅ Laptop (1280px)
- ✅ Tablet (768px)
- ✅ Mobile (375px)

## 🎯 Future Enhancements

- [ ] Real-time Telegram notifications
- [ ] Kanban board for tasks
- [ ] Sprint planning tools
- [ ] Team calendar
- [ ] File upload system
- [ ] Dark mode support

## 👥 Support

For issues or questions, please contact the development team.

## 📄 License

Private - Internal Use Only

---

Built with ❤️ using Next.js 15, TypeScript, PostgreSQL & Tailwind CSS