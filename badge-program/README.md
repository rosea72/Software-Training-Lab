# Software Training Lab - Badge Program

A web-based badge tracking system for software training programs. Students can track their progress across multiple software applications and earn badges as they complete requirements.

## Features

- 🎯 **Badge System**: 30+ badges across 10+ software applications
- 🖼️ **Professional Logos**: Real software logos for each application
- 📊 **Progress Tracking**: Real-time tracking of requirements and submissions
- 👥 **Multi-User Support**: Admin dashboard to view all students
- 🔐 **Sage Mode**: Password-protected endorsement system for instructors
- 💾 **Cloud Sync**: Firebase integration for data persistence
- 📱 **Responsive Design**: Works on desktop and mobile devices

## Quick Start (Without Database)

The application works immediately in offline mode using browser localStorage:

1. Clone this repository
2. Open `index.html` in a web browser
3. Enter your name and start tracking badges

**Note**: In offline mode, data is only stored locally in your browser.

## File Structure

```
badge-program/
├── index.html          # Main application file
├── logos/              # Software logo images
│   ├── After_Effects.jpeg
│   ├── Davinci_Resolve.jpeg
│   ├── Excel.jpeg
│   ├── GarageBand.jpeg
│   ├── Illustrator.jpeg
│   ├── InDesign.jpeg
│   ├── Lightroom.jpeg
│   ├── Photoshop.jpeg
│   ├── PowerPoint.jpeg
│   ├── Premiere.jpeg
│   ├── Procreate.jpeg
│   └── Word.jpeg
└── README.md           # This file
```

## Firebase Setup (For Multi-User Cloud Sync)

To enable cloud database features:

### 1. Create Firebase Project

1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Click "Add project" or select existing project
3. Follow the setup wizard

### 2. Enable Firestore Database

1. In Firebase Console, go to **Build > Firestore Database**
2. Click "Create database"
3. Start in **production mode** or **test mode** (for testing)
4. Choose a region close to your users

### 3. Get Your Firebase Config

1. Go to **Project Settings** (gear icon)
2. Scroll to "Your apps" section
3. Click the **web icon** (`</>`) to add a web app
4. Register your app (give it a nickname)
5. Copy the `firebaseConfig` object

### 4. Configure the App

Open `index.html` and find this section (around line 233):

```javascript
const YOUR_FIREBASE_CONFIG = {
    apiKey: "YOUR_API_KEY_HERE",
    authDomain: "YOUR_PROJECT_ID.firebaseapp.com",
    projectId: "YOUR_PROJECT_ID",
    storageBucket: "YOUR_PROJECT_ID.appspot.com",
    messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
    appId: "YOUR_APP_ID"
};
```

Replace with your actual Firebase config:

```javascript
const YOUR_FIREBASE_CONFIG = {
    apiKey: "AIzaSyDXXXXXXXXXXXXXXXXXXXXXXXX",
    authDomain: "your-project.firebaseapp.com",
    projectId: "your-project-id",
    storageBucket: "your-project.appspot.com",
    messagingSenderId: "123456789012",
    appId: "1:123456789012:web:abcdef123456"
};
```

### 5. Configure Firestore Security Rules

In Firebase Console, go to **Firestore Database > Rules** and add:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /badgeProgram/data/users/{userId} {
      allow read: if request.auth != null;
      allow write: if request.auth != null;
    }
  }
}
```

For testing, you can use (⚠️ **NOT recommended for production**):

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if true;
    }
  }
}
```

## Deploy to GitHub Pages

### Option 1: Using GitHub Web Interface

1. Create a new repository on GitHub
2. Upload **all files**:
   - `index.html`
   - `README.md`
   - `logos/` folder with all logo images
3. Go to **Settings > Pages**
4. Under "Source", select **main** branch
5. Click **Save**
6. Your site will be live at `https://yourusername.github.io/repository-name/`

### Option 2: Using Git Command Line

```bash
# Initialize git repository
git init

# Add your files
git add index.html README.md logos/

# Commit
git commit -m "Initial commit with logo images"

# Add remote (replace with your repository URL)
git remote add origin https://github.com/yourusername/badge-program.git

# Push to GitHub
git branch -M main
git push -u origin main

# Enable GitHub Pages in repository settings
```

**Important**: Make sure the `logos/` folder is uploaded with all the JPEG files. The application won't display badge icons without these images.

## Usage

### For Students

1. Enter your full name on the welcome screen
2. Browse available badges or search for specific software
3. Click a badge to view requirements
4. Check off completed requirements
5. Submit your work link (Box/Drive folder)
6. Wait for instructor endorsement

### For Instructors (Sage Mode)

1. Click on any student's badge
2. Click "Unlock Sage Mode"
3. Enter password: `STL Lead`
4. Review student's checklist and submission
5. Click "Endorse Badge" when requirements are met

### Admin Dashboard

- Click the admin icon (people icon) in the header
- View all students and their progress
- Click "View Record" to switch to any student's view

## Software Badges Available

- **Photoshop** (3 levels)
- **Illustrator** (3 levels)
- **InDesign** (4 levels)
- **Premiere Pro** (3 levels)
- **After Effects** (3 levels)
- **Excel** (3 levels)
- **Word** (3 levels)
- **ETD** (2 levels)
- **DaVinci Resolve** (2 levels)
- **Procreate** (2 levels)

## Customization

### Change Sage Mode Password

Find this line in the JavaScript (around line 547):

```javascript
if (document.getElementById('sage-password').value === "STL Lead") {
```

Replace `"STL Lead"` with your desired password.

### Add/Modify Badges

Find the `BADGE_DATA` array (around line 244) and add your badges:

```javascript
{ 
    id: "unique-id", 
    software: "Software Name", 
    level: 1, 
    title: "Badge Title", 
    icon: `<svg>...</svg>`, 
    requirements: ["Requirement 1", "Requirement 2", ...]
}
```

## Troubleshooting

### "Firebase not configured" error
- Make sure you've replaced the placeholder config with your actual Firebase credentials
- Check browser console for specific error messages

### Data not saving
- Verify Firestore security rules allow read/write access
- Check that your Firebase project has Firestore enabled
- In offline mode, data only persists in browser localStorage

### Can't endorse badges
- Ensure all requirements are checked
- Verify you've unlocked Sage Mode with correct password

## Browser Compatibility

- Chrome/Edge (recommended)
- Firefox
- Safari
- Mobile browsers (iOS Safari, Chrome Mobile)

## Privacy & Data

- Student names and progress are stored in Firestore
- No personal information beyond name is collected
- Data is shared among all users of the same Firebase project
- For private deployments, use Firebase security rules to restrict access

## License

MIT License - Feel free to use and modify for your training program

## Support

For issues or questions, please open an issue on GitHub.

---

Made for Software Training Labs with ❤️
