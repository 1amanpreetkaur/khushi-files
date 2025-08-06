# Firebase Setup Guide

## Step 1: Create a Firebase Project

1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Click "Create a project"
3. Enter project name: `task-list-pwa`
4. Enable or disable Google Analytics (optional)
5. Click "Create project"

## Step 2: Set up Firestore Database

1. In the Firebase console, click "Firestore Database"
2. Click "Create database"
3. Choose "Start in test mode" (for development)
4. Select a location (choose the closest to your users)
5. Click "Done"

## Step 3: Get Firebase Configuration

1. In the Firebase console, click the gear icon (Project settings)
2. Scroll down to "Your apps" section
3. Click "Web" icon (</>)
4. Register your app with name: `Task List PWA`
5. Copy the Firebase configuration object

## Step 4: Configure the App

1. Open `src/context/TaskContext.js`
2. Replace the `firebaseConfig` object with your actual configuration:

```javascript
const firebaseConfig = {
  apiKey: "your-actual-api-key",
  authDomain: "your-project.firebaseapp.com",
  projectId: "your-project-id",
  storageBucket: "your-project.appspot.com",
  messagingSenderId: "123456789",
  appId: "your-app-id"
};
```

## Step 5: Set Firestore Security Rules

1. In the Firebase console, go to "Firestore Database"
2. Click "Rules" tab
3. Replace the rules with:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /lists/{document=**} {
      allow read, write: if true; // For demo - use authentication in production
    }
  }
}
```

4. Click "Publish"

## Step 6: Enable Offline Persistence (Already done in code)

The app already has offline persistence enabled in the Firebase configuration. This allows the app to work when offline and sync when back online.

## Step 7: Test the Application

1. Run `npm start` to start the development server
2. Open http://localhost:3000 in your browser
3. Create a new list
4. Add some tasks
5. Test offline functionality by going offline and adding tasks

## Production Deployment

For production deployment:

1. Build the app: `npm run build`
2. Deploy to Firebase Hosting or any static hosting service
3. Update Firestore security rules to use proper authentication
4. Consider adding authentication with Firebase Auth

## Security Note

The current configuration allows all reads and writes for demonstration purposes. In production, you should:

1. Enable Firebase Authentication
2. Update Firestore rules to require authentication
3. Add user-specific data access controls

Example production rules:
```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /lists/{listId} {
      allow read, write: if request.auth != null && request.auth.uid == resource.data.userId;
    }
  }
}
```
