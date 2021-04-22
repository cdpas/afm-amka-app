# App to have AFM and AMKA ready on the phone

This is a Vue-Cordova android app that allows to add/remove and display the AFM and AMKA easily. 

The App consists of Home and Settings.
In Home all data is displayed in tabs, in case more data is added.
It is possible to add data in Settings and all data is stored in localStorage.

## Project setup
```
npm install
```

### Run the project in Vue
```
npm run serve
```

### Run on Android
```
npm run cordova-prepare 
cd src-cordova
cordova run android
```