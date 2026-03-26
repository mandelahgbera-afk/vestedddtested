# Supabase Setup Guide for Vested Crypto Platform

## Error You're Seeing
```
Error: Failed to run sql query: ERROR: 42P01: relation "public.super_admin" does not exist
```

This error means the database tables haven't been created yet. Don't worry - it's a simple 2-minute fix!

---

## Quick Setup (2 Minutes)

### Step 1: Go to Your Supabase SQL Editor
1. Go to [supabase.com](https://supabase.com) and log in
2. Select your Vested project
3. Click **SQL Editor** in the left sidebar
4. Click the **+** button and select "New Query"

### Step 2: Copy and Paste the Schema
1. In your project, open the file: `schema.sql`
2. Copy the ENTIRE contents (all 606 lines)
3. Paste into the Supabase SQL Editor
4. Click the blue **"Run"** button

**That's it!** The schema will be created in seconds.

---

## Verify It Worked

After running the schema, you should see:
- ✅ Green checkmark (success)
- Message shows tables created

To double-check:
1. Go to **Table Editor** in the left sidebar
2. You should see these tables:
   - `super_admin`
   - `users`
   - `cryptos`
   - `traders`
   - `transactions`
   - `user_traders`
   - `user_chart_data`
   - `user_cryptos`
   - `activity_logs`
   - `email_logs`
   - `audit_logs`
   - `admin_settings`
   - `email_templates`

---

## Next Step: Environment Variables

Once the schema is set up, add your Supabase credentials to your project:

1. In Supabase, go to **Settings → API**
2. Copy your **Project URL** and **anon key**
3. In your project, create a `.env.local` file:

```env
VITE_SUPABASE_URL=https://YOUR-PROJECT.supabase.co
VITE_SUPABASE_ANON_KEY=YOUR_ANON_KEY_HERE
```

4. Save and restart your dev server:
```bash
pnpm install
pnpm dev
```

---

## Troubleshooting

### Problem: "Extension not found" error
**Solution:** This happens on fresh Supabase projects. The extensions will be created automatically. Just run the schema again.

### Problem: "Permission denied" error
**Solution:** Make sure you're using a **Supabase service role key**, not the anon key. Go to Settings → API and use the **Service Role** secret key for running migrations.

### Problem: Tables already exist
**Solution:** The schema uses `CREATE TABLE IF NOT EXISTS` - it will skip tables that already exist. Safe to run multiple times.

### Problem: "Invalid password hash" on super_admin insert
**Solution:** This is expected - the default password hash is a placeholder. You don't need to log in as super admin to use the app. Regular user signup works fine.

---

## Seed Data

The schema includes sample data:
- **9 cryptocurrencies** (BTC, ETH, LTC, etc.)
- **5 sample traders** for copy trading
- **Default admin settings** (deposit addresses, fees, etc.)

You can modify these after running the schema by going to **Table Editor** and editing rows directly.

---

## Security Notes

The schema includes:
- ✅ Row-level security (RLS) on all tables
- ✅ Automatic timestamp updates (created_at, updated_at)
- ✅ Audit logging for admin actions
- ✅ Triggers for balance updates
- ✅ Proper foreign key constraints

Your data is secure!

---

## Next Steps

1. ✅ Run the schema (you're here!)
2. Add environment variables
3. Start the dev server
4. Create a test user account
5. Start building!

**Questions?** Check `QUICKSTART.md` for more details.
