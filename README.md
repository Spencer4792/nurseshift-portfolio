# NurseShift

> **Transparent, fair nursing scheduling for healthcare professionals**

NurseShift is a mobile-first scheduling platform designed to solve the critical pain points plaguing the nursing scheduling industry. Built on principles of transparency, fairness, and exceptional user experience.

**Note:** The full production repository is private due to proprietary
business logic and IP. This repository serves as a technical case study
demonstrating architecture, features, and implementation decisions.

## Core Differentiators

### Transparent Pricing
- **No hidden fees** - Nurses see exactly what they'll earn before accepting a shift
- **Flat platform fee** - $2/shift capped at $4/day (vs competitors who take 20-30%)
- **Clear breakdown** - Every deduction explained upfront

### Fair Cancellation Policies
- **Symmetric policies** - Same rules for nurses and facilities
- **Guaranteed pay** - If facility cancels within 4 hours, nurse gets 4 hours paid
- **No punitive scoring** - Warnings instead of punishments for legitimate cancellations

### Two-Way Ratings
- **Nurses rate facilities** - See cancellation rates, payment reliability, staff reviews
- **Facilities rate nurses** - Professional feedback system
- **Dispute resolution** - Platform mediates, not deflects

### Modern UX
- **Native calendar sync** - Google, Apple, Outlook integration
- **Offline support** - Clock in/out works without connectivity
- **Real human support** - Not chatbots, actual people who help

## Project Structure

```
nurseshift/
├── apps/
│   ├── mobile/          # React Native (Expo) mobile app
│   ├── web/             # Next.js web application & facility dashboard
│   └── api/             # Node.js/Express API server
├── packages/
│   ├── database/        # Prisma schema & client
│   ├── shared/          # Shared types, schemas, utilities
│   └── ui/              # Shared UI components (future)
├── turbo.json           # Turborepo configuration
└── package.json         # Root package.json with workspaces
```

## Getting Started

### Prerequisites

- Node.js 18+
- PostgreSQL 14+
- npm 10+

### Installation

1. Clone the repository:
```bash
git clone https://github.com/yourusername/nurseshift.git
cd nurseshift
```

2. Install dependencies:
```bash
npm install
```

3. Set up environment variables:
```bash
cp .env.example .env
# Edit .env with your values
```

4. Set up the database:
```bash
npm run db:push
```

5. Start development:
```bash
npm run dev
```

## Packages

### @nurseshift/database
Prisma schema and database client. Contains all data models including:
- Users (nurses, facility admins)
- Nurse profiles with licenses and certifications
- Facilities and units
- Shifts with transparent pricing
- Applications and assignments
- Ratings (two-way)
- Earnings with fee breakdowns
- Time tracking with offline support

### @nurseshift/shared
Shared code across all apps:
- **Constants** - Platform fees, cancellation policies, SLAs
- **Schemas** - Zod validation for all API inputs
- **Types** - TypeScript interfaces for UI components
- **Utilities** - Pricing calculations, date formatting, distance calculations

## Architecture

### Tech Stack

| Layer | Technology | Rationale |
|-------|------------|-----------|
| Mobile | React Native + Expo | Cross-platform, hot updates |
| Web | Next.js 14 | SSR, excellent DX |
| API | Node.js + TypeScript | Type safety, async performance |
| Database | PostgreSQL + Prisma | ACID, complex queries, type-safe ORM |
| Cache | Redis | Sessions, real-time |
| Payments | Stripe Connect | Marketplace payments, instant payouts |
| Auth | JWT + OAuth | Secure, flexible |

### Key Design Decisions

1. **Transparent Pricing Engine**
   - All fees calculated upfront
   - No hidden deductions at payout
   - Nurses see net earnings before accepting

2. **Fair Cancellation System**
   - Same rules for both sides
   - Guaranteed minimums for last-minute facility cancellations
   - Warning system instead of immediate penalties

3. **Offline-First Time Tracking**
   - Clock in/out works without internet
   - Syncs when connectivity returns
   - No lost wages due to app issues

4. **Two-Way Accountability**
   - Nurses can see facility cancellation rates
   - Payment reliability visible
   - Reviews from other nurses

## Security & Compliance

- **HIPAA-ready architecture** - Encrypted data, audit logs, access controls
- **PCI-DSS compliant payments** - Via Stripe
- **SOC 2 target** - Security best practices

## Database Schema Highlights

```prisma
// Transparent pricing on every shift
model Shift {
  nursePayRate     Decimal  // What nurse earns
  platformFeeRate  Decimal  // Our fee (visible!)
  estimatedNurseEarnings Decimal  // Total take-home
}

// Visible facility metrics
model Facility {
  averageRating      Decimal?
  cancellationRate   Decimal?  // Nurses can see this!
  onTimePaymentRate  Decimal?  // Do they pay reliably?
}

// Offline-capable time tracking
model TimeEntry {
  capturedOffline  Boolean
  syncedAt         DateTime?
}
```

## Development

### Commands

```bash
# Start all apps in development
npm run dev

# Build all packages
npm run build

# Run linting
npm run lint

# Database operations
npm run db:generate  # Generate Prisma client
npm run db:push      # Push schema to database
npm run db:studio    # Open Prisma Studio
```

### Environment Variables

See `.env.example` for all required environment variables.

## Roadmap

### Phase 1: MVP (Months 1-4)
- [ ] Nurse registration & onboarding
- [ ] Shift discovery with transparent pricing
- [ ] Native calendar sync
- [ ] Basic application flow
- [ ] Clock in/out with offline support

### Phase 2: Enhanced Experience (Months 5-8)
- [ ] Two-way rating system
- [ ] In-app messaging
- [ ] Payment processing
- [ ] Support chat with real humans

### Phase 3: Intelligence & Scale (Months 9-12)
- [ ] AI-powered matching
- [ ] Burnout detection
- [ ] EHR integrations
- [ ] Facility analytics dashboard

## Contributing

We welcome contributions! Please see our contributing guidelines.

## License

Proprietary - All rights reserved.
