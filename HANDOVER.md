# Rate Cockpit — Complete Client Handover Document

> **Product:** Rate Cockpit — Freelancer Rate Calculator
> **Live URL:** https://ratecockpit.com
> **Founder:** Vinay Kumar
> **Support Email:** support@ratecockpit.com
> **Handover Date:** June 1, 2026

---

## 1. LIVE DEPLOYMENT

| Item | Value |
|------|-------|
| Primary Domain | https://ratecockpit.com |
| Backup URL | https://rate-calculator--vinay89656.replit.app |
| Deployment Type | Replit Autoscale |
| Platform | Replit (replit.com — account: Vinay89656@gmail.com) |
| Status | ✅ Live & Deployed |

---

## 2. TECH STACK

| Layer | Technology |
|-------|-----------|
| Frontend | React + Vite + TypeScript |
| Backend API | Express 5 + Node.js 24 |
| Database | PostgreSQL + Drizzle ORM |
| Validation | Zod v4 |
| Payments | Stripe (card) + UPI QR + PayPal QR |
| Monorepo | pnpm workspaces |
| Hosting | Replit Autoscale |
| DNS | Cloudflare |

---

## 3. PROJECT STRUCTURE

```
ratecockpit/
├── artifacts/
│   ├── rate-calculator/        ← React frontend (Vite)
│   │   ├── src/pages/          ← All website pages
│   │   ├── src/components/     ← Shared components
│   │   └── public/             ← Static files (images, QR codes, etc.)
│   └── api-server/             ← Express backend
│       └── src/routes/         ← API routes
├── lib/
│   └── db/src/schema/          ← Database schema (Drizzle ORM)
└── pnpm-workspace.yaml
```

---

## 4. ALL WEBSITE PAGES

| Page | Route | Description |
|------|-------|-------------|
| Home / Calculator | `/` | Main freelancer rate calculator |
| Pricing | `/pricing` | Free vs Premium plans |
| PDF Tools | `/pdf-tools` | Premium — PDF generation tools |
| Invoice | `/invoice` | Invoice generator |
| Contract | `/contract` | Contract generator |
| Project Calculator | `/project-calc` | Project-based pricing |
| Retainer Calculator | `/retainer-calc` | Monthly retainer pricing |
| ROI Calculator | `/roi-calc` | Client ROI calculator |
| Tax Calculator | `/tax-calc` | Tax estimation |
| Savings Calculator | `/savings-calc` | Savings planner |
| Late Payment | `/late-payment` | Late payment fee calculator |
| Rate Card | `/rate-card` | Rate card generator |
| Benchmarks | `/benchmarks` | Industry rate benchmarks |
| Blog | `/blog` | Blog section |
| About | `/about` | Founder info |
| Terms | `/terms` | Terms of Service |
| Login | `/login` | User login |
| Signup | `/signup` | User registration |
| Checkout | `/checkout` | Stripe payment checkout |
| Acquisition Doc | `/acquisition-doc` | Business sale document |
| Financial Doc | `/financial-doc` | Financial summary document |
| Logo Download | `/logo-download` | Brand assets download |

---

## 5. DATABASE SCHEMA

### Tables (PostgreSQL)

**`users`**
| Column | Type | Notes |
|--------|------|-------|
| id | text (PK) | UUID |
| name | text | User's name |
| email | text (unique) | Login email |
| password_hash | text | bcrypt hashed |
| stripe_customer_id | text | Stripe customer |
| stripe_subscription_id | text | Active subscription |
| is_premium | boolean | Premium status |
| agreed_to_terms | boolean | ToS acceptance |
| created_at | timestamp | Registration date |

**`saved_profiles`**
| Column | Type | Notes |
|--------|------|-------|
| id | serial (PK) | Auto-increment |
| user_id | text (FK) | References users.id |
| name | text | Profile name |
| data | jsonb | Rate profile JSON data |
| created_at | timestamp | |
| updated_at | timestamp | |

**`sessions`**
| Column | Type | Notes |
|--------|------|-------|
| sid | text (PK) | Session ID |
| sess | jsonb | Session data |
| expire | timestamp | Expiry time |

---

## 6. API ENDPOINTS

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/health` | Health check |
| POST | `/api/auth/signup` | Register new user |
| POST | `/api/auth/login` | Login |
| POST | `/api/auth/logout` | Logout |
| GET | `/api/auth/me` | Get current user |
| GET | `/api/user/profiles` | Get saved profiles |
| POST | `/api/user/profiles` | Save a profile |
| DELETE | `/api/user/profiles/:id` | Delete a profile |
| GET | `/api/stripe/config` | Get Stripe publishable key |
| POST | `/api/stripe/create-subscription` | Create Stripe subscription |

---

## 7. MONETIZATION

### Subscription
- **Price:** $6.25/month
- **Payment:** Stripe (card payments)
- **Premium Features:** PDF Tools, PDF exports, saved profiles, ad-free

### Manual Payments (UPI & PayPal)
- **UPI:** vikash709804@oksbi (QR at `/public/qr-upi.jpg`)
- **PayPal:** Vinay Kumar (QR at `/public/qr-paypal.jpg`)
- Manual — after payment verify and flip `is_premium = true` in DB for user

---

## 8. ENVIRONMENT VARIABLES (Secrets)

These are stored in Replit Secrets — **never hardcode these:**

| Variable | Purpose |
|----------|---------|
| `DATABASE_URL` | PostgreSQL connection string |
| `SESSION_SECRET` | Express session encryption key |
| `STRIPE_SECRET_KEY` | Stripe secret key (from Stripe dashboard) |
| `STRIPE_PUBLISHABLE_KEY` | Stripe publishable key |

**Where to find:** Replit → Project → Secrets tab

---

## 9. DNS CONFIGURATION (Cloudflare)

Domain: `ratecockpit.com` — DNS managed via Cloudflare

| Type | Name | Target | Proxy |
|------|------|--------|-------|
| CNAME | `@` | `rate-calculator--vinay89656.replit.app` | DNS only (grey) |
| CNAME | `www` | `rate-calculator--vinay89656.replit.app` | DNS only (grey) |

> ⚠️ Keep proxy **OFF** (grey cloud). Orange cloud breaks Replit SSL.

---

## 10. HOW TO DEPLOY / REDEPLOY

1. Go to **replit.com** → Login with Vinay89656@gmail.com
2. Open the **Rate Cockpit** project
3. Click **Publish** (top right) → **Deploy**
4. Wait ~2 minutes for build to complete
5. Site is live at https://ratecockpit.com

---

## 11. HOW TO RUN LOCALLY (Development)

```bash
# Install dependencies
pnpm install

# Start API server (port 8080)
pnpm --filter @workspace/api-server run dev

# Start frontend (auto port from workflow)
pnpm --filter @workspace/rate-calculator run dev

# Push DB schema changes
pnpm --filter @workspace/db run push

# Full typecheck
pnpm run typecheck
```

---

## 12. STATIC FILES (public/)

| File | Purpose |
|------|---------|
| `logo.svg` | Main site logo |
| `favicon.svg` | Browser favicon |
| `founder.jpg` | Vinay Kumar photo (About page) |
| `qr-upi.jpg` | UPI payment QR code |
| `qr-paypal.jpg` | PayPal payment QR code |
| `opengraph.jpg` | Social media preview image |
| `robots.txt` | SEO crawler rules |
| `sitemap.xml` | SEO sitemap |
| `acquisition-doc.html` | Business sale document |
| `financial-doc.html` | Financial summary |
| `logo-download.html` | Brand assets page |

---

## 13. KEY CONTACTS

| Role | Name | Contact |
|------|------|---------|
| Founder / Owner | Vinay Kumar | support@ratecockpit.com |
| Replit Account | Vinay89656@gmail.com | replit.com |
| Cloudflare Account | (same Gmail) | cloudflare.com |
| Stripe Account | (same Gmail) | dashboard.stripe.com |

---

## 14. PREMIUM USER MANAGEMENT (Manual UPI/PayPal)

When a user pays via UPI or PayPal manually:

1. Get their registered email
2. Run this SQL on the database:

```sql
UPDATE users SET is_premium = true WHERE email = 'user@example.com';
```

3. User will get premium access on next login

---

*Document generated: June 1, 2026*
