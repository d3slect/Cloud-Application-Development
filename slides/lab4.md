
<!--title: Firebase-->
<!-- content_class: smaller -->

<center>
<!-- ![Firebase](images/firebase-logo.png) -->
<!--<img src="images/firebase-logo.png" alt="Firebase logo" style="width: 250px; margin-top: 60px;"/>-->
<img src="images/firebase-logo_new.png" alt="Firebase logo" style="margin-top: 75px;"/>
</center>

---

title: Firebase overview I
content_class: smaller

- Backend as a service (BaaS)

- Products to develop & test your app
    - **Real-time database** (backend for your app)
    - Authentication
    - Cloud Storage
    - Hosting
    - ...    
- Products to "grow & engage your audience"
    - Google Analytics
    - Dynamic Links
    - Remote Config
    - AdWords
    - ...
- Tight integration with Google Cloud Platform
    
---

title: Firebase overview II
content_class: smaller

- Apps can run on client-side code only 

- Platforms:
    - iOS
    - Android
    - Web
    - Games
        - C++ on iOS and Android
        - Unity game engine

---

title: Firebase Database I
content_class: smaller

- NoSQL data-store
- Returns JSON from a RESTful API

<center>
<img src="images/firebase_realtime-api.png" alt="Firebase realtime api" style="width: 600px;"/>
</center>

---

title: Firebase Database II
content_class: smaller

- Whenever **data is updated in Firebase**, it sends the update down to every **listening client**

<center>
<img src="images/firebase_realtime-sync-anim.gif" alt="Firebase realtime sync" style="width: 750px;"/>
</center>

---

title: Firebase Database III
content_class: smaller

- Offline
    - SDK persists data to disk
    - Data synchronized after re-connection

- Single JSON tree
    - Database denormalization

---

title: Firebase application (demo)
content_class: smaller

- Based on [Firebase Web Codelab](https://codelabs.developers.google.com/codelabs/firebase-web)    
    
---

title: Cloud Functions for Firebase
content_class: smaller

- "Glue" (connective layer) to connect cloud services
    - Not just FireBase
    - Executed on the server, not visible by clients
- JavaScript code, executes in Node.js environment
- Billed to the nearest 100ms

<center>
<img src="images/connect-extend.png" alt="Cloud services connection" />
</center> 

---

title: Firebase Cloud Functions for Firebase (demo)
content_class: smaller

- Based on [Cloud Functions for Firebase codelab](https://codelabs.developers.google.com/codelabs/firebase-cloud-functions)

---

title: Additional topics and resources
content_class: smaller

- [Architecting for Data Contention in a Realtime World with Firebase (Google I/O '17)](https://www.youtube.com/watch?v=eWj6dxfN63g)
- [How to structure data](https://firebase.google.com/docs/database/web/structure-data)
- [Enabling offline capabilities in JS](https://firebase.google.com/docs/database/web/offline-capabilities)

- [Intro to Firebase](https://github.com/firebase/firebase-intro-presentation)