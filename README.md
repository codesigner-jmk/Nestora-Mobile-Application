# NESTORA Android application

The NESTORA Android app is a native Expo and React Native client. It shares the existing NESTORA Supabase backend, customer accounts, products, wishlist, cart, checkout, and orders with the storefront.

## Requirements

- Node.js 22.13 or newer
- pnpm
- An Expo account for EAS APK builds
- The NESTORA Supabase project URL and publishable key

## Local setup

1. Copy `.env.example` to `.env.local`.
2. Set `EXPO_PUBLIC_SUPABASE_URL`, `EXPO_PUBLIC_SUPABASE_PUBLISHABLE_KEY`, and `EXPO_PUBLIC_SITE_URL` in `.env.local`. Use the deployed NESTORA website origin for `EXPO_PUBLIC_SITE_URL`.
3. Install dependencies and check types:

   ```powershell
   pnpm install
   pnpm typecheck
   ```

4. Start Expo:

   ```powershell
   pnpm start
   ```

## Build an installable APK

Sign in to EAS, configure the same three public environment variables for the production EAS environment, then build:

```powershell
pnpm dlx eas-cli@latest login
pnpm build:apk
```

The `production` profile in `eas.json` creates an internal-distribution Android APK. Keep and reuse the existing Android keystore for updates to the installed app.

## Backend and OAuth setup

- Use the existing NESTORA Supabase project. Do not create a mobile-only backend or include service-role, database, Resend, or OAuth client secrets in this repository or APK.
- Apply the storefront's Supabase migrations, including `202610050007_mobile_shared_cart.sql`, before using the shared cart features.
- Add `nestora://auth/callback` to the allowed Supabase Auth redirect URLs and use the existing Google provider configuration.
- Website-side checkout and order-confirmation email handling remains in the storefront repository.

For the implementation details and current boundaries, see [SETUP.md](./SETUP.md).
