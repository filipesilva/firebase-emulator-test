# firebase-emulator

Sample repo to test using the [Firebase emulators](https://github.com/firebase/firebase-tools#deployment-and-local-emulation).

## Setup

- install [node](https://nodejs.org/en/), [yarn](https://yarnpkg.com/lang/en/docs/install/), [java hotspot](https://adoptopenjdk.net/)
- `yarn`
- `yarn firebase init`
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
- `yarn start`