# Firebase Setup Guide

This app uses Firebase for real-time database and authentication. Follow these steps to connect your Firebase project.

## Step 1: Create a Firebase Project

1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Click "Add project" or select an existing project
3. Follow the setup wizard

## Step 2: Enable Firebase Services

### Enable Realtime Database
1. In Firebase Console, go to **Build → Realtime Database**
2. Click **Create Database**
3. Choose a location
4. Start in **Test mode** (you can configure security rules later)

### Enable Authentication
1. Go to **Build → Authentication**
2. Click **Get started**
3. Enable **Email/Password** sign-in method
4. Add your first user in the Users tab

## Step 3: Get Your Firebase Config

1. In Firebase Console, click the gear icon ⚙️ → **Project settings**
2. Scroll down to **Your apps** section
3. Click the web icon `</>` to add a web app
4. Register your app with a nickname
5. Copy the `firebaseConfig` object

## Step 4: Add Environment Variables

Create a `.env` file in your project root (or add to Lovable secrets):

```env
VITE_FIREBASE_API_KEY=your_api_key_here
VITE_FIREBASE_AUTH_DOMAIN=your-project.firebaseapp.com
VITE_FIREBASE_DATABASE_URL=https://your-project-default-rtdb.firebaseio.com
VITE_FIREBASE_PROJECT_ID=your-project-id
VITE_FIREBASE_STORAGE_BUCKET=your-project.appspot.com
VITE_FIREBASE_MESSAGING_SENDER_ID=123456789
VITE_FIREBASE_APP_ID=1:123456789:web:abcdef123456
```

⚠️ **Important:** The `databaseURL` must be in the format: `https://your-project-default-rtdb.firebaseio.com`

## Step 5: Initialize Your Database

After authentication is working, your database will automatically create the structure when you first use the controls:

```json
{
  "SMART_FARM": {
    "controls": {
      "autoMode": true,
      "laserSystem": false,
      "pump": false,
      "startTime": "20:17",
      "stopDuration": "00:01"
    }
  }
}
```

## Testing

1. Start your app
2. You should see: `✅ Firebase initialized successfully` in the console
3. Create a test user account
4. Try toggling controls - changes should persist in Firebase

## Security Rules (Optional)

For production, update your Realtime Database rules:

```json
{
  "rules": {
    "SMART_FARM": {
      ".read": "auth != null",
      ".write": "auth != null"
    }
  }
}
```

## Troubleshooting

- **"Cannot parse Firebase url"** - Check your `VITE_FIREBASE_DATABASE_URL` format
- **"Permission denied"** - Update your database security rules
- **"Auth domain mismatch"** - Add your domain to authorized domains in Firebase Console

## Demo Mode

The app will work in demo mode without Firebase configuration, but changes won't persist. You'll see notifications indicating demo mode.
