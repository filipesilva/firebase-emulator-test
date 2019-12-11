# firebase-emulator-test

Sample repo to test using the [Firebase emulators](https://github.com/firebase/firebase-tools#deployment-and-local-emulation).

This doesn't seem to be a public API for web clients.

## Testing the web api

- install [node](https://nodejs.org/en/), [yarn](https://yarnpkg.com/lang/en/docs/install/), [java hotspot](https://adoptopenjdk.net/)
- see `public/index.html` for script source code
- run `yarn emulators`
- open http://localhost:5000, see the console logs for added documents
- set `var useEmulators = false` in index and reload, you should see errors that shows now you're trying to connect to the real database but don't have permissions.
- restore the `var useEmulators = true`, see the documents again
- stop the `yarn emulators` process, start it again, see the db was reset

## Setup outside this repo

You don't need to do this setup when using this demo repository. 

These are the steps that I used to make this repo and the project/db that I use in the demo above.

- `npm install -g firebase-tools`
- `firebase init`
- choose to setup all features
- create a project called `emulator-test`
- use defaults for all questions unless you want something specific
- chose to setup and download all emulators
- if you see `Error: Cloud resource location is not set for this project but the operation you are attempting to perform in Cloud Firestore requires it.`, do this:
  - go to https://console.firebase.google.com/
  - open your project
  - click on cogwheel icon on the left -> project settings
  - click to edit `Google Cloud Platform (GCP) resource location`
  - choose a cloud resource location
  - run `yarn firebase init` again but this time choose an existing project
- go to https://console.firebase.google.com/, click on the `web` icon to add a web client
- add a firestore database with the following security rules to deny all:
```js
rules_version = '2';
// Deny read/write access to all users under any conditions
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if false;
    }
  }
}
```
- add a realtime database with the following rules to deny all:
```json
{
  /* Visit https://firebase.google.com/docs/database/security to learn more about security rules. */
  "rules": {
    ".read": false,
    ".write": false
  }
}
```
- replace `public/index.html` with your own