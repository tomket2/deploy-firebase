# Deploy to Firebase Hosting using target name

A GitHub Action to deploy to Firebase Hosting using target name

- You can choose a specific branch to allow deployment by using the `TARGET_BRANCH` env var (`master` if not specified).
- Make sure you have the `firebase.json` file in the repository
- Get the Firebase token by running `firebase login:ci` and [store it](https://help.github.com/en/actions/configuring-and-managing-workflows/creating-and-storing-encrypted-secrets) as the `FIREBASE_TOKEN` secret
- Set the project id in the `FIREBASE_PROJECT` env var
- Set the [target](https://firebase.google.com/docs/cli/targets) name in the `TARGET_NAME` env var (It will deploy to all targets if `TARGET_NAME` is not specified)

Example workflow

```
name: Build and Deploy
on:
  push:
    branches:
    - main
jobs:
  main:
    name: Build and Deploy
    runs-on: ubuntu-latest
    steps:
    - name: Check out code
      uses: actions/checkout@master
    - name: Build Hugo
      uses: lowply/build-hugo@v0.68.3
    - name: Deploy to Firebase
      uses: lowply/deploy-firebase@v0.0.3
      env:
        FIREBASE_TOKEN: ${{ secrets.FIREBASE_TOKEN }}
        FIREBASE_PROJECT: name-of-the-project
        TARGET_BRANCH: main
        TARGET_NAME: develop 
```
