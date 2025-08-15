────────────────────────────────
BACKEND README 
────────────────────────────────

# PulseVote API (Express + MongoDB + JWT)

**Video demo:** 
(https://youtu.be/Tv-hmkZs-GU?si=9hV0Ca34QMUJhsVC)

## What this is
Secure REST API that handles **register**, **login**, and a **JWT‑protected** example route.

## Features
- Register & Login (email + password)
- Issues JWT on success
- Protected route example: `/api/protected`
- CORS configured for the React frontend
- HTTPS in development (self‑signed certs)

## Quick start
```bash
npm install
npx nodemon server.js
# API runs at: https://localhost:5000
# (Open that URL once and accept the browser warning for the self-signed cert)
```

## .env (create in backend root)
```
PORT=5000
MONGO_URI=<your_mongodb_connection_string>
JWT_SECRET=<long_random_secret>
# Allow your Vite origins (Vite may use 5173 or 5174)
CORS_ORIGIN=https://localhost:5173,https://localhost:5174
```

## Endpoints
```
POST /api/auth/register  { email, password }  -> { token }
POST /api/auth/login     { email, password }  -> { token }
GET  /api/protected      Authorization: Bearer <token>  -> JSON
```

## The token (simple explanation)
- After register/login the API returns a **JWT**: `{ "token": "..." }`.
- The client must send it on protected requests: `Authorization: Bearer <token>`.
- The token proves who you are; it **expires** based on server settings (you can adjust this in code).
- Keep the secret (`JWT_SECRET`) safe. Never commit your real `.env`.

## Notes
- Don’t commit `.env` or `ssl/` (dev certificates).
- If you see CORS errors, make sure `CORS_ORIGIN` matches your frontend URL exactly.
