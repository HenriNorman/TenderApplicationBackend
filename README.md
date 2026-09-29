# 📋 Tendering API

A RESTful backend API for a B2B tendering platform, built with **Django REST Framework**.  
It lets companies post tenders, vendors submit bids, and admins review, approve, and evaluate — with a stats dashboard for oversight.

[![Frontend](https://img.shields.io/badge/frontend-TenderingDU-blue)](https://github.com/TheAtef/TenderingDU)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)

> ⚠️ **Project status:** Active development. Not yet deployed. See [Roadmap](#-roadmap) and [Known Issues](#-known-issues).

---

## 📖 Overview

This API powers a B2B tendering platform that connects **demand** (companies needing goods or services) with **supply** (vendors able to provide them). It covers the full tendering lifecycle:

**account verification → tender creation → admin approval → bid submission → evaluation → payment**

The backend follows REST principles with stateless JWT authentication and enforces strict role separation between `user` and `admin`.

The **frontend is implemented in a separate repository** — see [TenderingDU](https://github.com/TheAtef/TenderingDU) (Flutter mobile app + web UI).

---

## ✨ Features

### ✅ Implemented

- **Full tendering lifecycle** — create → approve → bid → evaluate → pay
- **Domain modeling:**
  - `Tender` — posted by users, requires admin approval before visibility
  - `Bid` — submitted against approved tenders, includes budget & deliverables
  - `BidDocument` — supporting files attached to bids
  - `Evaluation` — quality score computed from submitted documents
  - `TenderPayment`, `Currency`, `Status` — payment & lifecycle state
- **Account verification flow** — users cannot access the system until an admin approves their account
- **Admin gating** — tenders require admin review before becoming publicly visible
- **Quality-based bid evaluation** — score is calculated from attached documents  
  _(scoring logic partially implemented — see [Known Issues](#-known-issues))_
- **Admin dashboard** — aggregate statistics on tenders, bids, and users
- **JWT authentication** + **role-based access control** (`user` / `admin`)
- **Request validation** on all endpoints
- **Normalized relational schema** — see [Database Schema](#-database-schema)
- **RESTful architecture** — resource-oriented routes, standard HTTP verbs and status codes
- **Companion frontend** — Flutter mobile app + web UI in [TenderingDU](https://github.com/TheAtef/TenderingDU)

### 🚧 Planned / In Progress

- [ ] **Real payment gateway** — currently a simulation only
- [ ] **Security headers** (CSP, HSTS, X-Frame-Options, etc.)
- [ ] **Complete evaluation scoring** — quality measure from bid documents
- [ ] **Notifications system** — in-app alerts for bid status, approvals, etc.
- [ ] **Arabic / English localization**
- [ ] **Light / dark theme** (mobile)
- [ ] **Automated test suite**

---

## 🏗️ Architecture

The backend follows **Django's MVT architecture** on top of **Django REST Framework**. DRF serializers handle input validation and representation; business logic for approval workflows, evaluation scoring, and payment handling is kept out of views and organized into dedicated service/utility modules.


Admin-only operations (approve tender, ban user, review reports) are gated through DRF permission classes.

---

## 🧱 Tech Stack

| Layer | Technology |
|-------|------------|
| Backend | Django + Django REST Framework |
| Language | Python |
| Auth | JWT |
| Database | PostgreSQL |
| Mobile client | Flutter (Dart) — [TenderingDU](https://github.com/TheAtef/TenderingDU) |
| Admin UI | Django built-in admin |
| Architecture | REST, MVT + service layer |
---

### 📎Schema diagram

<img width="3100" height="1683" alt="Untitled(1)" src="https://github.com/user-attachments/assets/af2e6e03-c8c2-4414-8ee3-8acc742c2cbf" />

---

## 🚀 Getting Started

### Requirements

- Python 3.10+
- PostgreSQL
- pip / virtualenv
