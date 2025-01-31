# Firebase-Integrated HTML Project Documentation

## Project Structure
```
project-folder/
│-- index.html
│-- style.css
│-- script.js
│-- firebase.js
│-- firebase.json (for hosting)
```

## Step 1: Create an HTML File
Create a file named `index.html` and add the following code:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Firebase Website</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <h1>Welcome to My Website</h1>
    <input type="email" id="email" placeholder="Enter Email">
    <input type="password" id="password" placeholder="Enter Password">
    <button onclick="signup()">Sign Up</button>
    <button onclick="login()">Login</button>
    <button onclick="logout()">Logout</button>
    
    <script src="https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js"></script>
    <script src="https://www.gstatic.com/firebasejs/10.7.1/firebase-auth.js"></script>
    <script src="firebase.js"></script>
    <script src="script.js"></script>
</body>
</html>
```

## Step 2: Create a CSS File for Styling
Create a file named `style.css` and add:

```css
body {
    font-family: Arial, sans-serif;
    text-align: center;
    margin: 50px;
}
input {
    display: block;
    margin: 10px auto;
    padding: 8px;
    width: 200px;
}
button {
    padding: 10px;
    margin: 5px;
    cursor: pointer;
}
```

## Step 3: Set Up Firebase
1. Go to [Firebase Console](https://console.firebase.google.com/).
2. Click **Add Project** and follow the setup process.
3. Enable **Authentication** under Firebase Services.
4. Copy your Firebase configuration.

## Step 4: Add Firebase Configuration
Create a file `firebase.js` and paste the Firebase configuration:

```javascript
const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_PROJECT.firebaseapp.com",
    projectId: "YOUR_PROJECT_ID",
    storageBucket: "YOUR_PROJECT.appspot.com",
    messagingSenderId: "YOUR_SENDER_ID",
    appId: "YOUR_APP_ID"
};

// Initialize Firebase
firebase.initializeApp(firebaseConfig);
const auth = firebase.auth();
```

## Step 5: Implement Authentication Logic
Create a file `script.js` and add authentication functions:

```javascript
function signup() {
    let email = document.getElementById("email").value;
    let password = document.getElementById("password").value;
    auth.createUserWithEmailAndPassword(email, password)
        .then((userCredential) => alert("User Signed Up"))
        .catch(error => alert(error.message));
}

function login() {
    let email = document.getElementById("email").value;
    let password = document.getElementById("password").value;
    auth.signInWithEmailAndPassword(email, password)
        .then((userCredential) => alert("User Logged In"))
        .catch(error => alert(error.message));
}

function logout() {
    auth.signOut().then(() => alert("User Logged Out"));
}
```

## Step 6: Deploy the Website Using Firebase Hosting
1. Install Firebase CLI:
   ```sh
   npm install -g firebase-tools
   ```
2. Log in to Firebase:
   ```sh
   firebase login
   ```
3. Initialize Firebase in your project:
   ```sh
   firebase init
   ```
4. Select **Hosting** and follow the prompts.
5. Deploy the project:
   ```sh
   firebase deploy
   ```

## Firebase Hosting Configuration
Create `firebase.json` for Firebase Hosting:

```json
{
    "hosting": {
        "public": ".",
        "ignore": [
            "firebase.json",
            "**/.*",
            "**/node_modules/**"
        ]
    }
}
```

## Conclusion
You have now successfully created a basic Firebase-integrated website with authentication. You can enhance it by adding Firestore for database storage and better UI styling. 🚀
