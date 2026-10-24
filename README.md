# Grab Driver Application Admin Dashboard — adapted for new Supabase project

This is a prepared local build; it has **not** been committed to GitHub or deployed to Vercel.

## Changes in this build
- Uses the new Supabase project URL `https://xlvnjdusltbyrgskcgir.supabase.co` and its publishable key.
- Removes calls to the retired project's `admin_profiles`, `admin_list_applicants`, `admin_get_applicant_detail`, and `admin_update_applicant`.
- Uses Supabase Auth and checks the currently configured admin email before showing the dashboard.
- Reads applicants using the new `public.applicants` schema and `admin_list_new_applicants`-compatible fields.
- Loads details via `admin_get_new_applicant_detail(p_applicant_id)` and generates short-lived signed links for private applicant documents.
- Uses database status values `pending`, `in_progress`, `approved`, and `rejected`.
- Requires an admin note/reason before rejecting an application.

## Important before deployment
1. Confirm the intended admin email is `tanabodin.ch@grabtaxi.com`; the database RLS policies currently use this email.
2. Confirm that this user exists in Supabase Auth and can sign in.
3. Test in a preview deployment with the existing test applicant before promoting to production.
4. Status updates write to `public.applicants` under the existing RLS policy. This build does not yet write a row to `admin_audit_log` because no approved audit RPC was confirmed.
5. No Supabase schema, data, Edge Function, GitHub repository, or Vercel production deployment was changed by preparing this package.
