rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{email} {
      allow read: if request.auth != null;
      allow write: if request.auth != null && request.auth.token.email == email;
    }
    match /status/{email} {
      allow read: if request.auth != null;
      allow write: if request.auth != null && request.auth.token.email == email;
    }
    match /usageLogs/{id} {
      allow read: if request.auth != null;
      allow create: if request.auth != null && request.resource.data.email == request.auth.token.email;
      allow update: if request.auth != null && resource.data.email == request.auth.token.email;
    }
    match /chat/{id} {
      allow read: if request.auth != null;
      allow create: if request.auth != null && request.resource.data.email == request.auth.token.email;
    }
    match /config/schedule {
      allow read: if request.auth != null;
      allow write: if request.auth != null; // tighten to a custom claim/admin allow-list if you want stricter control
    }
    match /reminders/{id} {
      allow read, write: if false; // only the cron job's Admin SDK (server-side, bypasses rules) touches this
    }
  }
}








dvfh




// Import the functions you need from the SDKs you need
import { initializeApp } from "firebase/app";
// TODO: Add SDKs for Firebase products that you want to use
// https://firebase.google.com/docs/web/setup#available-libraries

// Your web app's Firebase configuration
const firebaseConfig = {
  apiKey: "AIzaSyAupC_gE4o7PMLXgaGpMNLBSIld8w6I-0k",
  authDomain: "kronos-5aff6.firebaseapp.com",
  projectId: "kronos-5aff6",
  storageBucket: "kronos-5aff6.firebasestorage.app",
  messagingSenderId: "1057500959007",
  appId: "1:1057500959007:web:a9bf45b39085903f9c602a"
};

// Initialize Firebase
const app = initializeApp(firebaseConfig);
