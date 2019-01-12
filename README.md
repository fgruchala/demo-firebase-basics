# Demo / Basics // Firebase 🔥
## Branches

**master** contains the solutions, that is to say, with implementation of Firebase.

**no-firebase-land** is to implement by your own.

## Prerequisites
### On the cloud side
* Go to the Firebase console https://console.firebase.google.com/
* Create a new project
* Copy the configuration via "Home > Add a new application"

### On the code side
Once you have cloned this repo, you can :

* Install globally the tooling

```
$ npm install -g firebase-tools
```

* Install all local dependencies

```
$ npm install
```

* Create a file .env.local with this content

```
VUE_APP_FIREBASE_API_KEY=<COPIED_CONFIGURATION>
VUE_APP_FIREBASE_AUTH_DOMAIN=<COPIED_CONFIGURATION>
VUE_APP_FIREBASE_PROJECT_ID=<COPIED_CONFIGURATION>
```

### Finally
Play with it :

```
$ npm run serve
```

## What's in the box ?????
### Authentification
In this part, you will see :
* How to create a new account
* How to sign in with it
* How to sign in with Google SSO
* How to sign out

### Persistence
In this part, you will see :
* How to create a new Firestore DB
* How to add new document on it
* How to get datas from it and in realtime

### Deployment
In this part, you will see :
* How to deploy your site

# Contact via [Issues](https://github.com/fgruchala/demo-firebase-basics/issues)
Helpful for **question**, **bug** and **contribution request**.

