# Firebase Setup Guide

## Firebase Configuration Instructions

### 1. Create a Firebase Project
   - Go to the [Firebase Console](https://console.firebase.google.com/).
   - Click on "Add project."
   - Enter your project name and click "Continue."
   - Enable Google Analytics for your project (if needed) and click "Create project."

### 2. Add Firebase SDK to Your App
   - Click on the web icon to add Firebase to your web app.
   - Register your app with a nickname and click "Register app."
   - Install Firebase via npm (if using Node.js):  
     ```bash
     npm install firebase
     ```
   - Include Firebase SDK scripts in your HTML:
     ```html
     <script src="https://www.gstatic.com/firebasejs/9.x.x/firebase-app.js"></script>
     <script src="https://www.gstatic.com/firebasejs/9.x.x/firebase-auth.js"></script>
     ```

### 3. Firebase Configuration Object
   - Go to your project's settings and find your Firebase config object:
   ```javascript
   const firebaseConfig = {
       apiKey: "YOUR_API_KEY",
       authDomain: "YOUR_AUTH_DOMAIN",
       databaseURL: "YOUR_DATABASE_URL",
       projectId: "YOUR_PROJECT_ID",
       storageBucket: "YOUR_STORAGE_BUCKET",
       messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
       appId: "YOUR_APP_ID"
   };
   ```
   - Initialize Firebase:
   ```javascript
   firebase.initializeApp(firebaseConfig);
   ```

## Email OTP Implementation Details

### 1. Setup Email Authentication
   - In Firebase Console, go to "Authentication" > "Sign-in method."
   - Enable "Email/Password" provider.

### 2. Send OTP via Email
   - Create a function to send OTP:
   ```javascript
   const sendEmailVerification = (user) => {
       user.sendEmailVerification().then(() => {
           console.log('Verification email sent!');
       }).catch((error) => {
           console.error('Error sending email verification:', error);
       });
   };
   ```

### 3. Verify OTP
   - Ask users to check their email and verify:
   ```javascript
   const verifyEmail = () => {
       firebase.auth().onAuthStateChanged((user) => {
           if (user) {
               if (user.emailVerified) {
                   console.log('Email verified.');
               } else {
                   console.log('Email not verified. Please check your inbox.');
               }
           }
       });
   };
   ```

### Conclusion
   Follow these steps to set up Firebase and implement email OTP for user authentication. For more details, refer to the [Firebase Documentation](https://firebase.google.com/docs).