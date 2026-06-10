# Cyber X — Official Website

**The official bilingual website and content platform for the Cyber X cybersecurity team.**

[![Live Site](https://img.shields.io/badge/Live-cyberxsec.me-purple?style=flat-square)](https://cyberxsec.me)
[![Original Repo](https://img.shields.io/badge/Original-CyberX--sec-blue?style=flat-square)](https://github.com/CyberX-sec/Web)

> **الصوت الذي يُرَى** — *A sound unveiled to the eyes*

---

## About

[Cyber X](https://cyberxsec.me) is a student cybersecurity team from **Cybersecurity Engineering, Northern Technical University** (الجامعة التقنية الشمالية). This repository contains the full-stack website used to publish projects, articles, lectures, team profiles, and services — with a built-in admin panel for content management.

Seven students. One mission: **to be a force of knowledge**.

---

## Features

### Public site
- Bilingual UI (Arabic / English) with dynamic content loading
- **Projects** — showcase cybersecurity tools and demos (e.g. NoPulse-HUB, WiFi Diagnoser)
- **Articles** — technical write-ups and research
- **Lectures** — educational content organized by channels
- **Services** — team offerings
- **Team profiles** — member bios, badges, certificates
- Rich detail pages with video embeds, image galleries, and collaborators

### Admin panel (`/admin`)
- Session-based authentication with role-based access
- CRUD for projects, articles, lectures, channels, and team profiles
- Media uploads with organized folder storage
- Site-wide branding settings (hero image, homepage copy, section order)
- Activity log for admin actions
- User management (super-admin, admin, editor roles)

### API backend
- Express.js REST API with SQLite database
- Serves static frontend + `/media` uploads
- Public read endpoints and protected admin routes

---

## Tech stack

| Layer | Technology |
|---|---|
| Frontend | HTML, CSS, JavaScript (vanilla) |
| Backend | Node.js, Express 5 |
| Database | SQLite (`sqlite3`) |
| Auth | `express-session`, `bcrypt` |
| Uploads | `multer` |
| Dev | `nodemon` |

---

## Project structure

```
Web/
├── index.html              # Homepage
├── Projects/               # Project listing & detail pages
├── Articles/               # Article listing & detail pages
├── Lectures/               # Lecture channels & detail pages
├── Services/               # Services pages
├── Team/                   # Team member profiles
├── Templates/              # Shared CSS, JS, API client
├── admin/                  # Admin dashboard UI
├── media/uploads/          # Uploaded images & files
├── Mainimages/             # Static branding assets
├── server/
│   ├── src/
│   │   ├── server.js       # Express app entry point
│   │   ├── routes/
│   │   │   ├── public.js   # Public API (/api/*)
│   │   │   └── admin.js    # Admin API (/api/admin/*)
│   │   ├── middleware/
│   │   │   └── auth.js     # Session & role guards
│   │   └── db/             # SQLite init & queries
│   └── package.json
└── README.md
```

---

## Quick start

### Prerequisites
- **Node.js** 18+
- **npm**

### 1. Install dependencies

```bash
cd server
npm install
```

### 2. Configure environment

```bash
cp .env.example .env
```

Edit `.env` with your values (see [Environment variables](#environment-variables) below).

### 3. Run the server

```bash
# Development (auto-reload)
npm run dev

# Production
npm start
```

The site is served at **http://localhost:3001** by default.

### 4. Admin login

Open [http://localhost:3001/admin](http://localhost:3001/admin) and sign in with the credentials set in your `.env` file (`DEFAULT_ADMIN_EMAIL` / `DEFAULT_ADMIN_PASSWORD`). The default admin account is created on first run.

---

## Environment variables

| Variable | Default | Description |
|---|---|---|
| `PORT` | `3001` | Server port |
| `SESSION_SECRET` | `dev-secret-change-me` | Session encryption key — **change in production** |
| `DEFAULT_ADMIN_EMAIL` | — | Initial admin email (created on first boot) |
| `DEFAULT_ADMIN_PASSWORD` | — | Initial admin password |
| `DEFAULT_ADMIN_DISPLAY_NAME` | — | Admin display name |
| `PUBLIC_ROOT` | repo root | Path to static frontend files |
| `MEDIA_ROOT` | `media/` | Uploaded media directory |
| `UPLOAD_ROOT` | `media/uploads` | Multer upload destination |
| `CORS_ORIGIN` | — | Comma-separated allowed origins |
| `TRUST_PROXY` | — | Set `true` behind reverse proxy |
| `COOKIE_SECURE` | — | Set `true` for HTTPS-only cookies |
| `COOKIE_SAMESITE` | `lax` | Cookie SameSite policy |

---

## API overview

### Public (`/api`)

| Method | Endpoint | Description |
|---|---|---|
| GET | `/api/health` | Health check |
| GET | `/api/projects` | List published projects |
| GET | `/api/projects/:slug` | Project detail |
| GET | `/api/articles` | List published articles |
| GET | `/api/articles/:slug` | Article detail |
| GET | `/api/lectures` | List lectures |
| GET | `/api/lectures/:id` | Lecture detail |
| GET | `/api/channels` | List lecture channels |
| GET | `/api/channels/:slug` | Channel with lectures |
| GET | `/api/team` | Team profiles |
| GET | `/api/team/:slug` | Single profile |
| GET | `/api/site-settings` | Homepage branding |

### Admin (`/api/admin`) — authenticated

| Method | Endpoint | Roles | Description |
|---|---|---|---|
| POST | `/auth/login` | — | Login |
| POST | `/auth/logout` | — | Logout |
| GET | `/auth/me` | any | Current user |
| POST | `/uploads` | editor+ | Upload media |
| POST/PUT/DELETE | `/projects` | editor+ | Manage projects |
| POST/PUT/DELETE | `/articles` | editor+ | Manage articles |
| POST/PUT/DELETE | `/lectures` | admin+ | Manage lectures |
| POST/PUT/DELETE | `/channels` | admin+ | Manage channels |
| GET/PUT | `/site-settings` | super-admin | Site branding |
| GET/POST/PUT/DELETE | `/users` | super-admin | User management |

---

## Deployment

The live site runs at **[cyberxsec.me](https://cyberxsec.me)**. For production:

1. Set strong `SESSION_SECRET` and admin credentials
2. Enable `COOKIE_SECURE=true` and `TRUST_PROXY=true` behind HTTPS
3. Point `PUBLIC_ROOT` and `MEDIA_ROOT` to persistent volumes
4. Run with a process manager (PM2, systemd) or container
5. Back up `server/data/*.db` regularly

---

## Contributors

Built by the **Cyber X** team. This mirror is maintained by [Van De Cipher](https://github.com/vancipher) as a contributor to the original project.

- **Original repository:** [CyberX-sec/Web](https://github.com/CyberX-sec/Web)
- **Live website:** [cyberxsec.me](https://cyberxsec.me)
- **Team:** Northern Technical University · Cybersecurity Engineering

---

## License

**Van Cipher Restricted License v1.0** — see [LICENSE](LICENSE).

Cyber X team website — **all rights reserved**. You may read this repo for learning. **Hosting, forking for use, or reusing this codebase requires written permission** from [Abdullah Y. Habash (@vancipher)](https://github.com/vancipher) / [Cyber X](https://cyberxsec.me).

---

<p align="center">
  <strong>CYBER X</strong><br>
  <em>To be a force of knowledge</em>
</p>
