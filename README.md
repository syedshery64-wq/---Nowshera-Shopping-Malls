# StockSense — AI Inventory for a Shopping Mall

GitHub-ready starter for the Nowshera Shopping Mall inventory system.

## Stack
- Next.js + TypeScript
- Supabase Auth + PostgreSQL + RLS
- AI API route (provider-agnostic placeholder)
- Tailwind CSS

## Setup

1. Create a Supabase project.
2. Open Supabase SQL Editor.
3. Run `supabase/schema.sql`.
4. Copy `.env.example` to `.env.local`.
5. Add your Supabase URL and anon key.
6. Install dependencies:
   ```bash
   npm install
   ```
7. Start:
   ```bash
   npm run dev
   ```

## Security model

- Staff can read operational inventory through `inventory_for_staff`.
- Cost/profit data is manager-only.
- Stock changes use database RPCs.
- AI prepares a pending change; it does not directly update inventory.
- Confirmation calls `confirm_pending_stock_change`.
- Stock-out cannot make inventory negative.
- Price changes require the manager RPC.

## Test data

`supabase/schema.sql` inserts:
- Type-C Cable — 15
- Wireless Mouse — 25
- USB Keyboard — 20

## AI integration

The `/api/ai` route is intentionally provider-neutral. Connect it to your chosen AI provider and expose only safe tools:
- read inventory
- read weekly sales
- create pending stock change

Never give the model direct SQL/update access.
