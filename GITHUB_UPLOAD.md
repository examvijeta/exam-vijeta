# 🚀 GitHub Upload Workflow

Follow these steps to upload your project to GitHub.

---

## 📋 Pre-Upload Checklist

- [ ] Remove sensitive data (API keys, passwords)
- [ ] Update `.gitignore` file
- [ ] Test the app locally
- [ ] Update README with your details
- [ ] Add LICENSE file (if needed)

---

## 🔐 Secure Your API Keys

### 1. Update `.gitignore`

Make sure these files are in `.gitignore`:

```
# API Keys & Secrets
lib/config/api_config.dart
google-services.json
GoogleService-Info.plist

# Environment files
.env
*.env

# Build files
build/
.dart_tool/
```

### 2. Create Template Config

Create `lib/config/api_config.template.dart`:

```dart
class ApiConfig {
  static const String supabaseUrl = 'YOUR_SUPABASE_URL';
  static const String supabaseAnonKey = 'YOUR_SUPABASE_ANON_KEY';
  static const String githubToken = 'YOUR_GITHUB_TOKEN';
  static const String geminiApiKey = 'YOUR_GEMINI_API_KEY';
}
```

---

## 📤 Upload Steps

### Step 1: Initialize Git

```bash
cd mock_test_flutter
git init
```

### Step 2: Create `.gitignore`

```bash
# Flutter/Dart
.dart_tool/
.flutter-plugins
.flutter-plugins-dependencies
.packages
build/
*.iml
*.ipr
*.iws
.idea/

# API Keys & Secrets
lib/config/api_config.dart
android/app/google-services.json
ios/Runner/GoogleService-Info.plist
.env

# Windows
windows/flutter/ephemeral/

# Android
android/.gradle/
android/local.properties
android/app/debug/
android/app/profile/
android/app/release/

# iOS
ios/Pods/
ios/.symlinks/
ios/Flutter/App.framework
ios/Flutter/Flutter.framework
ios/Flutter/Flutter.podspec
```

### Step 3: Add Files

```bash
git add .
git commit -m "Initial commit: Mock Test App"
```

### Step 4: Create GitHub Repository

1. Go to [GitHub](https://github.com)
2. Click **"New Repository"**
3. Name: `mock_test_flutter`
4. Description: "Complete Learning Platform with AI-Powered Features"
5. Choose **Private** or **Public**
6. Click **"Create Repository"**

### Step 5: Link & Push

```bash
# Add remote
git remote add origin https://github.com/YOUR_USERNAME/mock_test_flutter.git

# Push to GitHub
git branch -M main
git push -u origin main
```

---

## 🎨 Add Repository Details

### Topics (Add in GitHub Settings)

```
flutter
dart
firebase
supabase
mock-test
education
learning-platform
quiz-app
leaderboard
admin-panel
```

### About Section

```
📚 Complete Learning Platform with AI-Powered Features
🔥 Streak tracking, leaderboards, and intelligent data management
```

---

## 📸 Add Screenshots (Optional)

Create `screenshots/` folder:

```bash
mkdir screenshots
```

Add images:
- `home_screen.png`
- `quiz_screen.png`
- `leaderboard.png`
- `admin_dashboard.png`

Update README to include:

```markdown
## 📱 Screenshots

<div align="center">
  <img src="screenshots/home_screen.png" width="200"/>
  <img src="screenshots/quiz_screen.png" width="200"/>
  <img src="screenshots/leaderboard.png" width="200"/>
</div>
```

---

## 🔄 Future Updates

### Update Code

```bash
git add .
git commit -m "Description of changes"
git push origin main
```

### Create Release

1. Go to **Releases** on GitHub
2. Click **"Create a new release"**
3. Tag: `v1.0.0`
4. Title: `Version 1.0.0 - Initial Release`
5. Add release notes
6. Attach APK file (optional)
7. Click **"Publish release"**

---

## 🛡️ Security Best Practices

### Never Commit:
- ❌ API keys
- ❌ Passwords
- ❌ Firebase config files
- ❌ Private tokens
- ❌ `.env` files

### Always Use:
- ✅ Environment variables
- ✅ Template config files
- ✅ `.gitignore`
- ✅ GitHub Secrets (for CI/CD)

---

## 📝 README Customization

Before uploading, update these in README:

1. **Repository URL**: Replace `yourusername` with your GitHub username
2. **Email**: Update support email
3. **License**: Add appropriate license
4. **Screenshots**: Add actual app screenshots
5. **Demo Link**: Add live demo link (if available)

---

## ✅ Final Checklist

- [ ] All sensitive data removed
- [ ] `.gitignore` configured
- [ ] README updated with your details
- [ ] Repository created on GitHub
- [ ] Code pushed successfully
- [ ] Topics added
- [ ] About section filled
- [ ] License added (if needed)

---

## 🎉 Done!

Your project is now on GitHub! 🚀

**Repository URL**: `https://github.com/YOUR_USERNAME/mock_test_flutter`

---

## 📚 Additional Resources

- [GitHub Docs](https://docs.github.com)
- [Git Basics](https://git-scm.com/book/en/v2/Getting-Started-Git-Basics)
- [Flutter Deployment](https://docs.flutter.dev/deployment)
