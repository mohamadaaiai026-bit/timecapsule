# 🎁 Time Capsule

> Create surprise messages that unlock on special dates


<p align="center">
  <img src="screenshots/demo.gif" alt="Time Capsule Demo" width="300"/>
</p>

## 🎯 Problem & Solution

**Problem**: Special occasions like birthdays feel less special when everyone sends messages on the day itself.

**Solution**: Time Capsule lets friends create surprise messages BEFORE the date, which unlock automatically on the special day - creating a more meaningful, anticipated experience.

## ✨ Features

### 🎨 Three Themed Experiences
- **Birthday**: Candle decorations on birthday cake
- **Christmas**: Ornaments on Christmas tree (Fixed: Dec 25)
- **Valentine**: Roses in bouquet (Fixed: Feb 14)

### 🔗 Viral Deep Linking
- Share events via web links (GitHub Pages + Android App Links)
- Friends tap link → Opens app directly
- Fallback to web page with download button

### 🎯 Custom Decoration System
- Dynamic positioning algorithm
- Each theme has unique decoration placement logic
- Decorations reveal messages when event unlocks

### 🔒 Secure & Private
- Row-level security with Supabase
- Google OAuth authentication
- Users can only delete their own events
- Messages visible to all (by design - social experience)

## 📲 Try It

**[📥 Download APK (Android)](https://github.com/mohamadaaiai026-bit/timecapsule/releases/latest)**

**[🎥 Watch Demo Video](https://drive.google.com/file/d/1xqDcShnvxnUu0y-ZbDvCc49hG3zYuZVK/view)**

## 🛠️ Tech Stack

### Frontend
- **Flutter 3.x** - Cross-platform framework
- **Dart** - Programming language
- **GetX** - State management & routing

### Backend
- **Supabase** - PostgreSQL database + Authentication
- **Row-Level Security** - Data protection
- **Real-time subscriptions** - Live updates (future)

### Infrastructure
- **GitHub Pages** - Deep link landing page
- **Android App Links** - Seamless app opening
- **Google Sign-In** - OAuth authentication

## 🏗️ Architecture
```
lib/
├── controllers/          # GetX controllers (state management)
│   ├── auth_controller.dart
│   ├── home_controller.dart
│   ├── event_controller.dart
│   └── deep_link_controller.dart
├── models/              # Data models
│   ├── event_model.dart
│   ├── message_model.dart
│   └── theme_model.dart
├── services/            # API integration
│   ├── event_service.dart
│   ├── message_service.dart
│   └── auth_service.dart
├── views/
│   ├── screens/         # Full pages
│   └── widgets/         # Reusable components
└── core/
    ├── functions/       # Utilities
    └── config/          # Configuration
```

**Pattern**: MVC (Model-View-Controller)
- **Models**: Data structures
- **Views**: UI components
- **Controllers**: Business logic & state

## 🔧 Key Implementations

### 1. Deep Linking Flow
```dart
// User shares: https://mohamadaaiai026-bit.github.io/timecapsule/ABC123
// AndroidManifest.xml recognizes link → Opens app
// DeepLinkController extracts "ABC123" → Loads event
```

### 2. Dynamic Decoration Positioning
```dart
// Each theme has custom positioning logic
// Birthday: Candles placed in arc on cake
// Christmas: Ornaments scattered on tree
// Valentine: Roses arranged in bouquet layers
```

### 3. Row-Level Security (Supabase)
```sql
-- Users can only delete their own events
CREATE POLICY "Users can delete own events"
ON events FOR DELETE
USING (auth.uid() = user_id);

-- Everyone can view shared messages (social feature)
CREATE POLICY "Messages are public"
ON messages FOR SELECT
USING (true);
```

## 📊 Database Schema
```sql
-- Events table
CREATE TABLE events (
  id UUID PRIMARY KEY,
  user_id UUID REFERENCES auth.users,
  title TEXT,
  theme_id TEXT,
  unlock_datetime TIMESTAMPTZ,
  share_code TEXT UNIQUE,
  created_at TIMESTAMPTZ
);

-- Messages table
CREATE TABLE messages (
  id UUID PRIMARY KEY,
  event_id UUID REFERENCES events,
  sender_name TEXT,
  content TEXT,
  decoration_type TEXT,
  created_at TIMESTAMPTZ
);
```

## 🚀 Getting Started

### Prerequisites
- Flutter SDK 3.x
- Android Studio / VS Code
- Supabase account

### Installation

1. **Clone the repository**
```bash
git clone https://github.com/mohamadaaiai026-bit/timecapsule.git
cd timecapsule
```

2. **Install dependencies**
```bash
flutter pub get
```

3. **Configure Supabase**
- Create project at https://supabase.com
- Update `lib/core/constant/supabase_config.dart`:
```dart
class SupabaseConfig {
  static const String supabaseUrl = 'YOUR_URL';
  static const String supabaseAnonKey = 'YOUR_KEY';
}
```

4. **Run the app**
```bash
flutter run
```

## 📈 Roadmap

- [x] Core messaging functionality
- [x] Three themed experiences
- [x] Deep linking
- [x] Google authentication
- [ ] In-app purchase (Unlock Early - $2.99)
- [ ] More themes (Halloween, New Year)
- [ ] iOS support
- [ ] Message reactions/comments

## 🤝 Contributing

Contributions, issues, and feature requests are welcome!

## 📧 Contact

**Mohamed** - [LinkedIn]([https://linkedin.com/in/yourprofile](https://www.linkedin.com/in/mohamad-alnabhan-a87b89383/))

⭐ **Open to mobile development opportunities!**


<p align="center">
  <img src="screenshots/1-login.jpg" width="200"/>
  <img src="screenshots/2-theme_selection.jpg" width="200"/>
  <img src="screenshots/3-message.png" width="200"/>
</p>

<p align="center">
  Made with ❤️ using Flutter
</p>

<p align="center">
  ⭐ Star this repo if you find it useful!
</p>
```

---

