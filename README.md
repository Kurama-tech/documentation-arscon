# Application Architecture & Documentation

## Overview

Your application consists of:

- **Flutter Mobile App** (Riverpod state management, Firebase Phone Authentication, Mapbox integration)
- **Golang Backend API** (MongoDB, AWS S3 image uploads)
- **Nuxt.js Admin Dashboard** (Auth0 machine-to-machine authentication)
- **Flask ML API** (Daily updated recommendation engine)
- **Google Cloud Function** (Gemini AI chat integration)

## High level architecture Diagram

```
Flutter App
|
|- Firebase Phone Authentication
|- Mapbox Maps
|- Google Cloud Function (Gemini AI)
|- Golang API -> MongoDB
|             -> AWS S3 (Images)
|
|- Flask ML API -> MongoDB

Nuxt.js Dashboard
    -> Auth0 (Machine-to-Machine)
```

## Flutter App Setup

### Firebase Phone Auth Setup

1. Create Firebase project.
2. Enable Phone Authentication.
3. Register Flutter app (Android/iOS) in Firebase.
4. Add `google-services.json` (Android) and `GoogleService-Info.plist` (iOS).
5. Configure SHA-1 and SHA-256 keys in Firebase for phone authentication.

### Mapbox Setup

1. Get Mapbox API Key.
2. Configure key in Flutter.

### Generating Signed APK (refer flutter docs)

```
flutter build apk --release
```

## Backend API (Golang)

### Environment Variables (`.env` file)

```
MINIO_KEY="AWS_ACCESS_KEY"
MINIO_SECRET="AWS_SECRET_KEY"
MINIO_URL="s3.amazonaws.com"
MONGO_URL="mongodb://username:password@host:port/dbname"
```

### Running API

```
source .env
go mod download
go run main.go
```

### Google Cloud Service Account

- Set up for Firebase Admin SDK.
- Provide JSON credentials to Golang backend.
- place your service-account.json in root

## Flask ML API

### Setup

```
MONGO_URL="mongodb://username:password@host:port/dbname"
pip install -r requirements.txt
python app.py
```

### Scheduled Training

Automate daily training via cron job.

## Nuxt.js Dashboard

### Auth0 Setup (`nuxt.config.js`)

```js
auth: {
  strategies: {
    auth0: {
      domain: '<AUTH0_DOMAIN>',
      clientId: '<AUTH0_CLIENT_ID>',
      audience: 'https://dumdum-api.msawood.com',
      scope: ['openid', 'profile', 'email', 'roles', 'permissions'],
      endpoints: {
        authorization: 'https://<AUTH0_DOMAIN>/authorize',
        userInfo: 'https://<AUTH0_DOMAIN>/userinfo',
        token: 'https://<AUTH0_DOMAIN>/oauth/token'
      }
    }
  },
  redirect: {
    login: '/login',
    logout: '/',
    callback: '/callback',
    home: '/'
  }
}
```

### Run Dashboard

```
npm install / yarn
npm run dev
```

## Features

- Phone Authentication
- Posts & interactions (business/individual)
- Profile management
- Requirement postings
- Dark Mode
- AI Chat (Gemini API)
- Daily Recommendation updates
- Admin: subscriptions, verifications, maintenance mode

