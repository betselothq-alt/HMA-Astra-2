# HMA Astra Club OS

Files:
- index.html — complete member/admin web application.
- firestore.rules — role-based Firestore security rules.
- functions/index.js — scheduled reminder function.
- functions/package.json — Cloud Functions dependencies.

## 1. Firebase Authentication
Firebase Console → Authentication → Sign-in method → enable Email/Password.

## 2. Firestore
Create Firestore Database and publish `firestore.rules`.

Collections used:
members
courses
sessions
attendance
reminders
mail

## 3. First administrator
Register normally. Your account is initially `Member`.
In Firebase Console, open Firestore → members → your UID and change:
role: "Admin"

After that, use the Admin panel to promote other members.

## 4. Real welcome/program emails
The HTML app queues mail documents in the `mail` collection.
Install Firebase's official "Trigger Email" extension and configure an SMTP provider.
Do NOT put SMTP passwords or service-account private keys in index.html.

## 5. Real reminders
From the functions folder:
npm install
firebase deploy --only functions

The scheduled function checks reminders every 15 minutes and queues mail documents.
The Trigger Email extension then sends those emails.

## 6. Hosting
For GitHub Pages:
- upload index.html at the repository root
- make sure the file is named exactly `index.html`
- enable Pages from the main branch/root

Demo Mode works without Firebase data so you can preview the UI immediately.
