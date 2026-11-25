# Security notes

The site is a static page, so everything in `index.html` is visible to every visitor.

1. **JSONBin Master Key is public.** Anyone can read, edit or delete the whole database, including the user list, device tokens and password hashes. Rotate the key and move reads and writes behind a small server (Supabase Edge Function, Cloudflare Worker) or switch to Supabase Auth with Row Level Security.
2. **Device tokens are stored in the same bin.** Whoever can read the bin can sign in as any user, including the owner.
3. **Supabase `files` bucket** allows upload and delete with the public key. Restrict DELETE with Storage policies.
4. Password hashes use unsalted SHA-256. Use Supabase Auth (or bcrypt/argon2 server-side) instead.
