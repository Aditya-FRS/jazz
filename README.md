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
