# Telecom Account Management - README

This project is a **MERN Stack** (MongoDB, Express, React, Node.js) web application for a telecom service provider. It enables customers to manage their accounts, view billing statements, make payments, update personal information, track data usage, and request support — all in one platform.

---

## Table of Contents

1. [Project Overview](#project-overview)
2. [Microservices & Modules](#microservices--modules)
3. [API Endpoints](#api-endpoints)
   - [Authentication & Settings](#1-authentication--settings)
   - [Personal Information & Account Overview](#2-personal-information--account-overview)
   - [Support & Chatbot](#3-support--chatbot)
   - [Data Usage & Plan Management](#4-data-usage--plan-management)
   - [Payment & Transactions](#5-payment--transactions)
4. [Setup & Installation](#setup--installation)
5. [Folder Structure](#folder-structure)
6. [License](#license)

---

## Project Overview

This application addresses the following main objectives:

- **Account Management**: Secure login, account overviews, personal info edits.
- **Billing & Payments**: Billing statements, transaction history, and multiple payment methods.
- **Data Usage**: Real-time and historical usage tracking.
- **Support**: Ticket-based customer support and an FAQ chatbot.
- **Notifications**: In-app alerts for account events (payments, plan changes, etc.).

It covers 16 functional requirements (FR-1 to FR-16), including user registration, plan management, notifications, and support ticketing.

---

## Microservices & Modules

To ensure modular and maintainable development, the system is divided into five main modules (microservices):

1. **Authentication & Settings**
2. **Personal Information & Account Overview**
3. **Support & Chatbot**
4. **Data Usage & Plan Management**
5. **Payment & Transactions**

Each module can be developed as a separate Node.js service (or combined as needed) and integrated via REST APIs.

---

## API Endpoints

### 1. Authentication & Settings

| Endpoint                         | HTTP    | Description                                                                                       |
|----------------------------------|---------|---------------------------------------------------------------------------------------------------|
| `/auth/register`                 | POST    | Registers a new user (mobile/email, name, password, security question, etc.).                    |
| `/auth/login`                    | POST    | Authenticates user (or admin) and returns a session token/JWT.                                   |
| `/auth/logout`                   | POST    | Invalidates the current session token.                                                           |
| `/auth/forgot-password`          | POST    | Initiates password reset (verify mobile/security question).                                      |
| `/auth/reset-password`           | POST    | Resets the password after verification.                                                          |
| `/settings`                      | GET     | Retrieves user’s account settings (notification preferences, theme, etc.).                       |
| `/settings`                      | PUT     | Updates user’s account settings (notification prefs, theme, etc.).                               |
| `/settings/change-password`      | PATCH   | Changes the user’s password (requires old password or a valid session).                          |
| `/settings/account`              | DELETE  | Deactivates or deletes the user’s own account.                                                   |
| `/notifications`                 | GET     | Retrieves in-app notifications (filtered by user if user role, or all if admin role).            |
| `/notifications/:id/mark-read`   | PATCH   | Marks a specific notification as read.                                                           |

#### Role-based Logic:
- **User**: Can only manage their own settings and notifications.
- **Admin**: Can manage system-level settings or retrieve notifications for any user.

---

### 2. Personal Information & Account Overview

| Endpoint                         | HTTP    | Description                                                                                       |
|----------------------------------|---------|---------------------------------------------------------------------------------------------------|
| `/account`                       | GET     | Shows account overview (mobile #, status, plan type, etc.).                                      |
| `/account/plan`                  | GET     | Displays current plan details (name, validity, remaining data/SMS/talktime).                     |
| `/account/personal-info`         | GET     | Returns user’s personal info (email, address, alt mobile, etc.).                                 |
| `/account/personal-info`         | PUT     | Updates personal info (address, alt mobile, etc.).                                               |

#### Role-based Logic:
- **User**: Sees and updates their own account.
- **Admin**: May retrieve or modify any user’s account if permitted.

---

### 3. Support & Chatbot

| Endpoint                         | HTTP    | Description                                                                                       |
|----------------------------------|---------|---------------------------------------------------------------------------------------------------|
| `/support/tickets`               | GET     | Retrieves all support tickets for the logged-in user (or all if admin).                          |
| `/support/tickets`               | POST    | Creates a new support ticket.                                                                    |
| `/support/tickets/:ticketId`     | GET     | Fetches details of a specific support ticket.                                                    |
| `/support/tickets/:ticketId`     | PATCH   | Updates the ticket (add notes, change status, etc.).                                             |
| `/chatbot/query`                 | POST    | Submits a user query to the FAQ chatbot; returns an automated response.                          |
| `/chatbot/faq`                   | GET     | Retrieves frequently asked questions (static or dynamic).                                        |

#### Role-based Logic:
- **User**: Can only see and modify their own tickets.
- **Admin**: Can see and update all tickets (e.g., escalations).

---

### 4. Data Usage & Plan Management

| Endpoint                         | HTTP    | Description                                                                                       |
|----------------------------------|---------|---------------------------------------------------------------------------------------------------|
| `/usage`                         | GET     | Shows current usage stats (data, SMS, voice calls) for the logged-in user.                       |
| `/usage/history`                 | GET     | Retrieves historical usage data (daily/monthly breakdown).                                       |
| `/plans`                         | GET     | Lists available prepaid and postpaid plans with pricing details.                                 |
| `/plans/:planId`                 | GET     | Gets details of a single plan.                                                                   |
| `/plans/change`                  | POST    | Switches the user’s current plan to a new one (prepaid or postpaid).                             |
| `/plans/top-up`                  | POST    | (Prepaid) Adds talktime, data packs, or roaming packs.                                           |
| `/plans/upgrade`                 | PATCH   | (Postpaid) Upgrades the user’s plan (more connections, higher data, etc.).                       |

#### Role-based Logic:
- **User**: Changes their own plan and sees their own usage.
- **Admin**: Manages plan offerings (create/update/delete) or views any user’s usage if permitted.

---

### 5. Payment & Transactions

| Endpoint                         | HTTP    | Description                                                                                       |
|----------------------------------|---------|---------------------------------------------------------------------------------------------------|
| `/billing`                       | GET     | Retrieves current billing info (due dates, amounts, billing cycle).                              |
| `/billing/statements`            | GET     | Lists all past billing statements for the logged-in user.                                        |
| `/billing/statements/:id/download`| GET     | Downloads a specific statement as a PDF.                                                        |
| `/transactions`                  | GET     | Returns the user’s transaction history (or all if admin).                                        |
| `/transactions/:transactionId`   | GET     | Gets details of a specific transaction.                                                          |
| `/transactions`                  | POST    | Makes a payment (select credit/debit/UPI).                                                       |
| `/transactions/:transactionId/cancel`| PATCH | Cancels or reverses a pending transaction (if business logic allows).                            |

#### Role-based Logic:
- **User**: Can only access their own billing/transactions.
- **Admin**: May view or manage all user transactions for auditing/refunds if allowed.

---

## Setup & Installation

### Clone the Repository

```bash
git clone https://github.com/YourOrg/telecom-account-management.git
