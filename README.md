# Private Closet — Keyboard Learning System

Native Android application (Kotlin + Jetpack Compose) connected to the Express/TypeScript & MySQL backend API.

## Repository Structure

```
├── android/          # Native Android Studio project (compile to APK)
├── backend/          # Node.js + Express + TypeScript + MySQL REST API
└── admin-dashboard/  # Web admin management dashboard
```

---

## 1. Deploy the Backend Server (`backend/`)

1. Import the MySQL database schema and seed data:
   - `backend/database/keyboard_learning.sql`
   - `backend/database/seed.sql`
2. Configure environment variables:
   ```bash
   cd backend
   cp .env.example .env
   # Edit .env with your DB_HOST, DB_USER, DB_PASSWORD, DB_NAME, JWT_SECRET, and PORT
   ```
3. Build and start the API server:
   ```bash
   npm install
   npm run build
   npm start
   ```
   Verify health endpoint: `GET https://your-server-domain.com/api/health`

*(See `backend/BACKEND_UPGRADE_GUIDE.md` for optional SQL migrations and routes for Marketplace, Community Chat, and Tutor Studio.)*

---

## 2. Connect & Compile the Android APK (`android/`)

The Android app is wired to the backend endpoints (`/api/health`, `/api/auth/register`, `/api/auth/login`, `/api/auth/me`, `/api/courses`, `/api/courses/:id/lessons`, `/api/lessons/:id`, `/api/lessons/:id/progress`, `/api/me/enrollments`, `/api/me/progress`).

1. Open `android/` in **Android Studio**.
2. In `android/app/build.gradle.kts`, update `BACKEND_BASE_URL` to your deployed server URL:
   ```kotlin
   buildConfigField("String", "BACKEND_BASE_URL", "\"https://your-server-domain.com/\"")
   ```
3. Build the APK via **Build → Build Bundle(s) / APK(s) → Build APK(s)** (or `./gradlew assembleDebug` / `assembleRelease`).
4. Install the APK on a phone. You can also inspect or change the backend server URL at runtime inside the app's **Backend API Connection** dialog.
