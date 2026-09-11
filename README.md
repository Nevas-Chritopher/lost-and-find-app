Campus Lost & Found (Mobile + API)
React Native mobile app with Node.js/Express API and MongoDB.

This project helps students and staff report lost/found items, search reports, chat, and recover items faster.

Tech Stack
Mobile: React Native (0.74.5)
Backend: Node.js + Express
Database: MongoDB
Auth: JWT
Core Features
Register/Login
Lost and found report creation (photo + location)
Search and filters
Item details + potential matches
Chat between users
Save/bookmark reports locally
Notification center (in-app)
Admin moderation and dashboard
Ownership verification token
Architecture Overview
Mobile UI layer: React Native screens and reusable components
State layer: AuthContext, ItemsContext, and ThemeContext
Service layer: API/device helpers in src/services
Backend API: Express controllers and routes
Data layer: MongoDB models
Flow: Screen Action -> Context/Service -> API Client -> Express Controller -> MongoDB -> Response -> UI Update

Mobile Computing Project Notes
This project is designed for mobile-first constraints: unstable networks, runtime permissions, and device-resource limits.
The app uses local persistence for draft/saved continuity and API synchronization for real-time updates.
UX flow prioritizes short actions, clear feedback, and safe recovery handoff behavior.
Prerequisites
Node.js 18+
npm
Android Studio + SDK
ADB (for physical phone install)
MongoDB Atlas (or local MongoDB)
Quick Start
1) Install dependencies
npm install --legacy-peer-deps
npm --prefix server install
2) Configure backend
cp server/.env.example server/.env
Edit server/.env:

MONGODB_URI
JWT_SECRET
Start backend:

npm run server:dev
Health check:

http://localhost:5000/api/health
Confirm authConfigured: true
3) Configure mobile API base URL
Edit src/config/env.js.

Default repo config already uses hosted mode:

DEV_BACKEND_MODE = 'hosted'
HOSTED_API_BASE_URL = 'https://mobile-app-ff7d.onrender.com/api'
Run the Mobile App
Recommended: standalone release mode (no Metro required)
npm run android
This runs Android in release mode and behaves like a real installed app.

Debug mode (Metro + hot reload)
npm start
# in another terminal
npm run android:dev
Physical phone debug via USB
# terminal 1
npm start
# terminal 2
npm run android:usb
If multiple devices are connected:

ANDROID_SERIAL=<device-id> npm run android:usb:device
Build and Install APK
npm run apk:debug
npm run apk:release
npm run install:phone:debug
npm run install:phone
APK output paths:

Debug: android/app/build/outputs/apk/debug/app-debug.apk
Release: android/app/build/outputs/apk/release/app-release.apk
Useful Scripts
npm run start - Start Metro
npm run start:reset - Start Metro with cache reset
npm run android - Run Android release build
npm run android:dev - Run Android debug build
npm run server:dev - Start backend in dev mode
npm run server:start - Start backend in normal mode
npm run dev:all - Start backend + Metro together
npm run apk:release - Build release APK
npm run install:phone - Install release APK to connected device
Troubleshooting
"Unable to load script" (red screen)
You are running a debug build without Metro.

Fix:

npm start
adb reverse tcp:8081 tcp:8081
Or install standalone release build:

npm run apk:release
npm run install:phone
adb: more than one device/emulator
ANDROID_SERIAL=<device-id> npm run android:usb:device
App cannot reach backend
Check server/.env values
Check backend health endpoint
Check src/config/env.js mode and URL
First account admin role
For demo/setup convenience, the first registered account becomes admin.

Project Structure
.
├── App.js
├── src/
│   ├── components/
│   ├── config/
│   ├── context/
│   ├── navigation/
│   ├── screens/
│   ├── services/
│   └── utils/
├── server/
│   ├── src/
│   └── .env.example
└── docs/
Documentation Index
Product Documentation
Screen Gallery
Deployment Guide
API Specification
MongoDB Schema
Feature Matrix
Test Plan
UML Text
Submission Checklist
Screenshot Assets Path
All documentation screenshots are stored in:

docs/doc_image/
All image paths:

docs/doc_image/account.jpg
docs/doc_image/alerts.jpg
docs/doc_image/darkmode_account.jpg
docs/doc_image/found-items-search.jpg
docs/doc_image/home_page.jpg
docs/doc_image/home_page1.jpg
docs/doc_image/login.jpg
docs/doc_image/lost-found-form.jpg
docs/doc_image/lost_form.jpg
docs/doc_image/report_item.jpg
Main Screenshot Preview
Home
The Home screen is the discovery hub. Users see recent lost/found reports, quick actions, and visual highlights for faster browsing.
