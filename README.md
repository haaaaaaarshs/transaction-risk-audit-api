# Transaction Risk & Audit API

## Overview

A backend API that simulates transaction processing, automated risk assessment, flagged transaction review, and audit logging.

This project is inspired by concepts I encountered while completing software engineering and finance-focused Forage simulations, particularly transaction processing, backend system design, data workflows, and risk review.

## Why I Am Building This

I have completed several technical simulations and wanted to move beyond guided tasks by building a backend system independently from the ground up.

My main goals are to:

- design a relational database
- build REST API endpoints
- implement business logic beyond basic CRUD
- work with transaction state changes
- create a simple risk-scoring system
- implement audit logging
- write automated tests
- better understand how backend components work together

## Planned Tech Stack

- Node.js
- TypeScript
- Express
- PostgreSQL
- Prisma ORM
- Jest

## Planned Core Features

### Users and Accounts
- Customer and admin roles
- Multiple accounts per user
- Account balances

### Transactions
- Transfers between accounts
- Transaction status lifecycle
- Balance validation

### Risk Assessment
- Automated transaction risk scoring
- Low, medium, and high risk levels
- Stored reasons for flagged transactions

### Admin Review
- View flagged transactions
- Approve or reject transactions

### Audit Logging
- Record important system actions and status changes

## Planned Transaction Lifecycle

Created → Risk Assessment

Low Risk → Approved → Settled

High Risk → Flagged → Admin Review → Approved or Rejected

## Planned Database Design

The initial database will use five main models: `User`, `Account`, `Transaction`, `RiskAssessment`, and `AuditLog`.

### User

Represents a person who can own accounts or review flagged transactions.

Planned fields:

- `id` — unique identifier
- `name` — user's name
- `email` — unique email address
- `role` — `CUSTOMER` or `ADMIN`
- `createdAt`
- `updatedAt`

A user can own multiple accounts.

### Account

Represents an account that can send or receive transactions.

Planned fields:

- `id` — unique identifier
- `userId` — owner of the account
- `accountNumber` — unique account number
- `type` — `CHECKING` or `SAVINGS`
- `balance`
- `currency`
- `createdAt`
- `updatedAt`

Each account belongs to one user. An account can send and receive many transactions.

### Transaction

Represents a transfer between two accounts.

Planned fields:

- `id` — unique identifier
- `senderAccountId`
- `receiverAccountId`
- `amount`
- `currency`
- `memo` — optional transaction description
- `status`
- `createdAt`
- `updatedAt`
- `settledAt` — optional timestamp

Planned transaction statuses:

- `PENDING`
- `APPROVED`
- `FLAGGED`
- `REJECTED`
- `SETTLED`

A transaction has one sender account, one receiver account, and one risk assessment.

### RiskAssessment

Stores the result of the automated risk check for a transaction.

Planned fields:

- `id` — unique identifier
- `transactionId`
- `score` — numerical risk score
- `level` — `LOW`, `MEDIUM`, or `HIGH`
- `reasons` — explanations for why risk points were added
- `createdAt`

Each transaction will have one risk assessment.

### AuditLog

Records important actions and state changes in the system.

Planned fields:

- `id` — unique identifier
- `transactionId` — optional related transaction
- `actorUserId` — optional user responsible for the action
- `action`
- `details`
- `createdAt`

Audit logs will record events such as transaction creation, risk assessment, flagging, approval, rejection, settlement, and balance updates.

### Model Relationships

- One `User` can own many `Account` records.
- One `Account` can send many `Transaction` records.
- One `Account` can receive many `Transaction` records.
- One `Transaction` has one `RiskAssessment`.
- One `Transaction` can have many `AuditLog` records.
- One admin `User` can be associated with multiple review actions.

## Planned API Endpoints

The API will be organized around users, accounts, transactions, admin review, and audit logs.

### Users

#### `POST /api/users`

Create a new user.

#### `GET /api/users/:id`

Retrieve a user and their basic account information.

### Accounts

#### `POST /api/accounts`

Create an account for an existing user.

#### `GET /api/accounts/:id`

Retrieve account details.

#### `GET /api/users/:userId/accounts`

Retrieve all accounts owned by a user.

### Transactions

#### `POST /api/transactions`

Create a transfer between two accounts.

Creating a transaction will also trigger the automated risk assessment process.

#### `GET /api/transactions/:id`

Retrieve a transaction along with its status and risk assessment.

#### `GET /api/accounts/:accountId/transactions`

Retrieve transactions sent or received by an account.

### Admin Review

#### `GET /api/admin/transactions/flagged`

Retrieve transactions waiting for manual review.

#### `PATCH /api/admin/transactions/:id/approve`

Approve a flagged transaction.

#### `PATCH /api/admin/transactions/:id/reject`

Reject a flagged transaction.

### Audit Logs

#### `GET /api/transactions/:id/audit-logs`

Retrieve the recorded history of a transaction.

### Health Check

#### `GET /api/health`

Confirm that the API server is running.

## Development Progress

### Phase 1 — Planning
- [x] Defined project purpose
- [x] Selected initial tech stack
- [x] Defined core features
- [x] Design database schema
- [x] Define API endpoints

### Phase 2 — Project Setup
- [ ] Initialize Node.js and TypeScript project
- [ ] Configure Express
- [ ] Configure PostgreSQL and Prisma
- [ ] Create initial database migration

### Phase 3 — Core Backend
- [ ] Build user and account functionality
- [ ] Build transaction creation flow
- [ ] Implement transaction status lifecycle

### Phase 4 — Risk and Audit Systems
- [ ] Implement risk-scoring rules
- [ ] Implement flagged transaction review
- [ ] Implement audit logging

### Phase 5 — Testing and Documentation
- [ ] Add automated tests
- [ ] Test complete API flow
- [ ] Add API examples
- [ ] Final README polish

## Development Journal

### Project Start

I started this project to turn concepts from my Forage simulations into a backend system that I designed and built myself.

Before writing code, I am defining the project's scope, data model, and transaction workflow so that the implementation has a clear structure instead of growing feature by feature without a plan.

### Database Planning

I decided to separate the system into five main models: User, Account, Transaction, RiskAssessment, and AuditLog.

The main design decision I considered was whether risk information should be stored directly on each transaction or in its own model. I chose a separate RiskAssessment model because the transaction should represent the transfer itself, while the risk assessment represents an analysis performed on that transaction.

I also decided to keep audit logs separate from transactions so that multiple events can be recorded throughout a transaction's lifecycle instead of storing only its current state.

### API Planning

After defining the database models, I planned the initial API routes around the main actions the system needs to support.

I separated normal transaction activity from admin review endpoints because approving or rejecting flagged transactions represents a different level of access and responsibility.

I also included an endpoint for viewing a transaction's audit history so that the system can show not only the transaction's current status, but also the sequence of events that led to it.