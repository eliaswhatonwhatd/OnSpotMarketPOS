# OnspotMarket Cloud POS

A professional, cloud-synced Point of Sale system with barcode scanning.

## Setup Instructions
1. **Supabase Tables:** Run the following SQL in your Supabase SQL Editor:
   ```sql
   create table inventory (
     id uuid default gen_random_uuid() primary key,
     name text not null,
     barcode text unique not null,
     cost numeric not null,
     price numeric not null,
     qty integer not null,
     created_at timestamp with time zone default now()
   );

   create table sales (
     id uuid default gen_random_uuid() primary key,
     items jsonb not null,
     total numeric not null,
     cost numeric not null,
     method text not null,
     created_at timestamp with time zone default now()
   );

   create table cash_transactions (
     id uuid default gen_random_uuid() primary key,
     amount numeric not null,
     type text not null,
     note text,
     created_at timestamp with time zone default now()
   );

   -- Disable RLS to allow the app to work
   alter table inventory disable row level security;
   alter table sales disable row level security;
   alter table cash_transactions disable row level security;
