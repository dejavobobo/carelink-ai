# CareLink AI

CareLink AI is a HIPAA-aware telehealth and home-care marketplace built with Next.js 14, Tailwind CSS, Prisma, PostgreSQL, and OpenAI.

## Folder structure

- `app/` - Next.js App Router pages and API routes
- `components/` - shared UI components
- `lib/` - backend utilities for auth, database access, matching, and notifications
- `prisma/` - Prisma data model schema
- `styles/` - style assets and Tailwind config

## Key files

- `prisma/schema.prisma` - database model definitions
- `app/api/auth/register/route.ts` - user signup
- `app/api/auth/login/route.ts` - JWT login
- `app/api/providers/route.ts` - provider registration and listing
- `app/api/appointments/route.ts` - appointment booking and retrieval
- `app/api/ai-assistant/route.ts` - OpenAI conversational scheduling assistant
- `app/api/match/route.ts` - nearest available provider matching

## Setup

1. Copy environment variables:
   ```bash
   cp .env.example .env
   ```
2. Install dependencies:
   ```bash
   npm install
   ```
3. Generate Prisma client:
   ```bash
   npx prisma generate
   ```
4. Run database migrations after configuring `DATABASE_URL`:
   ```bash
   npx prisma migrate dev --name init
   ```
5. Start the development server:
   ```bash
   npm run dev
   ```

## Deployment

### Vercel

1. Connect the repository to Vercel.
2. Set environment variables in Vercel dashboard:
   - `DATABASE_URL`
   - `JWT_SECRET`
   - `OPENAI_API_KEY`
   - `EMAIL_HOST`, `EMAIL_PORT`, `EMAIL_USER`, `EMAIL_PASSWORD`
   - `TWILIO_ACCOUNT_SID`, `TWILIO_AUTH_TOKEN`, `TWILIO_MESSAGING_SERVICE_SID`
   - `GOOGLE_MAPS_API_KEY`
3. Use the default Next.js build command:
   ```bash
   npm run build
   ```

### PostgreSQL

Provision a managed PostgreSQL database and connect using `DATABASE_URL`.

## Notes

- The AI assistant uses OpenAI chat completions.
- Authentication is JWT-based with role support for `PATIENT`, `NURSE`, `PRACTITIONER`, and `ADMIN`.
- Provider availability is stored as JSON and matched against requested appointment times.
- Email and SMS notifications are supported via Nodemailer and Twilio.
