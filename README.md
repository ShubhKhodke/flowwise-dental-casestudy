# Flowwise Dental 🦷

> A modern, multi-tenant dental clinic management system built with TypeScript, Next.js, and Express.

[![TypeScript](https://img.shields.io/badge/TypeScript-5.x-blue.svg)](https://www.typescriptlang.org/)
[![Next.js](https://img.shields.io/badge/Next.js-14+-black.svg)](https://nextjs.org/)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)

## 📋 Overview

Dental CRM is a comprehensive practice management solution designed specifically for dental clinics. It provides patient management, appointment scheduling, treatment tracking, billing, and reporting in a mobile-first, user-friendly interface.

### Key Features

- ✅ **Patient Management** - Complete patient profiles with OPD numbers, contact info, and medical history
- ✅ **Appointment System** - Schedule, track, and manage patient appointments with queue management
- ✅ **Treatment Records** - Document treatments with categorized types, pricing, and approval workflows
- ✅ **Payment Tracking** - Record payments by method (cash/online/card) with daily summaries
- ✅ **Multi-Tenancy** - Complete data isolation per clinic with subscription management
- ✅ **Role-Based Access** - Super Admin, Clinic Admin, Doctor, and Staff roles
- ✅ **Mobile-First Design** - Optimized for tablets and mobile devices with touch-friendly UI
- ✅ **Secure Authentication** - Better Auth with HTTP-only cookies and session management
- ✅ **RESTful API** - Well-documented API for integrations

### Tech Stack

**Frontend:**
- Next.js 14+ (App Router)
- React 18+
- TailwindCSS + shadcn/ui
- TypeScript

**Backend:**
- Express.js
- Better Auth
- Drizzle ORM
- PostgreSQL (Neon)

**Infrastructure:**
- Vercel (Frontend hosting)
- Railway (Backend hosting)
- Neon (Serverless PostgreSQL)
- Turborepo (Monorepo management)

---

## 🚀 Quick Start

### Prerequisites

- Node.js 20.x or higher
- pnpm 8.x or higher
- PostgreSQL database (or Neon account)

## 📚 Documentation

| Document | Description |
|----------|-------------|
| [API Reference](./docs/API.md) | Complete API documentation with examples |
| [Architecture](./docs/ARCHITECTURE.md) | System design, database schema, patterns |
| [Deployment Guide](./docs/DEPLOYMENT.md) | Production deployment to Vercel/Railway |
| [Troubleshooting](./docs/TROUBLESHOOTING.md) | Common issues and solutions |
| [Contributing](./docs/CONTRIBUTING.md) | Development workflow and guidelines |

---

## 📁 Project Structure

```
dental-crm/
├── apps/
│   ├── web/                 # Next.js frontend (Port 3001)
│   │   ├── src/app/         # App Router pages
│   │   ├── components/      # React components
│   │   └── lib/             # API client & utilities
│   │
│   ├── server/              # Express backend (Port 3000)
│   │   ├── src/routes/      # API endpoints
│   │   ├── src/services/    # Business logic
│   │   └── src/middleware/  # Auth, validation, etc.
│   │
│   └── native/              # React Native mobile app
│       └── app/             # Expo Router
│
├── packages/
│   ├── db/                  # Drizzle ORM & schemas
│   ├── auth/                # Better Auth config
│   ├── env/                 # Environment validation
│   └── config/              # Shared TypeScript configs
│
├── docs/                    # Documentation
└── turbo.json               # Turborepo config
```

---

## 🛠️ Development

### Available Scripts

```bash
# Development
pnpm run dev              # Start all apps (web + server + native)
pnpm run dev:web          # Web only
pnpm run dev:server       # Server only
pnpm run dev:native       # Mobile only

# Database
pnpm run db:push          # Push schema changes
pnpm run db:studio        # Open Drizzle Studio
pnpm run db:generate      # Generate migrations

# Quality
pnpm run check-types      # TypeScript check
pnpm run lint             # ESLint check
pnpm run build            # Build all packages
```

---

## 🏗️ Architecture

### Multi-Tenancy

Every table includes `clinicId` for complete data isolation:
```typescript
const patients = await db.query.patients.findMany({
  where: eq(patients.clinicId, req.clinic!.id)
});
```

### Authentication Flow

```
User → Better Auth → Session Cookie → Auth Middleware → Clinic Middleware → Route Handler
```

### Production Proxy Pattern

Frontend and backend are deployed separately but cookies work via Next.js rewrites:

```
Browser → Vercel (/api/*) → Rewrite → Railway → Response
```

---

## 🌐 Deployment

### Production URLs

- **Frontend:** https://flow-wise-alpha.vercel.app
- **Backend:** https://flowwise-production-a4ab.up.railway.app

### Quick Deploy

1. **Database:** Create Neon PostgreSQL project
2. **Backend:** Deploy to Railway with environment variables
3. **Frontend:** Deploy to Vercel with `NEXT_PUBLIC_SERVER_URL`
4. **Update:** Set Railway's `BETTER_AUTH_URL` to Vercel URL

---

## 🙏 Acknowledgments

- Built with [create-better-t-stack](https://github.com/AmanVarshney01/create-better-t-stack)
- UI components from [shadcn/ui](https://ui.shadcn.com/)
- Authentication by [Better Auth](https://www.better-auth.com/)

---

**Made with ❤️ for dental professionals**

