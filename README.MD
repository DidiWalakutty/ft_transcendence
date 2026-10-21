# 🎟️ Eventra

**Eventra** is a full-stack event platform developed by a four-person team as part of the 42/Codam curriculum.

Users can discover and register for events, create and manage events, connect with friends, chat in real time, and manage their profiles. Administrators can manage users and events through a dedicated dashboard.

![Eventra Homepage](apps/frontend/src/assets/Eventra%20Homepage.png)

## My role

**Product Owner & Developer**

As Product Owner, I was responsible for product direction, backlog priorities, acceptance criteria, and validating completed features.

As a developer, I primarily worked on:

- **Event discovery:** Event catalogue, server-side filtering, sorting, pagination, event cards, and event detail pages.
- **Ticketing:** Event registration and cancellation
- **User experience:** Landing page, navigation, and accessibility improvements.
- **Internationalisation:** English and Dutch localisation.
- **Content and compliance:** Privacy Policy and Terms of Service pages.

### A technical problem I solved

We identified a race condition where two users could attempt to register for the final available ticket simultaneously.

I moved the capacity check into a database transaction and added database constraints to enforce ticket-registration integrity. These safeguards prevent events from exceeding their capacity and users from holding multiple active registrations for the same event.

This was an important example of handling concurrent requests and enforcing business rules at the database level, rather than relying solely on application-level checks.

---

## ✨ Features

- **Event management:** Create, update, and manage events, including capacity limits.
- **Event discovery:** Search and browse events with filtering, sorting, and pagination.
- **Ticket registration:** Register for and cancel event attendance, with capacity and uniqueness constraints.
- **Social features:** User profiles, avatars, friend requests, online status, and real-time chat.
- **Notifications:** In-app notifications and email.
- **Authentication:** User authentication and TOTP-based two-factor authentication.
- **Administration:** Dedicated dashboard for managing users and events.
- **Accessibility & localisation:** Accessibility improvements informed by WCAG 2.1 AA and support for English, Dutch, and Spanish.
- **Rendering & deployment:** Server-side rendering and Docker-based deployment with HTTPS.

---

## 🏗️ Technical architecture
The application separates the frontend, backend, and data services, with Caddy handling HTTPS and reverse proxying.

```text
                         Browser
                            │
                       HTTPS / Caddy
                            │
              ┌─────────────┴─────────────┐
              │                           │
        React Frontend              NestJS Backend
       TanStack Start                  tRPC
                                          │
                              ┌───────────┼───────────┐
                              │           │           │
                         PostgreSQL     Redis        SSE
```

### Technology Stack

| Layer | Technologies |
| ----- | ------------ |
| Frontend | React 19, TanStack Start, TanStack Router, TanStack Query, TanStack Form, TypeScript |
| UI | Tailwind CSS, shadcn/ui |
| Backend | NestJS 11, tRPC, Zod, TypeScript |
| Database | PostgreSQL 17, Drizzle ORM |
| Infrastructure | Docker, Docker Compose, Caddy, Redis | 
| Authentication | better-auth, TOTP |
| Testing | Vitest, Playwright |
| Quality & CI | Typescript type checking, linting, formatting, GitHub Actions| 

---

## 🗄️Database Design

The application uses PostgreSQL with Drizzle ORM.

The main data model covers:

* Users and sessions
* Events and organisers
* Event registrations
* Friendships
* Two-factor authentication
* User profiles

Data integrity is enforced through foreign keys, transactions, enums, and partial unique indexes.

For example, a partial unique index on (event_id, user_id) for active registrations prevents a user from holding multiple active tickets for the same event.

See [`docs/DATABASE.md`](./docs/DATABASE.md) for the full schema and additional details.

---

## Testing & quality

The project includes:

* Unit tests with **Vitest**
* End-to-end tests with **Playwright**
* Chromium and Firefox testing
* TypeScript type checking
* Linting and formatting
* CI checks through GitHub Actions

---

## Documentation

Further technical documentation is available in [`docs/`](./docs/):
| Document | Description |
| ------------- | ------------------------- |
| [Stack](./docs/STACK.md) | Architecture and technology choices |
| [Database](./docs/DATABASE.md) | Schema and database design |
| [Development](./docs/DEVELOPMENT.md) | Development workflow and commands |
| [Authentication](./docs/AUTHENTICATION.md) | Authentication architecture |
| [Environment](./docs/ENVIRONMENT.md) | Environment configuration |
| [Browser Support](./docs/BROWSER_SUPPORT.md) | Browser compatibility |
| [Prerequisites](./docs/PREREQUISITES.md) | Setup requirements |
| [Tooling](./docs/TOOLING.md) | Available development commands |

---

## 🚀 Running the project

### Prerequisites

* Docker Engine 20.10+
* Docker Compose v2

### Start

```bash
docker compose up --build
```

Then open:

```text
https://localhost:3000
```

The development setup and available commands are documented in [`docs/DEVELOPMENT.md`](./docs/DEVELOPMENT.md).

---

## 👥 Team & Collaboration

Eventra was developed as a four-person team as part of the 42/Codam curriculum.

| Role       | Login                    | Responsibilites    |
| ------------- | ------------------------- | ------------------- |
|Product Owner|	diwalaku|	Product vision, backlog priorities, acceptance criteria, validation of finished work.|
|Project Manager|	ccraciun|	Coordination, blockers, milestones and timelines, keeping the team in sync.|
|Technical Lead / Architect|	mde-krui|	Stack decisions, code-quality standards, pull-request reviews, architecture across the three tiers.|


The team used GitHub Projects, feature branches, pull requests, code review, CI, and asynchronous communication.

---

## Original project

This repository is my personal fork of the [original team project](https://github.com/milandekruijf/ft_transcendence).

Original team members:

* [mde-krui](https://github.com/milandekruijf)
* [diwalaku](https://github.com/DidiWalakutty)
* [ccraciun](https://github.com/corinbz)
* [rtorrent](https://github.com/R-Torrent)

