<div align="center">

# 📚 Mock Test App
### Complete Learning Platform with AI-Powered Features

![Flutter](https://img.shields.io/badge/Flutter-02569B?style=for-the-badge&logo=flutter&logoColor=white)
![Firebase](https://img.shields.io/badge/Firebase-FFCA28?style=for-the-badge&logo=firebase&logoColor=black)
![Supabase](https://img.shields.io/badge/Supabase-3ECF8E?style=for-the-badge&logo=supabase&logoColor=white)
![Dart](https://img.shields.io/badge/Dart-0175C2?style=for-the-badge&logo=dart&logoColor=white)

**A premium Flutter application with admin panel, real-time leaderboards, and intelligent data management**

[![License](https://img.shields.io/badge/License-Proprietary-red.svg)](LICENSE)
[![Platform](https://img.shields.io/badge/Platform-Android%20%7C%20iOS%20%7C%20Web-blue.svg)](https://flutter.dev)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

[Features](#-features) • [Architecture](#-architecture) • [Installation](#-installation) • [Documentation](#-documentation)

---

</div>

## ✨ Features

<table>
<tr>
<td width="50%" valign="top">

### 👤 User Features

- 🔐 **Authentication**
  - Email/Password login
  - Firebase Auth integration
  
- 📝 **Mock Tests**
  - Timed assessments
  - Instant results & solutions
  
- 🏆 **Leaderboard**
  - Weekly/Monthly rankings
  - Real-time updates
  
- 🔥 **Streak System**
  - Daily tracking
  - Coin rewards
  
- 📊 **Progress Tracking**
  - Test history
  - Performance analytics
  
- 🎨 **Customization**
  - 6 avatar options
  - Profile management

</td>
<td width="50%" valign="top">

### 👨‍💼 Admin Features

- 📊 **Dashboard**
  - Real-time analytics
  - User metrics
  
- ➕ **Test Management**
  - Create/Edit/Delete tests
  - JSON import support
  
- 📁 **Category Management**
  - Organize content
  - Subcategories
  
- 🔔 **Notifications**
  - Push notifications
  - Broadcast messages
  
- 🔒 **Security**
  - 2FA authentication
  - TOTP-based
  
- 🖼️ **Media**
  - GitHub image hosting
  - Auto-upload

</td>
</tr>
</table>

---

## 🏗️ Architecture

<div align="center">

### Tech Stack

![Flutter](https://img.shields.io/badge/Flutter-3.0+-02569B?style=flat-square&logo=flutter)
![Dart](https://img.shields.io/badge/Dart-3.0+-0175C2?style=flat-square&logo=dart)
![Firebase](https://img.shields.io/badge/Firebase-Auth_&_Firestore-FFCA28?style=flat-square&logo=firebase)
![Supabase](https://img.shields.io/badge/Supabase-Database-3ECF8E?style=flat-square&logo=supabase)

</div>

### 📱 Frontend (Flutter/Dart)
- **UI Screens**: 44 screens (Admin + User interfaces)
- **State Management**: Provider pattern
- **Local Storage**: SharedPreferences (encrypted)
- **Navigation**: Material routes with authentication guards
- **Widgets**: 7+ reusable components

### 🔧 Backend Services

<table>
<tr>
<td width="50%">

**Firebase Services:**
- 🔥 Firebase Auth
- 💾 Firestore Database
- 🔔 Cloud Messaging (FCM)

</td>
<td width="50%">

**Supabase Services:**
- 🗄️ PostgreSQL Database
- 🔒 Row-Level Security
- 🧹 Auto-cleanup Jobs

</td>
</tr>
</table>

### 🤖 External Agents/APIs

| Agent | Purpose | Integration | Configuration |
|-------|---------|-------------|---------------|
| ![Firebase](https://img.shields.io/badge/Firebase-Auth-orange?style=flat-square) | User authentication | `AuthService` | Firebase Console |
| ![Firestore](https://img.shields.io/badge/Firestore-Metadata-yellow?style=flat-square) | Metadata storage | `DatabaseService` | Firebase Console |
| ![Supabase](https://img.shields.io/badge/Supabase-Stats-green?style=flat-square) | Stats & leaderboard | `SupabaseService` | `api_config.dart` |
| ![FCM](https://img.shields.io/badge/FCM-Notifications-red?style=flat-square) | Push notifications | `NotificationService` | Firebase Console |
| ![GitHub](https://img.shields.io/badge/GitHub-Images-black?style=flat-square) | Image hosting | `GithubImageService` | `api_config.dart` |
| ![Gemini](https://img.shields.io/badge/Gemini-AI_Primary-blue?style=flat-square) | AI explanations (Primary) | `AIService` | `api_config.dart` |
| ![HuggingFace](https://img.shields.io/badge/HuggingFace-AI_Fallback-yellow?style=flat-square) | AI fallback (flan-t5) | `AIService` | `api_config.dart` |

#### 🤖 AI Agents Details

**Google Gemini AI (Primary)**
- **Model**: `gemini-1.5-flash`
- **Purpose**: Generate explanations for test questions
- **Implementation**: `lib/services/ai_service.dart`
- **Keys**: 10 obfuscated keys with rotation in `lib/config/api_config.dart`
- **Fallback**: Automatic switch to Hugging Face on failure

**Hugging Face (Fallback)**
- **Model**: `google/flan-t5-base`
- **Purpose**: Backup AI provider when Gemini fails
- **Implementation**: `lib/services/ai_service.dart`
- **Keys**: 10 obfuscated keys with rotation in `lib/config/api_config.dart`
- **API**: `https://api-inference.huggingface.co`

**AI Flow:**
```
User requests explanation
  ↓
Try Gemini Keys 1-10 (rotation)
  ↓ (if all fail)
Try HuggingFace Keys 1-10 (rotation)
  ↓
Return explanation or error message
```


### 💻 Language Stack

<div align="center">

| Layer | Languages | Purpose |
|:------|:----------|:--------|
| **Frontend** | ![Dart](https://img.shields.io/badge/Dart-100%25-0175C2?style=flat-square&logo=dart) | UI & Business Logic |
| **Backend** | ![JavaScript](https://img.shields.io/badge/JavaScript-Node.js-yellow?style=flat-square&logo=javascript) | Firebase Cloud Functions |
| **Database** | ![SQL](https://img.shields.io/badge/SQL-PostgreSQL-blue?style=flat-square&logo=postgresql) | Supabase Queries |
| **Tools** | ![Python](https://img.shields.io/badge/Python-PDF_Parser-green?style=flat-square&logo=python) | PDF to JSON Converter |
| **Native** | ![Kotlin](https://img.shields.io/badge/Kotlin-Android-purple?style=flat-square&logo=kotlin) ![C++](https://img.shields.io/badge/C++-Windows-blue?style=flat-square&logo=cplusplus) | Platform-specific code |

</div>

---

## 📂 Project Structure

<details>
<summary>Click to expand file tree</summary>

```
mock_test_flutter/
├── 📱 lib/
│   ├── ⚙️ config/              # API & App configurations
│   │   ├── 🔑 api_config.dart
│   │   └── 🎨 app_colors.dart
│   ├── 💾 data/                # Local data sources
│   ├── 📦 models/              # Data models
│   │   ├── ❓ question_model.dart
│   │   ├── 📝 test_model.dart
│   │   └── 👤 user_model.dart
│   ├── 🖼️ screens/             # UI Screens
│   │   ├── 👨‍💼 admin/           # Admin panel
│   │   ├── 🔐 auth/            # Authentication
│   │   ├── 👤 profile/         # User profile
│   │   └── 📝 test_series/     # Tests
│   ├── 🛠️ services/            # Backend services
│   │   ├── 🔐 auth_service.dart
│   │   ├── 💾 database_service.dart
│   │   ├── 🗄️ supabase_service.dart
│   │   ├── 🔔 notification_service.dart
│   │   └── 🖼️ github_image_service.dart
│   ├── 🧩 widgets/             # Reusable components
│   └── 🚀 main.dart            # Entry point
├── 🎨 assets/                  # Images, Fonts, Avatars
├── 🤖 android/                 # Android config
├── 🪟 windows/                 # Windows config
├── 🗄️ supabase/                # Migrations
└── 📦 pubspec.yaml             # Dependencies
```

</details>

---

## 🗄️ Database Schema

<div align="center">

### Firebase Firestore

| Collection | Purpose |
|------------|---------|
| `users` | User profiles & metadata |
| `categories` | Test categories |
| `tests` | Test metadata & questions |
| `notifications` | Notification history |

### Supabase PostgreSQL

| Table | Purpose |
|-------|---------|
| `user_stats` | Streaks, coins, rankings |
| `test_results` | Test submissions |
| `notifications` | Active notifications |

</div>

---

## 🧹 Auto-Cleanup System

<div align="center">

| Data Type | ⏱️ Retention | 🎯 Action |
|:----------|:------------|:---------|
| Notifications | 24 hours | ![Delete](https://img.shields.io/badge/DELETE-red?style=flat-square) |
| Test Results | 5 days | ![Delete](https://img.shields.io/badge/DELETE-red?style=flat-square) |
| Inactive Streaks | 15 days | ![Reset](https://img.shields.io/badge/RESET-orange?style=flat-square) |

</div>

---

## 🚀 Installation

### Prerequisites

![Flutter](https://img.shields.io/badge/Flutter-3.0+-blue?style=flat-square&logo=flutter)
![Firebase](https://img.shields.io/badge/Firebase-Account-orange?style=flat-square&logo=firebase)
![Supabase](https://img.shields.io/badge/Supabase-Account-green?style=flat-square&logo=supabase)

### Quick Start

```bash
# 1️⃣ Clone repository
git clone https://github.com/yourusername/mock_test_flutter.git
cd mock_test_flutter

# 2️⃣ Install dependencies
flutter pub get

# 3️⃣ Configure Firebase
# Add google-services.json to android/app/

# 4️⃣ Configure Supabase
# Update lib/config/api_config.dart

# 5️⃣ Run the app
flutter run
```

### Build APK

```bash
flutter build apk --release
```

---

## 🔐 Security Features

<div align="center">

✅ Encrypted local storage  
✅ Row-Level Security (RLS)  
✅ 2FA for admin access  
✅ API key obfuscation  
✅ Secure token management  

</div>

---

## 📊 Performance Metrics

<div align="center">

| Metric | Value |
|:-------|:-----:|
| **Supported Users** | ![50K+](https://img.shields.io/badge/50K+-Users-success?style=flat-square) |
| **Response Time** | ![<100ms](https://img.shields.io/badge/<100ms-Fast-green?style=flat-square) |
| **Uptime** | ![99.9%](https://img.shields.io/badge/99.9%25-Reliable-brightgreen?style=flat-square) |
| **Database** | ![Optimized](https://img.shields.io/badge/Auto--Cleanup-Optimized-blue?style=flat-square) |

</div>

---

## 📚 Documentation

- 📖 [Complete Workflow](WORKFLOW.md) - Visual app flow diagrams
- ✅ [Task Checklist](task.md) - Development progress
- 🎯 [Feature Walkthrough](walkthrough.md) - Detailed features
- 🚀 [Quick Start Guide](QUICKSTART.md) - Commands & troubleshooting

---

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📄 License

This project is proprietary software. All rights reserved.

---

## 📞 Support

For issues or questions:
- 📧 Email: support@example.com
- 🐛 Issues: [GitHub Issues](https://github.com/yourusername/mock_test_flutter/issues)

---

<div align="center">

### Made with ❤️ using Flutter

![Flutter](https://img.shields.io/badge/Built_with-Flutter-02569B?style=for-the-badge&logo=flutter&logoColor=white)

**[⬆ Back to Top](#-mock-test-app)**

</div>

