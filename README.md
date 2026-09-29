# Face-Key

Face-Key is a single-file guest check-in app with a separate front-desk dashboard. It uses Supabase for guest, room, face-token, preference, and desk-event data.

## Files

- `sourcecode.html` — guest consent, registration, face capture, check-in, room controls, and privacy screens.
- `dashboard.html` — live front-desk events and manual check-in override.
- `facekey_new_project_setup.sql` — creates the app tables and policies, then seeds fictional demo data.
- `desk_events.sql` and `returning_guest.sql` — earlier SQL setup snippets; the full setup file above includes the app schema they depend on.

## Run the demo

1. In the Supabase SQL Editor for the Face-Key project, run `facekey_new_project_setup.sql`.
2. Serve this folder from localhost or a secure HTTPS origin. For example, from this folder run `python3 -m http.server 8000`, then open `http://localhost:8000/sourcecode.html`.
3. Open `http://localhost:8000/dashboard.html` in another tab for the staff view.
4. Allow camera access to test face capture and face check-in. Face capture also loads MediaPipe and face-api.js models from their CDNs, so the browser needs internet access.

There is no build step. The guest app and dashboard each contain their Supabase project URL and browser-safe publishable key. Never put a Supabase secret or service-role key in either HTML file.

## Demo data

The setup SQL seeds 8 fictional guests, 8 rooms, 8 preference records, and 12 desk events. Four events remain `new`; all event timestamps are generated relative to the time the script runs. Demo passkeys are documented in a comment in the SQL file and stored in the database as SHA-256 hashes. No face embeddings are seeded, so the fictional guests can be checked in with their demo passkeys; face matching requires a real capture.

## Data access

The setup SQL enables RLS and creates anonymous policies to match the current browser-only app. Those policies allow public access to these app tables through the browser key. Use fictional demo data only until the app has an authenticated access model and appropriately restricted policies.
