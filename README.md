# App-est-tica-
App Fidelis 
meu-backend-firebase/
 ├── .gitignore
 ├── firebase.json
 ├── package.json
 └── functions/
     ├── index.js
     ├── package.json
     └── .gitignore
node_modules/
.firebase/
.env
{
  "functions": {
    "source": "functions"
  }
}
{
  "name": "backend-firebase",
  "private": true
}
node_modules/
.env
{
  "name": "functions",
  "description": "Firebase Cloud Functions",
  "engines": {
    "node": "18"
  },
  "main": "index.js",
  "scripts": {
    "serve": "firebase emulators:start --only functions",
    "deploy": "firebase deploy --only functions",
    "logs": "firebase functions:log"
  },
  "dependencies": {
    "firebase-admin": "^12.0.0",
    "firebase-functions": "^5.0.0"
  }
}
const functions = require("firebase-functions");
const admin = require("firebase-admin");

admin.initializeApp();

/**
 * Function HTTP simples para teste
 * URL será gerada no deploy
 */
exports.helloWorld = functions.https.onRequest((req, res) => {
  res.status(200).json({
    message: "🔥 Cloud Function funcionando!",
    timestamp: new Date().toISOString()
  });
});

/**
 * Exemplo de Function que grava no Firestore
 */
exports.createLog = functions.https.onRequest(async (req, res) => {
  try {
    const data = {
      message: req.body.message || "Log sem mensagem",
      createdAt: admin.firestore.FieldValue.serverTimestamp()
    };

    await admin.firestore().collection("logs").add(data);

    res.status(201).json({
      success: true,
      data
    });
  } catch (error) {
    res.status(500).json({
      success: false,
      error: error.message
    });
  }
