# Fine Soil

A personal Bible reading companion: one chapter a day, streaks, a bookshelf that fills as you read,
Google Calendar sync, meeting preparation and reminders. Installable on iPhone, Android and desktop.

## Files
- index.html            the whole app (HTML, CSS and JavaScript)
- manifest.webmanifest  install details (name, colours, icons)
- sw.js                 service worker (lets the app open offline)
- firebase-config.js    only needed if you do NOT host on Firebase Hosting
- firebase.json         Firebase Hosting settings
- favicon*.svg/png, icon-*.png, apple-touch-icon.png   icons
- brand/                logo concepts and brand notes

## Set up (once)
1. Create a Firebase project (console.firebase.google.com).
2. Authentication -> Sign-in method -> turn on Google.
3. Firestore Database -> create one, then set these rules:

   rules_version = '2';
   service cloud.firestore {
     match /databases/{database}/documents {
       match /users/{uid} {
         allow read, write: if request.auth != null && request.auth.uid == uid;
       }
     }
   }

4. Add a Web app in Project settings so the project has a web config.
5. In Google Cloud Console (same project): enable the Google Calendar API, and on the
   OAuth consent screen add your own Google account as a test user.

## Deploy (Firebase Hosting)
    npm install -g firebase-tools
    firebase login
    firebase init hosting     # pick your project, public folder ".", do NOT overwrite index.html
    firebase deploy

On Firebase Hosting the app finds its settings automatically. Then, in Firebase ->
Authentication -> Settings -> Authorized domains, make sure your hosting address is listed.

Other hosts (Netlify, GitHub Pages, Cloudflare Pages): upload the folder, add the host's address to
Authorized domains, and paste your Firebase config into firebase-config.js first.

## Install on a phone
iPhone: open the address in Safari -> Share -> Add to Home Screen.
Android / desktop Chrome: use the Install button in Settings, or the browser menu.

## Notes
- Reading progress is saved on the device and, when signed in, to your Firestore account.
- Calendar events go in a calendar the app creates ("Daily Bible Reading"). It only asks for
  permission to manage that calendar.
- Not tested on a live Firebase project or real devices: test sign-in, calendar sync and the
  JW Library link on your own phone first.
- Check the name "Fine Soil" for existing uses and domain availability before public use.
