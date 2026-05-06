# OrderDesk

OrderDesk is a role-based order management app built for businesses that take orders through internal staff instead of a public storefront. It helps teams manage customers, products, orders, and staff access from one place.

## Overview

This project is designed for teams that handle sales manually through phone calls, messages, in-person interactions, or sales agents. It replaces scattered spreadsheets and informal order tracking with a structured workflow.

With OrderDesk, teams can:

- manage customers and product catalogs
- create and track orders
- control access by user role
- monitor activity from a central dashboard

## Who It's For

OrderDesk is a good fit for:

- wholesalers and distributors
- retail back-office teams
- internal sales teams
- businesses taking orders on WhatsApp, phone, or in person
- teams that need a lightweight alternative to a full ERP

## Core Features

- Secure credential-based login
- Role-based access control
- Dashboard with quick business stats
- Customer management
- Product management with categories and units
- Order creation with customer and product selection
- Automatic order total calculation
- Order status tracking
- Search, filtering, and pagination
- Internal user management for staff accounts

## User Roles

The system currently supports three roles:

- `ADMIN`
  - full access to products, customers, users, and orders
- `MANAGER`
  - can manage orders and create operational users based on business rules
- `SALES_AGENT`
  - limited operational access intended for order-taking workflows

## Problems It Solves

- Replaces manual order tracking in notebooks or spreadsheets
- Reduces mistakes in customer and product selection
- Keeps customer, order, and product data centralized
- Improves visibility for admins and managers
- Prevents unauthorized changes with role-based permissions
- Makes past orders easier to search and review

## Tech Stack

- Next.js 15
- React 19
- TypeScript
- Prisma ORM
- MySQL
- NextAuth.js
- Tailwind CSS
- Radix UI
- React Hook Form
- Zod

## Data Model

The app is centered around these core entities:

- `User`
- `Customer`
- `Product`
- `Order`
- `OrderItem`

Supporting enums include:

- `Role`
- `Category`
- `Unit`
- `OrderStatus`

## Project Structure

```text
app/                  Next.js App Router pages and API routes
components/           Reusable UI and business components
lib/actions/          Server actions for orders, users, customers, products
lib/                  Shared utilities and Prisma client
prisma/               Schema and database migrations
public/               Static assets
```

## Getting Started

### 1. Install dependencies

```bash
pnpm install
```

You can also use `npm`, `yarn`, or `bun`.

### 2. Configure environment variables

Create a `.env` file in the project root and add the required variables:

```env
DATABASE_URL="mysql://USER:PASSWORD@HOST:PORT/DATABASE"
AUTH_SECRET="your-secret-here"
NEXTAUTH_URL="http://localhost:3000"
```

Depending on your local setup and NextAuth configuration, you may only need `DATABASE_URL` and `AUTH_SECRET`, but `NEXTAUTH_URL` is recommended for local development.

### 3. Run database migrations

```bash
pnpm prisma migrate deploy
```

For local development, you can also use:

```bash
pnpm prisma migrate dev
```

### 4. Generate Prisma client

```bash
pnpm prisma generate
```

Note: Prisma client is also generated automatically during `postinstall`.

### 5. Start the development server

```bash
pnpm dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

## Available Scripts

```bash
pnpm dev          # start development server
pnpm build        # create production build
pnpm start        # run production server
pnpm lint         # run linter
pnpm prisma generate
pnpm prisma migrate dev
```

## Authentication

This project uses credential-based authentication with NextAuth.js and Prisma.

Users sign in with:

- `username`
- `password`

Passwords are stored as hashed values using `bcrypt`.

## Order Workflow

A typical flow inside the app looks like this:

1. An admin creates products and customer records.
2. Authorized staff log in.
3. A manager or admin creates an order.
4. The order is linked to a customer and one or more products.
5. The total amount is calculated from selected products.
6. The order status is tracked as `PENDING`, `COMPLETED`, or `CANCELED`.

## Current Functional Scope

From the current implementation, the app supports:

- dashboard metrics for total orders, customers, products, and today's orders
- searchable product listing with category filters
- searchable customer listing
- searchable order listing with status and date filters
- paginated user management
- internal CRUD operations for core business entities

## Deployment Notes

Before deploying:

- provision a MySQL database
- set production environment variables
- run Prisma migrations against production
- ensure `AUTH_SECRET` is set securely

The project includes a `vercel-build` script, so it can be adapted for Vercel deployments if desired.

## Roadmap Ideas

Potential next improvements:

- quantity support per order item
- invoices and printable receipts
- sales reports and analytics
- customer order history views
- stock tracking and inventory deduction
- audit logs for user actions
- export to CSV or PDF

## Contributing

If you're using this as a portfolio or internal project, feel free to adapt the naming, branding, and workflows to your business domain.

## License

No license has been added yet. If you plan to publish this publicly, consider adding an appropriate license.
