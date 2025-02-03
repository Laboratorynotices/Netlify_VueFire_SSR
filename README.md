# Nuxt 3 VueFire SSR + Netlify Experiment

## Overview

This project is an experiment to investigate issues encountered when setting up a Nuxt 3 application with VueFire while enabling Server-Side Rendering (SSR) in Netlify. The goal is to identify the root cause of potential problems and find a working solution.

## Expected Challenges

- Deployment issues specific to Netlify.

## Experiment Steps

### 1. Update Package Manager and Dependencies

Ensure you have the latest versions of npm and nuxi installed:

```bash
sudo npm install -g npm@latest nuxi@latest
```

### 2. [Initialize Nuxt 3 Project](https://github.com/Laboratorynotices/Netlify_VueFire_SSR/tree/f7b7472e5fce4fcfad22c4e1642aa0a157b7d09e)

```bash
npx nuxi init . --package-manager npm --force --no-telemetry --no-git-init
```

### 3. Deploy the Project to Netlify

Follow the official Netlify guide: [Getting Started with Netlify](https://docs.netlify.com/get-started/).

### 4. [Enable SSR](https://github.com/Laboratorynotices/Netlify_VueFire_SSR/tree/bff592c73e5c1bf9ab2f6ad4e048c7bf4ee46684)

Modify `nuxt.config.ts` to enable SSR:

```typescript
export default defineNuxtConfig({
  ssr: true,
  // Other configuration options...
});
```

### 5. [First SSR Request](https://github.com/Laboratorynotices/Netlify_VueFire_SSR/tree/421f00dac2c7eafcc5faf43a67e88f9d9c123419)

Create the file `server/api/hello.ts`:

```typescript
export default defineEventHandler((event) => {
  return {
    hello: "world",
  };
});
```

In `app.vue`, add the following code to fetch and display the data:

```html
<script setup lang="ts">
  const { data } = await useFetch("/api/hello");
</script>

<template>
  <pre>{{ data }}</pre>
</template>
```

### 6. Firebase Admin SDK Setup

- Download the secret key from [Firebase Console](https://console.firebase.google.com/).
- Rename the downloaded file to `service-account.json` and place it in the project root.
- Add `service-account.json` to `.gitignore` to prevent accidental commits.

### 9. Install VueFire

Install necessary dependencies:

```bash
npm install firebase
npx nuxi@latest module add vuefire
npm install firebase-admin firebase-functions @firebase/app-types
```

### 10. Configure VueFire

Update `nuxt.config.ts`:

```typescript
export default defineNuxtConfig({
  vuefire: {
    config: {
      apiKey: process.env.GOOGLE_FIREBASE_CONFIG_API_KEY,
      authDomain: process.env.GOOGLE_FIREBASE_CONFIG_AUTH_DOMAIN,
      projectId: process.env.GOOGLE_FIREBASE_CONFIG_PROJECT_ID,
      appId: process.env.GOOGLE_FIREBASE_CONFIG_APP_ID,
    },
  },
  // Other configuration options...
});
```

Add Firebase credentials to the `.env` file:

```
GOOGLE_FIREBASE_CONFIG_API_KEY="..."
GOOGLE_FIREBASE_CONFIG_AUTH_DOMAIN="....firebaseapp.com"
GOOGLE_FIREBASE_CONFIG_PROJECT_ID="..."
GOOGLE_FIREBASE_CONFIG_APP_ID="..."
GOOGLE_APPLICATION_CREDENTIALS=/service-account.json
```

## Result

??? We will see it...
