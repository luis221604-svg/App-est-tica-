# App-est-tica-
App Fidelis 
npm install -g firebase-tools
firebase --version
firebase login
firebase init functions
functions/
 ├── index.js
 ├── package.json
 const functions = require("firebase-functions");

exports.helloWorld = functions.https.onRequest((req, res) => {
  res.send("🔥 Cloud Function funcionando!");
});
firebase deploy --only functions
Function URL: https://...
firebase functions:log
