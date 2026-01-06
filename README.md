# MINT_sample_games_2025

A genome assembly puzzle game for educational purposes.

## 🎮 How to Play

1. Select difficulty level (Easy/Medium/Hard/Expert)
2. Select ploidy mode (Haploid/Polyploid)
3. Click "Start Game" to begin
4. Drag and drop genome fragments to reconstruct the sequence
5. Match the orange overlap regions to connect pieces correctly

## 🚀 Deployment

### Local Development

Simply open `index.html` in your browser. Scores will be saved locally using localStorage.

### Deploy to Vercel (with Cloud Scores)

1. Push this repository to GitHub
2. Connect to Vercel and deploy
3. Configure Firebase (see below) for shared leaderboards

## ☁️ Firebase Setup (for Global Rankings)

To enable cloud-based score sharing when deployed to Vercel:

### Step 1: Create Firebase Project

1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Click "Add project"
3. Enter a project name and follow the setup wizard

### Step 2: Enable Realtime Database

1. In Firebase Console, go to **Build > Realtime Database**
2. Click "Create Database"
3. Choose a location (closest to your users)
4. Start in **test mode** (you can secure it later)

### Step 3: Get Configuration

1. Go to **Project Settings** (gear icon)
2. Scroll to "Your apps" and click the web icon (`</>`)
3. Register your app and copy the configuration

### Step 4: Update index.html

Replace the placeholder values in `FIREBASE_CONFIG`:

```javascript
const FIREBASE_CONFIG = {
    apiKey: "AIzaSy...",           // Your actual API key
    authDomain: "your-project.firebaseapp.com",
    databaseURL: "https://your-project-default-rtdb.firebaseio.com",
    projectId: "your-project",
    storageBucket: "your-project.appspot.com",
    messagingSenderId: "123456789",
    appId: "1:123456789:web:abc123"
};
```

### Step 5: Set Security Rules (Recommended)

In Firebase Console > Realtime Database > Rules:

```json
{
  "rules": {
    "scores": {
      ".read": true,
      ".write": true,
      ".indexOn": ["time", "difficulty", "ploidy"]
    }
  }
}
```

> ⚠️ For production, consider adding validation rules to prevent abuse.

## 🔄 How Environment Detection Works

The game automatically detects the environment:

| Environment | Rankings Mode | Storage |
|-------------|---------------|---------|
| `localhost` | Local | localStorage |
| `file://` | Local | localStorage |
| `*.github.io` | Local | localStorage |
| `*.vercel.app` | Global (if configured) | Firebase |
| Custom domain | Global (if configured) | Firebase |

If Firebase is not configured (placeholder values remain), it falls back to local mode everywhere.

## 📝 License

MIT License
