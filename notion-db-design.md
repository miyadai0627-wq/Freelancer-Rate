# Freelancer Business OS — Notion Database Design

> All property names are in English (targeting the English-speaking market).

---

## Architecture Overview

```
CLIENTS ──┬── PROJECTS ──── TASKS
           │         │
           └── INVOICES ──── TRANSACTIONS ──── CATEGORIES
                                                    │
                              SUBSCRIPTIONS ────────┘
```

5 Core DBs + 2 Support DBs = 7 databases total.

---

## 1. 🤝 Clients (CRM)

| Property | Type | Description |
|----------|------|-------------|
| **Client Name** | Title | Company or client name |
| **Status** | Select | `🟢 Active` / `🟡 Lead` / `🔵 Prospect` / `⚪ Past` |
| **Contact Name** | Text | Point of contact |
| **Email** | Email | Contact email |
| **Phone** | Phone | Phone number |
| **Website** | URL | Client's website |
| **Industry** | Select | `Tech` / `Marketing` / `E-commerce` / `Healthcare` / `Education` / `Other` |
| **Source** | Select | `Referral` / `Cold Outreach` / `Upwork` / `LinkedIn` / `Website` / `Other` |
| **Hourly Rate** | Number ($) | Agreed rate with this client |
| **Notes** | Text | Preferences, reminders |
| **Projects** | Relation → Projects | Linked projects |
| **Invoices** | Relation → Invoices | Linked invoices |
| **Total Revenue** | Rollup (Invoices → Amount, SUM) | Lifetime revenue from this client |
| **Active Projects** | Rollup (Projects → Status=Active, COUNT) | Number of active projects |
| **Created** | Created time | Date added |

### Views
- **All Clients** — Table, sort by Status → Name
- **Pipeline** — Board, group by Status
- **Top Clients** — Table, sort by Total Revenue (desc)

---

## 2. 📋 Projects

| Property | Type | Description |
|----------|------|-------------|
| **Project Name** | Title | Name of the project |
| **Client** | Relation → Clients | Associated client |
| **Status** | Select | `📝 Proposal` / `🟢 Active` / `⏸ On Hold` / `✅ Completed` / `❌ Cancelled` |
| **Priority** | Select | `🔴 High` / `🟡 Medium` / `🟢 Low` |
| **Type** | Select | `Fixed Price` / `Hourly` / `Retainer` / `Pro Bono` |
| **Budget** | Number ($) | Total project budget |
| **Start Date** | Date | Project start |
| **Deadline** | Date | Due date |
| **Estimated Hours** | Number | Estimated work hours |
| **Actual Hours** | Rollup (Tasks → Hours Logged, SUM) | Actual hours from tasks |
| **Tasks** | Relation → Tasks | Linked tasks |
| **Invoices** | Relation → Invoices | Linked invoices |
| **Revenue** | Rollup (Invoices → Amount, SUM) | Total revenue for this project |
| **Progress** | Formula | `Tasks Completed / Total Tasks × 100` |
| **Days Until Deadline** | Formula | `dateBetween(prop("Deadline"), now(), "days")` |
| **Notes** | Text | Project notes |

### Views
- **Kanban Board** — Board, group by Status
- **Timeline** — Timeline, Start Date → Deadline
- **Active Projects** — Gallery, filter Status = Active
- **By Client** — Table, group by Client

---

## 3. ✅ Tasks

| Property | Type | Description |
|----------|------|-------------|
| **Task** | Title | Task name |
| **Project** | Relation → Projects | Associated project |
| **Status** | Status | `Not Started` / `In Progress` / `Blocked` / `Done` |
| **Priority** | Select | `🔴 Urgent` / `🟡 Important` / `🟢 Normal` / `⚪ Low` |
| **Assignee** | Person | Assigned team member |
| **Due Date** | Date | Task deadline |
| **Hours Logged** | Number | Time spent (manual or timer) |
| **Tags** | Multi-select | `Design` / `Development` / `Writing` / `Admin` / `Meeting` / `Review` |
| **Notes** | Text | Task notes |
| **Completed Date** | Date | Completion date |

### Views
- **Board** — Board, group by Status
- **My Tasks** — Table, filter Assignee = Me, sort by Due Date
- **This Week** — Calendar, Due Date
- **Eisenhower Matrix** — Board, group by Priority

---

## 4. 💰 Invoices

| Property | Type | Description |
|----------|------|-------------|
| **Invoice #** | Title | Invoice number (e.g. `INV-2025-001`) |
| **Client** | Relation → Clients | Billed client |
| **Project** | Relation → Projects | Associated project |
| **Status** | Select | `📝 Draft` / `📤 Sent` / `⏳ Overdue` / `✅ Paid` / `❌ Cancelled` |
| **Amount** | Number ($) | Invoice amount |
| **Tax Amount** | Formula | `prop("Amount") × 0.25` |
| **Net After Tax** | Formula | `prop("Amount") - prop("Tax Amount")` |
| **Issue Date** | Date | Date issued |
| **Due Date** | Date | Payment due date |
| **Paid Date** | Date | Date payment received |
| **Days Overdue** | Formula | `if(prop("Status")=="⏳ Overdue", dateBetween(now(), prop("Due Date"),"days"), 0)` |
| **Payment Method** | Select | `Bank Transfer` / `PayPal` / `Stripe` / `Wise` / `Other` |
| **Notes** | Text | Memo |
| **Transactions** | Relation → Transactions | Linked payment records |

### Views
- **All Invoices** — Table, sort by Issue Date (desc)
- **Pipeline** — Board, group by Status
- **Overdue** — Table, filter Status = Overdue
- **Monthly Summary** — Table, group by Month

---

## 5. 📊 Transactions (Financial Tracker)

> **Most important DB.** Tracks actual income and expenses against the target hourly rate from the simulator.

| Property | Type | Description |
|----------|------|-------------|
| **Description** | Title | Transaction description |
| **Type** | Select | `💚 Income` / `🔴 Expense` |
| **Amount** | Number ($) | Amount |
| **Category** | Relation → Categories | Classification |
| **Date** | Date | Transaction date |
| **Invoice** | Relation → Invoices | Linked invoice (for income) |
| **Payment Method** | Select | `Bank` / `PayPal` / `Stripe` / `Cash` / `Credit Card` |
| **Is Recurring** | Checkbox | Recurring expense flag |
| **Receipt** | Files & Media | Receipt image |
| **Tax Deductible** | Checkbox | Tax deductible flag |
| **Notes** | Text | Memo |

### Dashboard Formulas (at page level)

```
Monthly Revenue   = SUM(Amount) WHERE Type = Income AND Date = This Month
Monthly Expenses  = SUM(Amount) WHERE Type = Expense AND Date = This Month
Monthly Profit    = Revenue - Expenses
Tax Vault (25%)   = Monthly Revenue × 0.25
Net Take-Home     = Monthly Revenue - Monthly Expenses - Tax Vault
YTD Revenue       = SUM(Amount) WHERE Type = Income AND Date = This Year
```

### Views
- **All Transactions** — Table, sort by Date (desc)
- **Income Only** — Table, filter Type = Income
- **Expenses Only** — Table, filter Type = Expense
- **Monthly Overview** — Table, group by Month
- **Tax Deductible** — Table, filter Tax Deductible = ✓

---

## 6. 🏷 Categories (Master)

| Property | Type | Description |
|----------|------|-------------|
| **Category Name** | Title | Category name |
| **Type** | Select | `Income` / `Expense` |
| **Icon** | Text | Emoji icon |
| **Transactions** | Relation → Transactions | Linked transactions |
| **Total** | Rollup (Transactions → Amount, SUM) | Total for this category |

### Preset Categories

**Income:** `Client Work` / `Digital Products` / `Consulting` / `Affiliate` / `Other Income`

**Expense:** `Software & Tools` / `Hardware` / `Marketing` / `Education` / `Co-working` / `Communication` / `Insurance` / `Travel` / `Professional Services` / `Other Expense`

---

## 7. 🔄 Subscriptions

| Property | Type | Description |
|----------|------|-------------|
| **Service Name** | Title | Service name |
| **Status** | Select | `🟢 Active` / `⏸ Paused` / `❌ Cancelled` |
| **Cost** | Number ($) | Amount |
| **Billing Cycle** | Select | `Monthly` / `Quarterly` / `Annually` |
| **Monthly Cost** | Formula | See below |
| **Annual Cost** | Formula | `prop("Monthly Cost") × 12` |
| **Category** | Relation → Categories | Classification |
| **Renewal Date** | Date | Next renewal date |
| **URL** | URL | Service URL |
| **Essential** | Checkbox | Business-essential flag |
| **Notes** | Text | Memo |

### Monthly Cost Formula

```
if(prop("Billing Cycle") == "Monthly", prop("Cost"),
  if(prop("Billing Cycle") == "Quarterly", prop("Cost") / 3,
    if(prop("Billing Cycle") == "Annually", prop("Cost") / 12, 0)))
```

### Views
- **Active Subscriptions** — Table, filter Status = Active
- **By Category** — Table, group by Category
- **Cost Overview** — Table, sort by Monthly Cost (desc)

---

## Relation Map

| From | → To | Type | Purpose |
|------|-------|------|---------|
| Projects | → Clients | Many-to-One | Project ↔ Client link |
| Tasks | → Projects | Many-to-One | Task ↔ Project link |
| Invoices | → Clients | Many-to-One | Invoice ↔ Client link |
| Invoices | → Projects | Many-to-One | Invoice ↔ Project link |
| Transactions | → Invoices | Many-to-One | Payment ↔ Invoice link |
| Transactions | → Categories | Many-to-One | Transaction ↔ Category |
| Subscriptions | → Categories | Many-to-One | Subscription ↔ Category |

---

## Implementation Priority

| Phase | DB | Reason |
|-------|----|--------|
| **Phase 1** | Categories → Transactions | Financial tracking is the #1 selling point |
| **Phase 2** | Clients → Projects | CRM and project management |
| **Phase 3** | Tasks | Project task breakdown |
| **Phase 4** | Invoices | Billing (links to Transactions) |
| **Phase 5** | Subscriptions | Fixed cost visibility |
| **Final** | Dashboard | Top page aggregating all DBs |

---

## Dashboard Layout

```
┌────────────────────────────────────────────────────────┐
│  🚀 Freelancer Business OS                             │
│  Welcome back! Here's your business at a glance.       │
├─────────────────────┬──────────────────────────────────┤
│  📊 Revenue MTD     │  💰 Profit MTD                   │
│     $X,XXX          │     $X,XXX                       │
├─────────────────────┼──────────────────────────────────┤
│  🏦 Tax Vault       │  📈 YTD Revenue                  │
│     $X,XXX          │     $XX,XXX                      │
├─────────────────────┴──────────────────────────────────┤
│  ⚡ Rate Simulator Widget (Embedded via GitHub Pages)  │
├────────────────────────────────────────────────────────┤
│  📋 Active Projects          ✅ My Tasks This Week     │
├────────────────────────────────────────────────────────┤
│  💳 Invoices Awaiting Payment    🔄 Subscriptions      │
└────────────────────────────────────────────────────────┘
```
