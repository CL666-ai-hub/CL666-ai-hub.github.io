English Flow 2.0 - Supabase cloud-connected prototype

Files
- index.html: single-page learning app

Before use
1. Create/configure a Supabase project.
2. In the app login screen, enter the Supabase Project URL and Publishable key, then tap Save connection settings.
   Use only the public Publishable key (or legacy anon key). Never use secret/service_role keys.
3. Ensure public.user_learning_data has columns:
   - user_id uuid (PRIMARY KEY or UNIQUE; references auth.users recommended)
   - date jsonb
   - updated_at timestamptz
4. Enable RLS. Policies must allow authenticated users to select/insert/update only rows where auth.uid() = user_id.
5. Register with email/password. If email confirmation is enabled, confirm the email before logging in.
6. After deployment, add the deployed site URL to Supabase Authentication > URL Configuration (Site URL and Redirect URLs).

Cloud behavior
- Login/signup use Supabase Auth.
- Learning state is stored as JSON in public.user_learning_data.date, keyed by the authenticated user's UUID.
- Existing cloud data is loaded first. If no row exists, the app initializes it from this browser's local cache (or an empty state).
- Subsequent changes are saved locally immediately and synchronized to Supabase after a short debounce.
- RLS is essential; do not disable it.

Prototype limitations
- This is a functional integration prototype, not a finished production product.
- It still contains a small demonstration phrase set and three sample reading articles, not the planned 500 phrases / 15 topics.
- Dictionary entries are examples and should be verified.
- Audio recording is browser-local playback only; recordings are not uploaded.
- Supabase connectivity and live auth must be tested in the deployed site using the user's own project credentials.
