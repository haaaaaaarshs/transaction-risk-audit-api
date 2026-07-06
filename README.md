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

## Development Progress

### Phase 1 — Planning
- [x] Defined project purpose
- [x] Selected initial tech stack
- [x] Defined core features
- [ ] Design database schema
- [ ] Define API endpoints

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
