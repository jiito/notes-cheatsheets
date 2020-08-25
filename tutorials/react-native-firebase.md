# React Native Firebase

## Ben Allan-Rahill

## Configuration

1. Install expo cli
   1. `npm install -g expo-cli`
2. Add Config file 1.

   ```js
   import \* as firebase from 'firebase';
   import '@firebase/auth';
   import '@firebase/firestore';

   const firebaseConfig = {
   apiKey: 'YOUR_KEY_HERE_AIzaSyAOWH',
   authDomain: 'your-auth-domain-b1234.firebaseapp.com',
   databaseURL: 'https://your-database-name.firebaseio.com',
   projectId: 'your-project-id-1234',
   storageBucket: 'your-project-id-1234.appspot.com',
   messagingSenderId: '12345-insert-yourse',
   appId: 'insert yours: 1:1234:web:ee873bd1234c0deb7eba61ce',
   };

   if (!firebase.apps.length) {
   firebase.initializeApp(firebaseConfig);
   }

   export { firebase };
   ```
