# Task List Progressive Web App

A comprehensive task list management application built with React, featuring offline support, multiple lists, and priority-based task organization.

## Features

✅ **Progressive Web App Requirements Met:**
- 5+ React single-file components (Navigation, Footer, Home, ListView, About, ListForm, TaskForm, TaskItem, ListCard)
- Children prop usage (Footer component)
- List rendering (task lists and task items)
- Conditional rendering (show/hide completed tasks, loading states, empty states)
- React Router with multiple routes (/, /list/:id, /about)
- Navigation bar, lists, and footer
- Context API for state management
- Firestore database with offline persistence
- Responsive design with Bootstrap
- Form validation and error handling

## Setup Instructions

### 1. Install Dependencies
```bash
npm install
```

### 2. Firebase Setup
1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Create a new project
3. Enable Firestore Database
4. Get your Firebase configuration
5. Replace the config in `src/context/TaskContext.js`:

```javascript
const firebaseConfig = {
  apiKey: "your-api-key",
  authDomain: "your-project.firebaseapp.com",
  projectId: "your-project-id",
  storageBucket: "your-project.appspot.com",
  messagingSenderId: "123456789",
  appId: "your-app-id"
};
```

### 3. Firestore Rules
Set up Firestore security rules:
```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /lists/{document=**} {
      allow read, write: if true; // For demo purposes - restrict in production
    }
  }
}
```

### 4. Run the Application
```bash
npm start
```

## Usage

### Creating Lists
1. Click "Create New List" on the home page
2. Enter a list name and optional description
3. Click "Create List"

### Managing Tasks
1. Click "View List" on any list card
2. Click "Add New Task" to create tasks
3. Set task description and priority (High, Medium, Low)
4. Tasks are automatically sorted by priority

### Task Operations
- **Complete/Incomplete**: Check/uncheck the checkbox
- **Delete**: Click the delete button
- **Filter**: Toggle "Show completed tasks" switch

### List Operations
- **View**: Click "View List" to see all tasks
- **Delete**: Click "Delete" button (with confirmation)
- **Navigate**: Use the navigation to switch between lists

## Technical Implementation

### Components Structure
- **App.js**: Main application with routing
- **Navigation.js**: Top navigation bar with online/offline status
- **Footer.js**: Footer component (uses children prop)
- **Home.js**: Main page showing all lists
- **ListView.js**: Individual list view with tasks
- **About.js**: Information page
- **ListForm.js**: Form for creating new lists
- **TaskForm.js**: Form for creating new tasks
- **TaskItem.js**: Individual task component
- **ListCard.js**: List summary card component

### State Management
- Uses React Context API (`TaskContext`)
- Firestore real-time updates
- Offline persistence enabled
- Error handling and loading states

### Responsive Design
- Bootstrap 5 for responsive layout
- Mobile-first approach
- Flexible grid system
- Touch-friendly interface

## PWA Features
- Service Worker for caching
- Manifest.json for app-like experience
- Offline functionality
- Responsive design

## Firestore Data Structure
```
lists (collection)
├── listId (document)
    ├── name: string
    ├── description: string
    ├── createdAt: timestamp
    └── items: array
        ├── id: number
        ├── task: string
        ├── priority: string
        ├── completed: boolean
        └── createdAt: string
```

## Browser Compatibility
- Modern browsers with ES6+ support
- Chrome, Firefox, Safari, Edge
- Mobile browsers (iOS Safari, Chrome Mobile)

## Development
- Built with Create React App
- React 18 with functional components and hooks
- TypeScript support ready (rename .js to .tsx)
- ESLint configuration included
