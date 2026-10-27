# StreamForge Live — starter MVP

A runnable starter for a dark streaming dashboard, API, persistent FFmpeg loop worker, Docker development stack, and Android Kotlin scaffold.

## What works in this starter
- Responsive dashboard UI with destination cards, playlist controls, status panels, and demo state.
- Express API with health, destination CRUD, playlist CRUD, and broadcast start/stop endpoints.
- SQLite-backed persistence for local development.
- FFmpeg worker process manager for looping a local prerecorded file to an RTMP/RTMPS destination.
- Stream-key encryption-at-rest using AES-256-GCM when `CREDENTIAL_ENCRYPTION_KEY` is configured.
- Docker Compose stack for API, Redis, and RTMP worker environment.
- Android app scaffold that opens the StreamForge dashboard in a WebView.

## Not yet production-ready
Official YouTube/Facebook/Instagram/TikTok/Moj OAuth/API integrations, account eligibility checks, multi-tenant hardening, billing, push notifications, production KMS, monitoring, and complete Android native controls are not implemented. The UI must not be treated as proof a social platform is live. Test with a private RTMP receiver first.

## Requirements
- Node.js 20+
- FFmpeg installed and available as `ffmpeg`
- Android Studio for the Android scaffold
- Docker Compose (optional)

## Run locally
```bash
cd server
cp .env.example .env
npm install
npm run dev
```
Open `web/index.html` directly for the static dashboard preview, or serve `web/` with any static file server. API default: `http://localhost:4100`.

For API-backed dashboard, serve the web folder and set `window.STREAMFORGE_API_URL` to the API origin before loading `app.js` (or edit the constant near the top of `app.js`).

## Configure a loop
1. Place an authorized test video at a path accessible to the API/worker, e.g. `./media/demo.mp4`.
2. Add a destination using an RTMP/RTMPS server URL and stream key.
3. Call `POST /api/broadcasts/start` with `{ "mediaPath": "/absolute/path/demo.mp4", "destinationId": "..." }`.
4. Stop with `POST /api/broadcasts/:id/stop`.

Never put a real stream key in source code, screenshots, query strings, or logs. Use a private/unlisted test stream first.

## Docker
```bash
cp server/.env.example server/.env
# Set a strong CREDENTIAL_ENCRYPTION_KEY (32 bytes, base64) before using real keys.
docker compose up --build
```
The worker requires a mounted media directory and outbound access to your authorized RTMP endpoint. Production continuous streaming needs a persistent compute service that permits long-running FFmpeg processes and adequate bandwidth.
