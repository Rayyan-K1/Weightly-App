# Weightly – Easy GLP-1 Tracker

**Weightly** is a full-stack web app made by me (front-end and back-end) that helps people on GLP-1 medications (Ozempic, Wegovy, Mounjaro, Tirzepatide, Zepbound, etc.) track their weight, injections, side effects, and daily health metrics in one place.

> 📌 This repository is a **case study** of the product & engineering behind Weightly.  
> The production source code is private for commercial and IP reasons.

---

## Live App

- [iOS App Store] (https://apps.apple.com/us/app/weightly-mounjaro-tracker/id6743134664)
- [Google Play] (https://play.google.com/store/apps/details?id=com.bilaal5279.weightly&hl=en)
---

## Feature Overview

### Weight tracking & analytics

- Time-series chart of weight with smooth curve and labels.
- Key metrics:
  - Current weight
  - BMI
  - Weekly average
  - 1-month progress
  - Total change since starting treatment
- Goal tab for tracking progress against a target weight.

### Health diary

- Calendar-based **Health Diary** to log each day.
- Per-day cards for:
  - Steps
  - Calories
  - Protein and other macros
  - Heart rate
  - Notes / symptoms
- Optimised for very fast data entry.

### GLP-1 shot tracking

- **Shots history** grouped by month.
- For each shot:
  - Medication name (e.g. Mounjaro, Tirzepatide)
  - Dose (mg)
  - Date & time
  - Injection site
- Used by users to keep an accurate medication record.

### Medication dashboard

- **Weight Loss Analytics** – how weight responds over time to treatment.
- **Medication Levels** – tracks dosage strength and timing.
- **Side Effects Monitor** – log and review side effects.
- **Picture Diary** – upload photos over time to visually track progress.

### Reminders, feedback & settings

- Shot reminders.
- In-app feedback:
  - Report a problem
  - Request a feature
  - Rate the app
- Appearance & format settings.
- Legal: Terms of Service, Privacy Policy.

---

## Tech Stack

**Frontend**

- React
- React Router (multi-page navigation)
- Custom charting UI for analytics
- Responsive layout + dark theme

**Backend**

- Node.js
- Express.js (HTTP API + routing)
- MySQL (relational database)
- Bcrypt (password hashing / sensitive data protection)
- Node clustering for natural load balancing across CPU cores

**Data & communication**

- RESTful HTTP APIs
- JSON payloads
- `POST`/`GET` endpoints for weight entries, diary logs, injections, photos, and user auth

**Auth & security**

- Email/password auth (hashed with bcrypt)
- Third-party login:
  - Sign in with Apple
  - Sign in with Google
- Input validation and server-side checks
- Role-ready model (easy to extend to admin/clinician views)

**Observability / logging**

- Centralised **audit logging**:
  - Page transitions
  - CRUD actions (create/update/delete entries)
  - Timestamps and user IDs
- Structured logs used for debugging, funnel analysis, and product decisions.

---

## Architecture (High-Level)

Weightly follows a classic **React + Node/Express + MySQL** architecture, designed for scalability and maintainability.

```mermaid
graph TD
  U[User Browser / Mobile WebView] --> R[React Frontend]
  R -->|HTTP JSON (POST/GET)| A[Node.js + Express API]
  A -->|SQL Queries| DB[(MySQL Database)]
  A --> L[Audit Logger]

  subgraph Backend
    A
    L
    C[Node Cluster (multiple workers)]
  end
