@AGENTS.md

# Dairy Farm Management System — AI Development Master Plan

## 0. Purpose

This repository is for building a production-ready Dairy Farm Management System for a dairy farm in Pakistan.

The system should manage:

- Animals and animal profiles
- Animal age, weight and growth
- Milk production and milk sales
- Treatments and treatment history
- Medicines and medicine records
- Vaccinations
- Deworming
- Breeding, AI, pregnancy and calving
- Feed calculator
- Feed formulas and ingredient prices
- Feed/medicine inventory
- Farm expenses and profit
- Calendar and reminders
- Browser/PWA notifications
- WhatsApp alerts
- Reports
- Multi-user farm access
- Future AI farm assistant

The primary goal is a practical farm-management system that is easy to use from a phone.

---

# 1. AI AGENT OPERATING RULES

Any AI coding agent (Claude Code, Claude web, Cursor, Codex, etc.) working on this repository MUST follow these rules.

## Rule 1 — Read this file first

Before changing code, read:

`/DAIRY_FARM_MASTER_PLAN.md`

Also inspect the existing repository structure and current implementation.

Do not assume that a phase is incomplete just because this file says it is planned.

## Rule 2 — Inspect before modifying

Before coding:

1. Inspect package.json
2. Inspect Next.js configuration
3. Inspect Supabase configuration
4. Inspect environment variable usage
5. Inspect existing routes/pages
6. Inspect existing components
7. Inspect database migrations
8. Inspect authentication
9. Inspect current tests
10. Inspect README and other project documentation

Never rewrite an existing working system unnecessarily.

## Rule 3 — Preserve working functionality

Do not break existing functionality.

Prefer small, focused changes.

Do not replace libraries/frameworks unless there is a documented technical reason.

## Rule 4 — No fake implementation

Do NOT create fake buttons, fake dashboards, fake database responses, placeholder CRUD, or hard-coded production data and call the feature complete.

A feature is complete only when the relevant data flow works end-to-end.

## Rule 5 — Security first

Never expose:

- Supabase service-role keys
- WhatsApp API secrets
- private tokens
- database credentials
- API keys

Never commit `.env` secrets.

Use environment variables and server-side functions where appropriate.

## Rule 6 — Database changes must be migrations

Never manually modify production database structure without a migration.

Every schema change must have a migration file.

## Rule 7 — Validate after every phase

At minimum run:

- TypeScript check
- Linter
- Build
- Relevant tests
- Database migration validation where applicable

Fix errors before declaring a phase complete.

## Rule 8 — Don't overbuild

Only implement the current phase unless a dependency is required.

Do not jump ahead into WhatsApp, AI, advanced analytics, etc. during early phases.

## Rule 9 — Veterinary safety

The app may store veterinary information, but it must not invent medical treatment protocols.

Medicine records should support:

- Active ingredient
- Strength/concentration
- Species
- Route
- Dose
- Milk withdrawal
- Meat withdrawal
- Warnings
- Vet notes

Any automated dosage calculation must be based on a verified protocol/product label and clearly show that it requires professional confirmation.

## Rule 10 — Farm usability

The UI should be:

- Mobile-first
- Fast
- Simple
- Large touch targets
- Easy for non-technical farm staff
- Usable in Roman Urdu/English labels where useful
- Optimized for weak/intermittent internet where practical

---

# 2. RECOMMENDED STACK

Use:

- Next.js
- React
- TypeScript
- Tailwind CSS
- Supabase PostgreSQL
- Supabase Auth
- Supabase Storage
- Supabase Edge Functions where required
- Supabase Cron for scheduled jobs
- PWA
- Vercel
- Recharts or an equivalent lightweight chart library
- React Hook Form
- Zod

Do not build a native mobile app initially.

Build a responsive PWA first.

Later, the same backend can support a native Android/iOS application.

---

# 3. DEVELOPMENT STRATEGY

Build in this order:

1. Foundation
2. Database + security
3. Authentication
4. Animals
5. Health/treatments
6. Vaccination/deworming
7. Milk
8. Breeding
9. Feed
10. Expenses/profit
11. Inventory
12. Calendar/reminders
13. Notifications
14. WhatsApp
15. Reports
16. Offline/PWA improvements
17. AI assistant
18. Production hardening

Do not start with WhatsApp.

The core farm system must work without WhatsApp.

---

# 4. PHASE STATUS

Update this section after every completed phase.

Current phase:

`PHASE 0 — NOT STARTED`

Completed phases:

- None

Next phase:

`PHASE 0`

---

# 5. PHASE 0 — REPOSITORY AUDIT & FOUNDATION

## Goal

Understand the existing project before making changes.

## Tasks

- Inspect repository
- Identify framework/version
- Identify package manager
- Identify existing routes
- Identify existing components
- Identify current Supabase setup
- Identify environment variables
- Identify existing authentication
- Identify styling system
- Identify existing testing
- Identify deployment configuration
- Identify technical debt
- Identify anything already implemented

Create/update:

`docs/PROJECT_AUDIT.md`

The audit should contain:

- Current architecture
- Existing functionality
- Missing functionality
- Risks
- Recommended changes
- Commands used to verify project
- Proposed folder structure

## Verification

Run:

- install/dependency check
- lint
- typecheck
- build
- tests if available

## Completion criteria

Do not proceed until:

- Existing project is understood
- Build works
- No unexplained critical errors remain
- `docs/PROJECT_AUDIT.md` exists

## Handoff

After completion, report:

1. What was inspected
2. What already exists
3. What needs to be built
4. What was changed
5. Verification results
6. Any blockers

Then update this master file:

`PHASE 0 — COMPLETE`

and set next phase to:

`PHASE 1`

---

# 6. PHASE 1 — DATABASE ARCHITECTURE

## Goal

Create the core Supabase/PostgreSQL data model.

## Core tables

### farms

Fields:

- id
- name
- currency
- timezone
- created_at
- updated_at

### profiles

- id
- full_name
- phone
- role
- created_at
- updated_at

### farm_members

- id
- farm_id
- user_id
- role
- created_at

### animals

- id
- farm_id
- tag_number
- name
- species
- breed
- sex
- date_of_birth
- purchase_date
- purchase_price
- source
- color
- current_weight
- weight_date
- status
- is_milking
- is_pregnant
- is_dry
- lactation_number
- mother_id
- father_id
- photo_url
- notes
- created_at
- updated_at

### weight_records

- id
- animal_id
- date
- weight_kg
- measurement_method
- notes
- created_at

### medicines

- id
- name
- brand_name
- active_ingredient
- concentration
- dosage_unit
- route
- species
- purpose
- manufacturer
- milk_withdrawal_days
- meat_withdrawal_days
- warnings
- active
- created_at

### treatments

- id
- animal_id
- treatment_date
- problem
- diagnosis
- medicine_id
- dose
- dose_unit
- route
- frequency
- duration
- vet_name
- notes
- next_due_date
- withdrawal_milk_until
- withdrawal_meat_until
- status
- created_by
- created_at

### vaccines

- id
- name
- disease
- manufacturer
- default_interval_days
- dose
- route
- notes

### vaccinations

- id
- animal_id
- vaccine_id
- date_given
- batch_number
- dose
- next_due_date
- administered_by
- notes

### breeding_events

- id
- animal_id
- event_type
- event_date
- bull_or_semen
- semen_batch
- technician
- cost
- pregnancy_result
- pregnancy_check_date
- expected_calving_date
- notes

### milk_records

- id
- animal_id
- date
- morning_liters
- evening_liters
- total_liters
- recorded_by
- notes

### milk_sales

- id
- farm_id
- date
- quantity_liters
- rate_per_liter
- total_amount
- customer
- payment_status
- notes

### ingredients

- id
- name
- unit
- current_price
- price_date
- dry_matter
- crude_protein
- tdn
- fat
- fiber
- calcium
- phosphorus
- stock_quantity
- supplier
- created_at
- updated_at

### feed_formulas

- id
- name
- animal_category
- target_cp
- target_tdn
- notes

### feed_formula_items

- id
- formula_id
- ingredient_id
- percentage
- kg_per_100kg

### feed_records

- id
- animal_id
- date
- ingredient/formula reference
- quantity_kg
- cost
- notes

### expenses

- id
- farm_id
- date
- category
- animal_id
- description
- amount
- payment_method
- supplier
- receipt_url
- notes

### inventory_items

- id
- farm_id
- name
- category
- unit
- current_stock
- minimum_stock
- purchase_price
- supplier
- expiry_date

### inventory_transactions

- id
- inventory_item_id
- transaction_type
- quantity
- unit_cost
- reference_type
- reference_id
- date
- notes

### reminders

- id
- farm_id
- animal_id
- type
- title
- description
- due_at
- priority
- status
- repeat_rule
- channel_app
- channel_push
- channel_whatsapp
- completed_at
- created_at

### notification_queue

- id
- reminder_id
- channel
- recipient
- message_template
- scheduled_at
- sent_at
- status
- provider_message_id
- error_message
- retry_count

## Security

Implement Row Level Security.

Users must only access data belonging to farms they are members of.

Roles:

- owner
- manager
- worker

Workers should not automatically have financial/admin permissions.

## Verification

- Run all migrations on a clean database
- Test relationships
- Test RLS
- Test unauthorized access
- Run type generation if used
- Run lint/typecheck/build

## Completion

Database and RLS must be genuinely functional.

Update master status to:

`PHASE 1 — COMPLETE`

---

# 7. PHASE 2 — AUTHENTICATION & FARM SETUP

## Goal

Create secure login and initial farm setup.

Features:

- Login
- Logout
- Password reset
- Farm creation
- Farm membership
- Role assignment
- Profile
- Basic settings

## Verification

Test:

- Owner login
- Worker login
- Invalid login
- Logout
- Password reset
- Unauthorized farm access

Then mark:

`PHASE 2 — COMPLETE`

---

# 8. PHASE 3 — ANIMAL MANAGEMENT

## Goal

Build the central animal management system.

Pages:

`/animals`

`/animals/new`

`/animals/[id]`

Features:

- Animal list
- Search
- Filter
- Add animal
- Edit animal
- Archive animal
- Animal photo
- Automatic age calculation
- Weight records
- Animal timeline

Animal profile tabs:

- Overview
- Health
- Vaccination
- Deworming
- Breeding
- Milk
- Feed
- Expenses
- Timeline

Age must be calculated from DOB rather than permanently stored.

## Verification

Create test animals.

Verify:

- Create
- Edit
- Search
- Filter
- Delete/archive permissions
- Age calculation
- Weight history
- Photo upload
- RLS

Then:

`PHASE 3 — COMPLETE`

---

# 9. PHASE 4 — HEALTH & TREATMENTS

## Goal

Build treatment records without unsafe automatic medical assumptions.

Pages:

- `/health`
- `/health/treatments`
- `/medicines`

Features:

- Add treatment
- Medicine selection
- Active ingredient
- Strength/concentration
- Dose
- Route
- Frequency
- Duration
- Vet
- Diagnosis
- Notes
- Milk withdrawal
- Meat withdrawal
- Follow-up date
- Treatment history

## Safety

Never infer a dose merely from medicine name.

If a calculator is added later, it must require:

- Species
- Weight
- Product concentration
- Verified dosing protocol

## Verification

Test complete treatment CRUD and animal history integration.

Then:

`PHASE 4 — COMPLETE`

---

# 10. PHASE 5 — VACCINATION & DEWORMING

## Goal

Track preventive health.

Features:

- Vaccine library
- Vaccination records
- Batch number
- Date given
- Next due date
- Deworming records
- Preventive-care history
- Reminder creation

Next due dates should be configurable rather than assuming one universal schedule.

Then:

`PHASE 5 — COMPLETE`

---

# 11. PHASE 6 — MILK MANAGEMENT

## Goal

Track milk production and sales.

Features:

- Morning milk
- Evening milk
- Daily total
- Animal-level milk
- Farm-level milk
- Milk sales
- Rate/liter
- Revenue
- Historical chart
- Monthly summary

Formula:

`Revenue = Liters × Rate`

Then:

`PHASE 6 — COMPLETE`

---

# 12. PHASE 7 — BREEDING & PREGNANCY

## Goal

Track reproductive events.

Event types:

- Heat
- AI
- Natural service
- Pregnancy check
- Pregnant
- Not pregnant
- Calving
- Abortion

Features:

- Breeding date
- Semen/bull
- Technician
- Cost
- Pregnancy check
- Expected calving date
- Notes
- Reminder

Gestation calculations must be configurable and should not be presented as medical certainty.

Then:

`PHASE 7 — COMPLETE`

---

# 13. PHASE 8 — FEED CALCULATOR & FORMULA BUILDER

## Goal

Create practical feed management.

## Feed Calculator

Inputs:

- Animal type
- Weight
- Milk/day
- Lactation
- Pregnancy
- Dry status
- Feed availability

Outputs:

- Green fodder
- Dry fodder
- Concentrate
- Mineral
- Water
- Estimated cost

The nutritional formulas must be configurable.

Do not hard-code unsafe universal rations.

## Formula Builder

Allow:

- Ingredient selection
- Percentage
- Batch size
- Cost/kg
- CP estimate
- TDN estimate
- Mineral/DCP inclusion
- Saved formulas

Cost:

`Ingredient cost = quantity × price/kg`

`Batch cost = sum of ingredient costs`

`Cost/kg = batch cost ÷ batch weight`

`Daily cost = daily quantity × cost/kg`

Then:

`PHASE 8 — COMPLETE`

---

# 14. PHASE 9 — EXPENSES, PROFIT & INVENTORY

## Goal

Understand actual farm economics.

Expense categories:

- Feed
- Medicine
- Vet
- Vaccine
- Breeding
- Labour
- Electricity
- Transport
- Maintenance
- Other

Profit:

`Net Profit = Milk Revenue - Total Expenses`

Metrics:

- Profit/month
- Profit/liter
- Feed cost/liter
- Feed cost/animal
- Medicine cost/animal

Inventory:

- Feed
- Medicine
- Vaccines
- Supplements
- Other supplies

Stock should automatically decrease when linked consumption is recorded.

Low-stock alerts must be supported.

Then:

`PHASE 9 — COMPLETE`

---

# 15. PHASE 10 — FARM DASHBOARD

## Goal

Create a useful daily command center.

Dashboard cards:

- Total animals
- Milking animals
- Dry animals
- Pregnant animals
- Calves
- Today's milk
- Today's revenue
- Today's feed cost
- Today's expenses
- Estimated profit
- Due treatments
- Due vaccines
- Due breeding tasks
- Low stock

Quick actions:

- Add Animal
- Add Treatment
- Add Milk
- Add Expense
- Feed Calculator

Dashboard must use real database data.

No fake metrics.

Then:

`PHASE 10 — COMPLETE`

---

# 16. PHASE 11 — CALENDAR & REMINDER ENGINE

## Goal

Centralize all upcoming tasks.

Reminder types:

- Treatment
- Vaccination
- Deworming
- Breeding
- Pregnancy check
- Calving
- Dry-off
- Custom

Reminder states:

- Upcoming
- Due today
- Overdue
- Completed
- Cancelled

Reminder windows:

- 7 days before
- 3 days before
- 1 day before
- Due day

These must be configurable.

Use Supabase Cron for scheduled processing where appropriate.

Flow:

`Record saved → reminder created → scheduled check → notification queue`

Then:

`PHASE 11 — COMPLETE`

---

# 17. PHASE 12 — PUSH/BROWSER NOTIFICATIONS

## Goal

Notify the owner without requiring WhatsApp initially.

Implement:

- PWA
- Service worker
- Notification permission
- Push subscription
- Reminder notifications

Example:

`Cow COW-104 — Deworming due tomorrow.`

Handle:

- Permission denied
- Expired subscription
- Retry
- Duplicate prevention

Then:

`PHASE 12 — COMPLETE`

---

# 18. PHASE 13 — WHATSAPP ALERTS

## Goal

Add WhatsApp automation after the internal reminder system is stable.

Architecture:

`Database`

↓

`Supabase Cron`

↓

`Reminder Engine`

↓

`Notification Queue`

↓

`Server-side/Edge Function`

↓

`WhatsApp Business Platform/API`

↓

`Owner WhatsApp`

Never expose WhatsApp secrets in frontend code.

Notification states:

- pending
- sending
- sent
- failed
- retrying
- cancelled

Implement retries and logging.

WhatsApp templates and current platform requirements must be verified against official Meta/WhatsApp documentation before production deployment.

Do not assume WhatsApp messaging is permanently free.

Then:

`PHASE 13 — COMPLETE`

---

# 19. PHASE 14 — REPORTS

Reports:

## Daily

- Milk
- Feed
- Expenses
- Treatments

## Weekly

- Milk trend
- Feed consumption
- Expenses

## Monthly

- Milk
- Revenue
- Feed cost
- Medicine
- Other expenses
- Net profit

## Animal report

- Milk
- Weight
- Treatments
- Breeding
- Expenses
- Feed

Add export later:

- CSV
- Excel
- PDF

Then:

`PHASE 14 — COMPLETE`

---

# 20. PHASE 15 — PWA, OFFLINE & MOBILE UX

## Goal

Make the app genuinely useful on the farm.

Features:

- Installable PWA
- Mobile navigation
- Large buttons
- Fast forms
- Offline-friendly basic data entry
- Sync when connection returns

Offline synchronization must include conflict prevention.

Do not implement complicated offline writes unless the data model can safely reconcile duplicates/conflicts.

Then:

`PHASE 15 — COMPLETE`

---

# 21. PHASE 16 — AI FARM ASSISTANT

Only after all core data is reliable.

Examples:

- "Which cows produced the most milk this month?"
- "Which treatments are due?"
- "What was feed cost this month?"
- "Show COW-104 history."
- "Which animals have falling milk production?"

AI should query farm data through controlled server-side tools.

Do not give the AI unrestricted database access.

Do not allow AI to silently modify health records.

For medical questions, the assistant should distinguish:

- Stored farm record
- General educational information
- Veterinary recommendation requiring professional confirmation

Then:

`PHASE 16 — COMPLETE`

---

# 22. PHASE 17 — PRODUCTION HARDENING

Before real production:

- Security audit
- RLS audit
- Auth audit
- Input validation
- Error handling
- Rate limiting
- Logging
- Backups
- Database indexes
- Performance optimization
- Image optimization
- Accessibility
- Mobile testing
- Browser testing
- PWA testing
- Notification testing
- WhatsApp failure testing

Test with realistic farm data.

Do not use sensitive real credentials in development.

Then:

`PHASE 17 — COMPLETE`

---

# 23. FINAL DATABASE RELATIONSHIP

Conceptually:

FARM
→ USERS / FARM MEMBERS

FARM
→ ANIMALS

ANIMAL
→ WEIGHT RECORDS
→ TREATMENTS
→ VACCINATIONS
→ BREEDING EVENTS
→ MILK RECORDS
→ FEED RECORDS
→ EXPENSES
→ REMINDERS

FARM
→ MEDICINES
→ VACCINES
→ INGREDIENTS
→ FEED FORMULAS
→ INVENTORY
→ EXPENSES
→ MILK SALES
→ NOTIFICATION QUEUE

---

# 24. SUGGESTED ROUTE STRUCTURE

```text
/
 /login
 /dashboard

 /animals
 /animals/new
 /animals/[id]

 /health
 /health/treatments
 /health/vaccinations
 /health/deworming
 /medicines

 /breeding

 /milk
 /milk/sales

 /feed
 /feed/calculator
 /feed/formulas
 /feed/ingredients

 /expenses
 /inventory

 /reminders
 /calendar

 /reports

 /settings
 /settings/farm
 /settings/users
 /settings/notifications
 /settings/whatsapp
```

---

# 25. SUGGESTED CODE STRUCTURE

Adapt this to the existing project rather than blindly replacing it.

```text
src/
  app/
  components/
  features/
    animals/
    health/
    vaccination/
    breeding/
    milk/
    feed/
    expenses/
    inventory/
    reminders/
    notifications/
    reports/
  lib/
    supabase/
    validation/
    calculations/
    permissions/
  hooks/
  types/
  utils/

supabase/
  migrations/
  functions/

docs/
  PROJECT_AUDIT.md
  DATABASE.md
  SECURITY.md
  NOTIFICATIONS.md
  WHATSAPP.md
  TESTING.md
```

---

# 26. CALCULATION RULES

Calculations should live in reusable utility functions, not duplicated inside UI components.

Examples:

`calculateAge(dob, today)`

`calculateMilkTotal(morning, evening)`

`calculateMilkRevenue(liters, rate)`

`calculateIngredientCost(quantity, price)`

`calculateBatchCost(items)`

`calculateCostPerKg(batchCost, batchWeight)`

`calculateDailyFeedCost(quantity, costPerKg)`

`calculateProfit(revenue, expenses)`

Calculations should have unit tests.

---

# 27. TESTING STANDARD

For each important feature:

## Unit tests

Calculations and pure functions.

## Integration tests

Database operations and business logic.

## E2E tests

Critical user journeys.

Minimum critical flows:

1. Login
2. Create farm
3. Add animal
4. Edit animal
5. Add treatment
6. Add vaccine
7. Add milk
8. Add expense
9. Create reminder
10. Complete reminder
11. Feed calculation
12. Dashboard totals
13. Permission restrictions

---

# 28. DEFINITION OF DONE

A phase is NOT complete merely because code was written.

A phase is complete only when:

- Feature works end-to-end
- Data persists correctly
- Permissions are correct
- Validation works
- Errors are handled
- Mobile UI works
- Tests pass
- Lint passes
- Typecheck passes
- Build passes
- Documentation is updated
- No known critical regression exists

---

# 29. VERIFICATION REPORT FORMAT

After every phase, AI must provide:

```text
PHASE: X

STATUS:
COMPLETE / BLOCKED

IMPLEMENTED:
- ...
- ...

FILES CHANGED:
- ...

DATABASE CHANGES:
- ...

TESTS:
- ...

TYPECHECK:
PASS / FAIL

LINT:
PASS / FAIL

BUILD:
PASS / FAIL

MANUAL VERIFICATION:
- ...

KNOWN ISSUES:
- ...

NEXT PHASE:
X+1
```

Then update this file's PHASE STATUS section.

---

# 30. PROMPT FOR ANY AI CODING AGENT

Use this when starting a new AI session:

```text
Read /DAIRY_FARM_MASTER_PLAN.md completely before doing anything.

You are working on the Dairy Farm Management System.

First inspect the repository and determine the current phase from the master plan.

Do not assume previous work is correct. Verify the current implementation.

If the current phase is incomplete, continue ONLY that phase.

If the current phase is already complete and verified, explain why and ask/prepare for the next phase according to the master plan.

Do not jump multiple phases ahead.

Before coding:
1. Inspect the existing architecture.
2. Inspect relevant files.
3. Inspect database migrations.
4. Inspect environment variables without exposing secrets.
5. Identify dependencies.
6. Make a short implementation plan.

Then implement the current phase.

After implementation:
1. Run tests.
2. Run typecheck.
3. Run lint.
4. Run production build.
5. Fix all issues you introduced.
6. Verify database/security changes.
7. Update documentation.
8. Update PHASE STATUS in /DAIRY_FARM_MASTER_PLAN.md.
9. Produce the required verification report.

Never use fake data to hide incomplete functionality.

Never expose secrets.

Never make unsafe veterinary treatment assumptions.

Do not modify unrelated parts of the application unless required.
```

---

# 31. PROMPT FOR CONTINUING FROM A COMPLETED PHASE

```text
Read /DAIRY_FARM_MASTER_PLAN.md.

I have verified that PHASE X is complete.

Start PHASE X+1 only.

First inspect the current implementation and confirm that the previous phase actually works.

Then implement the next phase according to the master plan.

Do not redo completed work unless you find a real defect.

At the end:
- test
- typecheck
- lint
- build
- verify manually
- document changes
- update the master plan status
- give me the verification report
- clearly state the next phase
```

---

# 32. IMPORTANT RULE FOR CLAUDE WEB / CLAUDE CODE / CURSOR

The same master plan should remain the source of truth.

If moving between AI platforms:

1. Commit/save the current code.
2. Update this MD file.
3. Tell the new AI to read this file.
4. Tell it the last verified phase if necessary.
5. Ask it to inspect the actual repository before continuing.

Do not rely on chat history as the project specification.

The repository + this master plan should be the source of truth.

---

# 33. CLAUDE WEB VS CLAUDE CODE

Recommended workflow:

## Claude Code / coding extension

Use for:

- Reading repository
- Creating/editing files
- Running commands
- Running tests
- Database migrations
- Refactoring
- Debugging
- Implementing phases

This should be the PRIMARY development environment.

## Claude Web

Use for:

- Architecture discussion
- Reviewing plans
- Reviewing code snippets
- Research
- Writing documentation
- Checking business logic
- Planning the next phase

Do not depend on Claude Web alone for large repository implementation if it cannot reliably inspect and modify the entire project.

## Cursor/Codex/other coding agents

Can also be used.

The master MD file is deliberately platform-independent.

---

# 34. GIT WORKFLOW

Recommended:

```text
main
  │
  ├── phase-0-foundation
  ├── phase-1-database
  ├── phase-2-auth
  ├── phase-3-animals
  ├── phase-4-health
  └── ...
```

Before starting a phase:

```text
git status
git pull
```

After successful verification:

```text
git add .
git commit -m "Complete phase X"
```

Do not commit secrets.

---

# 35. ENVIRONMENT VARIABLES

Use a `.env.example`.

Never commit real values.

Example structure:

```text
NEXT_PUBLIC_SUPABASE_URL=
NEXT_PUBLIC_SUPABASE_ANON_KEY=

SUPABASE_SERVICE_ROLE_KEY=

WHATSAPP_ACCESS_TOKEN=
WHATSAPP_PHONE_NUMBER_ID=
WHATSAPP_BUSINESS_ACCOUNT_ID=
```

Only variables genuinely required by the chosen architecture should be included.

Server-only secrets must never be exposed through `NEXT_PUBLIC_*`.

---

# 36. IMPORTANT PRODUCT PRINCIPLE

The application should answer three questions quickly:

### What happened?

History.

### What is happening?

Dashboard.

### What needs to happen next?

Reminders.

The third question is the most important.

The app should reduce the chance of forgetting:

- Treatment
- Vaccine
- Deworming
- Pregnancy check
- Calving
- Feed purchase
- Inventory refill
- Other scheduled farm tasks

---

# 37. FUTURE FEATURES

Only after the core system is stable:

- Multiple farms
- Customer management
- Milk delivery routes
- Customer WhatsApp notifications
- Barcode/QR animal tags
- RFID integration
- Automatic weighing
- Advanced analytics
- Weather integration
- Feed optimization
- AI assistant
- Native mobile application

Do not implement these before the core roadmap is complete.

---

# 38. FINAL SUCCESS CRITERIA

The project is successful when the owner can open the app on a phone and:

1. See the whole farm status.
2. Find any animal within seconds.
3. Open its complete history.
4. Record treatment.
5. Record vaccination.
6. Record deworming.
7. Record breeding/pregnancy.
8. Record milk.
9. Calculate feed.
10. Track feed cost.
11. Record expenses.
12. See profit.
13. Know what is due today.
14. Receive reminders.
15. Receive WhatsApp alerts.
16. Work comfortably from a mobile phone.
17. Trust that the data is protected.

---

# CURRENT PROJECT STATE

Update this section after every verified phase.

```text
Current Phase: PHASE 0
Status: NOT STARTED

Last Verified Phase: NONE

Next Phase: PHASE 0

Last Verification Date: YYYY-MM-DD

Known Blockers:
- None
```

END OF MASTER PLAN
