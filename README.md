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
4. [Functional Requirements Mapping](#functional-requirements-mapping)
5. [Setup & Installation](#setup--installation)
6. [Folder Structure](#folder-structure)
7. [License](#license)

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

For the other modules' API endpoints, functional requirements mapping, and detailed role-based logic, please refer to the full documentation in the project folder.

---

## Setup & Installation

### Clone the Repository

```bash
git clone https://github.com/YourOrg/telecom-account-management.git
