# KeyLedger — browser-only expense preview

KeyLedger is a frontend-only expense-tracking preview for small property and small-business operators. It runs as a Next.js application and stores changes in this browser on this device only.

## Included screens and features

- **Overview** (`/`): calculated spending summaries, category breakdown, recent expenses, and a shared date range.
- **Expenses** (`/expenses`): search and filters, create/edit/delete flows, duplicate warnings, bulk category/property updates, and CSV export.
- **Property reports** (`/reports`): property-level totals, average expense, category mix, unassigned entries, and the selected date range.
- **Budgets** (`/budgets`): category or property monthly limits, progress, warning thresholds, and over-budget notices.
- **Recurring templates** (`/recurring`): monthly, quarterly, or yearly templates that create reviewable drafts only after a user action; an expense is saved only after confirmation.
- **Data tools** (`/data`): CSV import preview/validation and JSON backup/restore.
- **Expense forms** (`/expenses/new` and `/expenses/[id]/edit`): required amount/date/description/category fields; optional vendor, property label, payment method, note, voice-to-note, and receipt preview.

## Run locally

Requires Node.js 18.18 or newer; Node.js 22 LTS is recommended.

```bash
npm ci
npm run dev
```

Open the local URL printed by Next.js. For production validation:

```bash
npm run typecheck
npm run build
npm start
```

## Deployment and verification

- Follow [DEPLOYMENT.md](./DEPLOYMENT.md) for GitHub-to-Vercel steps.
- Read [VERIFICATION.md](./VERIFICATION.md) for the checks actually run, their results, and known limitations.

## Important limitations

This is a **browser-only preview**, not a secure multi-user expense service. It has no authentication, database, API, server-side sync, Supabase integration, or cross-device sync. Expense records, budgets, recurring templates, and receipts are kept in browser local storage. They are scoped to the browser profile and site origin, can be lost if browser data is cleared, are not encrypted by this app, and may be constrained by browser storage quotas.

Receipt files are kept locally and are not uploaded. The app does not provide protected receipt access. Voice capture depends on browser speech-recognition and microphone permissions; its current behavior is to add a transcript to an editable note, not to extract structured expense fields or parse spoken amounts. Typed notes are always available. Sample records and NGN figures are illustrative, not a confirmed business reporting currency.

Do not use this preview for sensitive or multi-user financial records. Authentication, database persistence, Row Level Security, secure receipt uploads, and cross-user isolation are not implemented. See the verification report for features that were not exercised in this run.
