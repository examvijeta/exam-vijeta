# 🔄 App Workflow - Visual Flow Diagrams

Complete visual workflow showing how the app works from user signup to admin management.

---

## 📱 Complete User Journey Flow

```mermaid
graph TB
    Start([User Opens App]) --> Auth{Authenticated?}
    
    Auth -->|No| LoginScreen[🔐 Login/Signup Screen]
    Auth -->|Yes| HomeScreen[🏠 Home Screen]
    
    LoginScreen --> FireAuth[🔥 Firebase Auth]
    FireAuth --> CreateUser[Create User]
    CreateUser --> SaveFirestore[(💾 Firestore<br/>users collection)]
    CreateUser --> SaveSupabase[(🗄️ Supabase<br/>user_stats table)]
    SaveFirestore --> HomeScreen
    SaveSupabase --> HomeScreen
    
    HomeScreen --> UserActions{User Action}
    
    UserActions -->|Take Test| TestFlow[📝 Test Flow]
    UserActions -->|View Leaderboard| LeaderboardFlow[🏆 Leaderboard]
    UserActions -->|Claim Streak| StreakFlow[🔥 Streak System]
    UserActions -->|Edit Profile| ProfileFlow[👤 Profile]
    UserActions -->|View News| NewsFlow[📰 Current Affairs]
    
    TestFlow --> BrowseTests[Browse Test Categories]
    BrowseTests --> LoadTests[(💾 Firestore<br/>tests collection)]
    LoadTests --> SelectTest[Select Test]
    SelectTest --> QuizScreen[📝 Quiz Screen<br/>Timer Started]
    QuizScreen --> SubmitAnswers[Submit Answers]
    SubmitAnswers --> CalculateScore[Calculate Score]
    CalculateScore --> SaveResults[(🗄️ Supabase<br/>test_results)]
    SaveResults --> UpdateStats[(🗄️ Update user_stats)]
    UpdateStats --> ShowResults[📊 Results Screen]
    ShowResults --> HomeScreen
    
    LeaderboardFlow --> FetchRankings[(🗄️ Supabase<br/>Query Rankings)]
    FetchRankings --> DisplayLeaderboard[📊 Display Rankings]
    DisplayLeaderboard --> HomeScreen
    
    StreakFlow --> CheckStreak{Streak Valid?}
    CheckStreak -->|Yes| AddCoins[💰 Add Coins]
    CheckStreak -->|No| ResetStreak[❌ Reset to 0]
    AddCoins --> UpdateSupabase[(🗄️ Update Supabase)]
    ResetStreak --> UpdateSupabase
    UpdateSupabase --> ShowPopup[🎉 Reward Popup]
    ShowPopup --> HomeScreen
    
    ProfileFlow --> EditProfile[✏️ Edit Profile Screen]
    EditProfile --> UpdateProfile[(💾 Update Firestore<br/>& Supabase)]
    UpdateProfile --> HomeScreen
    
    NewsFlow --> FetchNews[📡 Fetch RSS Feed]
    FetchNews --> DisplayNews[📰 News List]
    DisplayNews --> HomeScreen
```

---

## 👨‍💼 Admin Flow with 2FA

```mermaid
graph TB
    AdminStart([Admin Opens App]) --> AdminLogin[🔐 Admin Login]
    AdminLogin --> CheckAuth{Authenticated?}
    
    CheckAuth -->|No| LoginFailed[❌ Access Denied]
    CheckAuth -->|Yes| CheckRole{Check Role}
    
    CheckRole -->|User| AccessDenied[❌ Not Admin]
    CheckRole -->|Admin/Owner| Check2FA{2FA Enabled?}
    
    Check2FA -->|No| Dashboard[📊 Admin Dashboard]
    Check2FA -->|Yes| TOTPScreen[🔒 Enter TOTP Code]
    
    TOTPScreen --> VerifyCode{Valid Code?}
    VerifyCode -->|No| TOTPScreen
    VerifyCode -->|Yes| Dashboard
    
    Dashboard --> AdminActions{Admin Action}
    
    AdminActions -->|Manage Tests| TestMgmt[📝 Test Management]
    AdminActions -->|Categories| CatMgmt[📁 Categories]
    AdminActions -->|Notifications| NotifMgmt[🔔 Notifications]
    AdminActions -->|Analytics| Analytics[📊 Analytics]
    AdminActions -->|Users| UserMgmt[👥 User Management]
    
    TestMgmt --> AddEditTest[➕ Add/Edit Test]
    AddEditTest --> UploadJSON[📄 Upload JSON]
    UploadJSON --> ProcessQuestions[Process Questions]
    ProcessQuestions --> UploadImages{Has Images?}
    UploadImages -->|Yes| GitHubUpload[🖼️ GitHub Upload]
    UploadImages -->|No| SaveTest
    GitHubUpload --> GetImageURL[Get Image URL]
    GetImageURL --> SaveTest[(💾 Save to Firestore)]
    SaveTest --> Dashboard
    
    CatMgmt --> ManageCategories[Add/Edit Categories]
    ManageCategories --> SaveCategories[(💾 Firestore<br/>categories)]
    SaveCategories --> Dashboard
    
    NotifMgmt --> ComposeNotif[✏️ Compose Message]
    ComposeNotif --> SendFCM[📡 Send via FCM]
    SendFCM --> SaveNotifDB[(🗄️ Supabase<br/>notifications)]
    SaveNotifDB --> TriggerCleanup[🧹 Trigger Cleanup]
    TriggerCleanup --> CleanOldData[Clean 24h+ Data]
    CleanOldData --> Dashboard
    
    Analytics --> FetchMetrics[(📊 Fetch Data<br/>Firestore + Supabase)]
    FetchMetrics --> DisplayCharts[📈 Display Charts]
    DisplayCharts --> Dashboard
    
    UserMgmt --> ViewUsers[(💾 Fetch Users<br/>Firestore)]
    ViewUsers --> ManageUsers[View/Edit Users]
    ManageUsers --> Dashboard
```

---

## 🗄️ Database Architecture & Connections

```mermaid
graph LR
    subgraph Firebase["🔥 Firebase Ecosystem"]
        FireAuth[Firebase Auth]
        Firestore[(Firestore Database)]
        FCM[Cloud Messaging]
    end
    
    subgraph Supabase["🗄️ Supabase Ecosystem"]
        SupaDB[(PostgreSQL DB)]
        SupaRLS[Row Level Security]
        SupaCleanup[Auto Cleanup Jobs]
    end
    
    subgraph External["🌐 External Services"]
        GitHub[GitHub API<br/>Image Hosting]
        Gemini[Google Gemini AI<br/>Primary]
        HuggingFace[Hugging Face<br/>Fallback AI]
        RSS[RSS Feed<br/>News API]
    end
    
    subgraph Services["📱 Flutter App Services"]
        AuthService[AuthService]
        DBService[DatabaseService]
        SupaService[SupabaseService]
        NotifService[NotificationService]
        ImageService[GithubImageService]
        AIService[AIService]
    end
    
    AuthService --> FireAuth
    AuthService --> Firestore
    
    DBService --> Firestore
    DBService --> SupaService
    
    SupaService --> SupaDB
    SupaService --> SupaRLS
    
    NotifService --> FCM
    NotifService --> SupaDB
    
    ImageService --> GitHub
    
    AIService --> Gemini
    AIService -.Fallback.-> HuggingFace
    
    DBService --> RSS
    
    Firestore -.Users.-> Users[users]
    Firestore -.Tests.-> Tests[tests]
    Firestore -.Categories.-> Categories[categories]
    
    SupaDB -.Stats.-> UserStats[user_stats]
    SupaDB -.Results.-> TestResults[test_results]
    SupaDB -.Notifs.-> Notifications[notifications]
    
    SupaCleanup -.24h.-> Notifications
    SupaCleanup -.5d.-> TestResults
    SupaCleanup -.15d.-> UserStats
```

---

## 🤖 AI Agents Configuration

### Google Gemini AI (Primary)

```mermaid
graph LR
    User[User Requests Explanation] --> AIService[AIService]
    AIService --> TryGemini{Try Gemini Keys}
    
    TryGemini -->|Key 1| Gemini1[Gemini API]
    TryGemini -->|Key 2| Gemini2[Gemini API]
    TryGemini -->|Key 3-10| GeminiN[Gemini API...]
    
    Gemini1 -->|Success| Return[Return Explanation]
    Gemini1 -->|Fail| TryNext1[Try Next Key]
    Gemini2 -->|Success| Return
    Gemini2 -->|Fail| TryNext2[Try Next Key]
    GeminiN -->|All Failed| Fallback[Fallback to HuggingFace]
    
    Fallback --> TryHF{Try HF Keys}
    TryHF -->|Key 1-10| HuggingFace[HuggingFace API]
    HuggingFace -->|Success| Return
    HuggingFace -->|All Failed| Error[Return Error Message]
```

### AI Configuration Details

**File Locations:**
- **API Keys**: `lib/config/api_config.dart`
- **Service**: `lib/services/ai_service.dart`

**Gemini Configuration:**
```dart
// lib/config/api_config.dart
static const List<String> _geminiKeysEnc = [
  // 10 obfuscated Gemini API keys
];

// lib/services/ai_service.dart
Future<String?> _generateWithGemini(String prompt, String apiKey) {
  final model = GenerativeModel(
    model: 'models/gemini-1.5-flash',
    apiKey: apiKey,
  );
  // Generate explanation
}
```

**Hugging Face Configuration:**
```dart
// lib/config/api_config.dart
static const List<String> _hfKeysEnc = [
  // 10 obfuscated Hugging Face API keys
];

// lib/services/ai_service.dart
Future<String?> _generateWithHuggingFace(String prompt, String apiKey) {
  const modelId = 'google/flan-t5-base';
  const url = 'https://api-inference.huggingface.co/models/$modelId';
  // API call with Bearer token
}
```

**Key Features:**
- ✅ 10 API keys per provider for redundancy
- ✅ Automatic key rotation on failure
- ✅ Obfuscated keys using `SecurityService`
- ✅ Seamless fallback from Gemini to HuggingFace
- ✅ Error handling with user-friendly messages


---

## 🔄 Complete Data Sync Flow

```mermaid
sequenceDiagram
    participant User
    participant App
    participant AuthService
    participant Firebase
    participant Supabase
    participant GitHub
    participant AI
    
    Note over User,AI: User Signup Flow
    User->>App: Sign Up
    App->>AuthService: createUser()
    AuthService->>Firebase: Create Auth User
    Firebase-->>AuthService: User UID
    AuthService->>Firebase: Save to Firestore
    AuthService->>Supabase: Create user_stats
    Supabase-->>AuthService: Stats Created
    AuthService-->>App: Success
    App-->>User: Welcome Screen
    
    Note over User,AI: Take Test Flow
    User->>App: Start Test
    App->>Firebase: Fetch Questions
    Firebase-->>App: Questions + Images
    User->>App: Submit Answers
    App->>App: Calculate Score
    App->>Supabase: Save test_results
    App->>Supabase: Update user_stats
    Supabase-->>App: Rankings Updated
    App-->>User: Show Results
    
    Note over User,AI: Admin Upload Image
    User->>App: Upload Image
    App->>GitHub: POST /repos/.../contents
    GitHub-->>App: Image URL
    App->>Firebase: Save URL in Question
    Firebase-->>App: Success
    App-->>User: Image Uploaded
    
    Note over User,AI: AI Explanation Request
    User->>App: Request Explanation
    App->>AI: Query Gemini API
    AI-->>App: Explanation
    alt Gemini Failed
        App->>AI: Fallback to HuggingFace
        AI-->>App: Explanation
    end
    App-->>User: Show Explanation
```

---

## 🧹 Auto Cleanup System Flow

```mermaid
graph TB
    Trigger[🔔 Admin Sends Notification] --> StartCleanup[🧹 Start Cleanup Process]
    
    StartCleanup --> Parallel{Run in Parallel}
    
    Parallel --> Clean1[Clean Notifications]
    Parallel --> Clean2[Clean Test Results]
    Parallel --> Clean3[Reset Leaderboard]
    
    Clean1 --> Query1[(🗄️ Query Supabase<br/>notifications table)]
    Query1 --> Check1{Age > 24h?}
    Check1 -->|Yes| Delete1[❌ DELETE Records]
    Check1 -->|No| Keep1[✅ Keep Records]
    Delete1 --> Log1[📝 Log Cleanup]
    
    Clean2 --> Query2[(🗄️ Query Supabase<br/>test_results table)]
    Query2 --> Check2{Age > 5 days?}
    Check2 -->|Yes| Delete2[❌ DELETE Records]
    Check2 -->|No| Keep2[✅ Keep Records]
    Delete2 --> Log2[📝 Log Cleanup]
    
    Clean3 --> Query3[(🗄️ Query Supabase<br/>user_stats table)]
    Query3 --> Check3{Inactive > 15 days?}
    Check3 -->|Yes| Reset[🔄 Reset Streaks to 0]
    Check3 -->|No| Keep3[✅ Keep Streaks]
    Reset --> Log3[📝 Log Reset]
    
    Log1 --> Complete[✅ Cleanup Complete]
    Log2 --> Complete
    Log3 --> Complete
```

---

## 🎯 Feature Module Connections

```mermaid
graph TB
    subgraph UI["📱 UI Layer"]
        LoginScreen[Login Screen]
        HomeScreen[Home Screen]
        QuizScreen[Quiz Screen]
        ProfileScreen[Profile Screen]
        AdminDashboard[Admin Dashboard]
    end
    
    subgraph Service["🔧 Service Layer"]
        AuthService[AuthService]
        DBService[DatabaseService]
        SupaService[SupabaseService]
        NotifService[NotificationService]
    end
    
    subgraph Data["💾 Data Layer"]
        FireAuth[(Firebase Auth)]
        Firestore[(Firestore)]
        Supabase[(Supabase)]
        LocalCache[(SharedPreferences)]
    end
    
    LoginScreen --> AuthService
    HomeScreen --> DBService
    HomeScreen --> SupaService
    QuizScreen --> DBService
    QuizScreen --> SupaService
    ProfileScreen --> AuthService
    ProfileScreen --> DBService
    AdminDashboard --> DBService
    AdminDashboard --> NotifService
    
    AuthService --> FireAuth
    AuthService --> Firestore
    AuthService --> LocalCache
    
    DBService --> Firestore
    DBService --> SupaService
    DBService --> LocalCache
    
    SupaService --> Supabase
    
    NotifService --> Firestore
    NotifService --> Supabase
```

---

This workflow document provides complete nvisual flows with better color contrast for readability! 🚀
