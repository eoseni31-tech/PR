# Private couple ledger

This is one of two separate Node/Express services. Upload all files inside this folder to its corresponding GitHub repository. Keep the repositories separate. No nested folders or standalone index.html are needed: server.js serves the page, styles, media and backend.

## Render deployment

Guest service: gu-adh5.onrender.com. Couple service: cp-247k.onrender.com.
Build command: npm ci && npm run build
Start command: npm start
Node: 24.x
Use a Web Service, not a static site. Keep existing Turso settings. Render's RENDER_EXTERNAL_URL is recognised automatically; APP_ORIGIN, if set, must match that service's exact https address without a trailing slash.

For Vercel: Express framework, npm run build, repository root, no Output Directory override.

## Required database settings in BOTH services

TURSO_DATABASE_URL=libsql://safiyahs-weddings-ella3638.aws-ap-south-1.turso.io
TURSO_AUTH_TOKEN=<your private database token>

Both services must point to the SAME database. Never put the token in GitHub or frontend code. Sign in to the couple site once to prepare its wedding record. Missing SGW tables/indexes are created additively; existing wedding ownership and guest records are preserved. The authorised test account uses the supplied email and password hash and is prepared once per database; cold starts do not reset a subsequently changed password. Change password is available inside the ledger.

## RSVP and gifts

Ordinary guest links work without personalised tokens. The server chooses PUBLIC_WEDDING_SLUG (default chioma-henry), preventing callers from selecting another wedding. PUBLIC_MAX_GUESTS defaults to 1 and accepts 1–20. Personal invitation links still work; set GUEST_SITE_ORIGIN=https://gu-adh5.onrender.com in the couple service to create them.

A browser cookie restores a guest's identity and repeat RSVPs update that browser's record. Different devices can create duplicate entries. Gifts/reservations are saved to the same database and the protected couple ledger checks for updates every two seconds while visible. Success appears only after database writes complete. No network or host can guarantee instant responses.

## Paystack payment link only — no Paystack API keys required

The payment link https://paystack.shop/pay/bgtkmsmy8c is retained for monetary gifts and contributions towards registry items. Paystack collects and confirms payment in its own dashboard. This application does not request Paystack API keys, initialise payments through the API, receive payment webhooks, or automatically import Paystack transactions.

Guest RSVP submissions, gift reservations and gift notifications still save to Turso and appear in the private couple ledger. A gift notification remains labelled unverified because it is a guest report; this does not mean Paystack has failed to confirm the actual payment. Opening the payment link is not proof of payment, and the application does not claim that money has been received.

The original payment page displays Wedding by HealthAura Skin. Verify its destination bank/subaccount in your own Paystack dashboard. Payments do not order physical items or arrange delivery. No database tables or existing payment records are deleted by removing this integration.

## Verified scope and limits

npm run build and npm test exercise server syntax and HTTP/SQL security, storage, isolation against isolated test storage. They do not charge money or contact your remote Turso. GET /api/health on the guest service checks its database connection without returning records.

Existing guest CSS/media are preserved, with functional gift controls added. Original sample bank/venue data remain samples. Photo uploads, livestream, asoebi contacts and logistics remain unconfigured. Payout routing and the latest deployment still need live verification after configuration.
