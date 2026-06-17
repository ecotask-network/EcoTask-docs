# Mobile App Setup Guide

## Prerequisites
- Node.js 18+
- React Native CLI
- Android Studio (for Android) or Xcode (for iOS)
- Physical device or emulator

## Installation
```bash
git clone https://github.com/ecotask-network/ecotask-app.git
cd ecotask-app
cp .env.example .env
npm install
```

### iOS (Mac only)
```bash
cd ios && pod install && cd ..
npm run ios
```

### Android
```bash
npm run android
```

## Environment Variables
See `.env.example` for all required variables.

## Verification
- Metro bundler starts without errors
- App renders Home screen with impact stats
- Wallet connect button appears
- Tasks tab shows sample data
