# FeeView - Lagos School Fees
**An offline, one-page phone app that helps small low-fee private schools in Lagos track who has paid, who owes, and when to send reminders, so fee conversations with parents are clear instead of arguments.**

---

## ⚙️ Project Type Flags
- [ ] Exploratory Data Analysis (EDA)
- [ ] SQL Analysis / Querying
- [ ] Dashboard / Data Visualization
- [ ] Data Pipeline / ETL
- [ ] Predictive Modelling / Machine Learning
- [ ] Data Cleaning / Wrangling
- [ ] End-to-End (multiple of the above)
- [ ] Other: Problem discovery + AI-assisted web app prototype (Meta AI Academy capstone)

---

## Table of Contents
1. [Project Overview](#1-project-overview)
2. [Objectives](#2-objectives)
3. [Project Scope & Tools](#3-project-scope--tools)
4. [Repository Structure](#4-repository-structure)
5. [Project Workflow](#5-project-data-workflow)
6. [Data Model](#6-project-model)
7. [Features](#7-features)
8. [Testing & Metrics](#8-testing--metrics)
9. [Key Insights](#9-key-insights)
10. [Recommendations](#10-recommendations)
11. [Assumptions & Limitations](#11-assumptions--limitations)
12. [Future Enhancements](#12-future-enhancements)
13. [Deliverables](#13-deliverables)
14. [Author](#14-author)

---

## 1. Project Overview

**Context:** Small low-fee private schools (50-150 pupils) in Oshodi, Lagos, live with unpredictable cash flow. Fees are tracked in ruled notebooks with no receipts, no debt history and no reminders. When a parent says "I paid last term", the owner has no proof.

**Problem Statement:** Small private school owners in Oshodi struggle to track fee payments and recover debts because records live in notebooks, and existing school apps cost too much and need constant internet and a laptop.

**Approach:** I used the Meta AI Academy method: research the problem first, then build the smallest working prototype, then test it with real users. The prototype was built with AI tools and tested with school staff over WhatsApp.

**Outcome:** FeeView, a mobile-friendly tracker that works with no login, no backend and no internet. It shows each pupil's total fee, amount paid and balance, records payments, produces a shareable receipt, and prepares WhatsApp deadline reminders for parents.

---

## 2. Objectives

- **Primary Objective:** Give small schools a free, simple way to know who owes what, and prove what has been paid.
- **Secondary Objective 1:** Make recording a payment fast (about 10 seconds).
- **Secondary Objective 2:** Give parents a clear receipt they can screenshot, share on WhatsApp or print.
- **Secondary Objective 3:** Help staff remind parents politely as fee deadlines approach.

💡 Every feature in this project traces back to one of these objectives.

---

## 3. Project Scope & Tools

### Scope

| Dimension | Details |
|-----------|---------|
| **In Scope** | Pupil fee records, payment history, balances, status labels, receipts, term-week tracking, deadline reminder messages |
| **Out of Scope** | Official accounting, tax filing, money transfers, bank integration, user roles, cloud backup (see Limitations) |
| **Time Period** | One school term (Weeks 1-13) |
| **Granularity** | Per pupil, with payment-level history |

### Tools & Technologies 

| Category | Tool(s) Used |
|----------|-------------|
| Data Storage | Browser LocalStorage (on the phone only) |
| Bulid | AI app builder (Manus) - confirm before publishing |
| Research & Planning | Meta AI |
| Front end | One-page responsive web app, optimized for 375px Android screens |
| Messaging | WhatsApp click-to-chat links |
| Version Control | Git / GitHub |
| Documentation | Markdown |

---

## 4. Repository Structure

```
[FeeView/
│
├── app/                # Prototype source / build output
├── docs/
│   └── Meta AI Development Capstone Project.docx   # Problem, prototype and reflection
├── visuals/            # Screenshots of the app (375px mobile view)
└── README.md           # You are here
```
---


## 5. Project Workflow

```
[Problem Discovery: interviews & research in Oshodi]
                    ↓
[Problem Statement & Value Proposition]
                    ↓
[Prototype Plan (3-4 features) → Build]
                    ↓
[Test with 3 school staff via WhatsApp]
                    ↓
[Version 2: term start date & deadline reminders]

```

1. **Problem Discovery:** Mapped existing school apps (15+ in Nigeria at about N40k-N120k monthly) and why they fail small schools.
   
2. **Plan:** Kept the prototype to one main job and a few supporting features.

3. **Build:** One-page, mobile-first, offline app with sample data marked clearly.

4. **Test:** Three school staff tried it without training.

5. **Iterate:** Added term-week tracking and deadline reminders.

---

## 6. Data Model 
All data is stored locally in the browser. No real pupil data is included in this repository; the prototype ships with 5 sample pupils.

### Table: `Record: Pupil`

| Field Name | Description | Example Value |
|------------|-------------|---------------|
| `Pupil name` | Name of the pupil | [Non-sensitive example] |
| `Class`  | Class the pupil is in | Primary  |
| `Parent name`  | Used in reminder messages | [Non-sensitive example] |
| `Total fee` | Fee for the term (₦) | ₦110,000 |
| `Paid` | Sum of payments (₦) |   ₦30,000  |
| `Balance` | Total fee minus paid (₦)| ₦50,000 |
| `Status` | Paid / Owing / Partial (green / red / yellow) | Partial |

###Record: Payment

| Field | Description |
|-------|-------------|
| `Amount` | Amount paid (₦) |
| `Date` | Auto-filled, editable |

### Settings

| Field | Description |
|-------| ------------|
|`Term start date` | Set once; drives the current school week (1-13) |

---

## 7. Features

### Version 1: Fee tracker

- One-page responsive layout optimized for small Android phones
- 5 sample pupils pre-loaded with naira balances and status dots
- Search by pupil name or class
- Payment history and an Add Payment popup with instant balance updates
- Printable receipt, with a Share as Image fallback
- LocalStorage only: no login, backend, payment processing or internet needed

### Version 2: Deadline reminders
- One-time term start date setup
- Current school week indicator (Week 1-13)
- Yellow "Deadline approaching" label from Week 5
- Red "Deadline reached" label from Week 7
- Send deadline reminder" button that opens WhatsApp with the message ready
- Parent name, pupil name, balance and school name filled in automatically
- Safety note: reminders are not sent automatically; staff review and send each one

Verification: production build, route check, and 375px mobile screenshots.

---

## 8. Testing & Metrics
### Key Metrics Defined

| Metric | Plain-Language Definition | Why It Matters |
|--------|--------------------------|----------------|
|`Task completion` | Staff who finished search → add payment → show receipt unaided | Shows whether the app works without training |
|`Time to record payment`| Time to save a payment | Target is about 10 seconds |
|`Fees at risk`| Share of fees paid late or lost as bad debt | The size of the problem being solved |

### Problem sizing (from Oshodi research)
- For a 100-pupil school charging ₦110,000 per pupil:
- Expected per term: 100 × ₦110,000 = ₦11,000,000
- Paid late or lost (30-40%): ₦3.3M - ₦4.4M stuck every term
- Plus 6-8 hours every weekend spent calling parents
These figures come from my own interviews with school owners and are estimates, not audited numbers.

### Methods Used
- Interviews with school owners in Oshodi
- Mapping of existing solutions and their cost
- Remote usability test over WhatsApp with 3 school staff

---

## 9. Key Insights

**Insight 1: The barrier is cost and connectivity, not a lack of software** More than 15 school apps already exist, but small schools cannot afford them or rely on constant internet and a laptop.

**Insight 2: A simple flow works without training** All 3 staff completed search → add payment → show receipt on their own.

**Insight 3: The receipt solves the real argument** One tester said: "This will stop the argument at the gate."


---

## 10. Recommendations

| Priority | Recommendation | Based On | Suggested Owner |
|----------|---------------|----------|-----------------|
| High | Add Fee Summary by Class (Expected, Collected, Outstanding) | Owners need a quick view of money owed | Developer / me
| Medium | Test with more schools beyond the first 3 staff| Small test sample|Me
| Low | Explore a backup option | Data is lost if the phone is lost| Me

---

## 11. Assumptions & Limitations

### Assumptions
- Staff use an Android phone with WhatsApp installed.
- School owners enter fees and payments accurately.
- Parents respond to polite WhatsApp reminders

### Limitation: what FeeView should NOT be trusted with
- Official accounting, tax filing or audit-ready reports. It is not a replacement for an accountant.
- Long-term backup. Data lives on one phone; if the phone is lost, the data is lost.
- Handling money. It has no bank integration and does not process transfers.
- User roles. There is no login or separation between staff.
- Sensitive documents. Do not store parent ID documents in it.
- Automatic reminders. Reminders are never sent automatically; a person must tap and send.
- Small test sample. Only 3 staff tested it, so results are early evidence, not proof.
Prototype only: use sample data, not real pupils' details, in anything shared publicly.

---

## 12. Future Enhancements

- [ ] Fee Summary by Class: Expected, Collected, Outstanding for each class
- [ ] Backup and restore, so data survives a lost phone
- [ ] Wider testing with more schools and more staff

---

## 13. Deliverables
| Deliverable | Description | Location |
|-------------|-------------|----------|
| Freeview prototype | Offline one-page fee tracker with deadline reminders|[Add prototype link]|
| Capstone write-up | Problem, prototype, what it can't do, module reflection| /docs/Meta AI Development Capstone Project.docx |
| Screenshots | 375px mobile views of the app | /visuals/ |
---

## 14. Author

**[Your Name]**
[Your role or title - current or target]

- 🔗 [LinkedIn URL]
- 💼 [Portfolio or GitHub profile URL]
- 📧 [Email - optional]

---

*Last updated: [Month YYYY]*
*If this template helped you, consider starring the repository.*
