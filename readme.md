# DROELOE - Roadside Flowers

![DROELOE - Roadside Flowers postcard](https://storage.googleapis.com/nielskersic/static-images/github/roadsideflowers-example-horizontal.jpg)

This is an adapted showcase version of an application developed by me, Niels Kersic, for the record label [bitbird](https://bitbirdofficial.com/) and artist [DROELOE](https://www.instagram.com/droeloemusic/).
The purpose of this application was for people to presave DROELOE's new track 'Roadside Flowers', one of the singles of their (then) upcoming Anthology Album '[A Matter of Perspective](https://bitbird.lnk.to/amatterofperspective)'.

---
## The premise
'Roadside Flowers' is themed around a roadside gas station with a view of a field full of beautiful flowers. The idea of sending a postcard to a loved one fit well with the message of the actual song. The presave application allows people to write a message to anyone. It then generates a postcard with the person's message, which they can download after presaving the song on either Spotify or Apple Music.

![DROELOE - Roadside Flowers gas station](https://storage.googleapis.com/nielskersic/static-images/github/roadsideflowers-presave-cover.jpg)

## How it's made
### Frontend
The frontend is an Angular 9 app. This app consists of just two routes. The main route is where users leave their messafe and select a presave option (Spotify or Apple Music). The second route is where people land after completing the save. This is where they can download their generated postcards and share them to social media. The frontend makes use of Apple's MusicKitJS, as this is required to enable login with Apple Music.

### Backend
The backend is a NodeJS Express application. This is where most of the interactions with the Spotify Web API and Apple Music API take place. The backend is also where tickets are generated using the [canvas package](https://www.npmjs.com/package/canvas). The canvas consists of a static background image onto which the user's text is added. The canvas is then written to a JPG file to be stored on Google Cloud Storage for retrieval by the user.

### Infrastructure
- Frontend is hosted using Firebase Hosting
- Data is stored in Firestore (only in the original version)
- API is deployed on Google Cloud Run (to keep costs low and to scale with demand) 

## What's different in this version
- The original application would store Spotify and Apple Music tokens in Firestore. On release day, these tokens were used to save the track to the user's libraries. No data is stored in Firestore for the showcase version. The track is instantly saved to the user's library instead.
- To keep accurate metrics of presaves, Firestore Cloud Functions would fire on each new document add or remove.
- The original implemented both Google Analytics and Facebook Pixel to track events for marketing purposes. These were removed for the showcase version.
- In the original ticket generator, the code at the bottom would auto-increment with each presave. Since presaves are not stored and such a counter is not kept, a random number is generated instead. 

## What could be improved
- TESTS! The original application was developed under a very tight deadline, so no tests were written.
- Cleaner code. This presave app was adapted from an earlier presave campaign. This saved a lot of time implementing elements like the Spotify and Apple Music login, but it also lead to some unused code remaining in the app.
- Moving the Spotify OAuth flow to a pop-up. This would prevent having to pass around the unique ID for each presave (used for the user-generated tickets) in the URL.
- Small UI improvements and bug fixes.
