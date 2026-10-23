# Velvet & Blade — Live Booking App

A portfolio-ready salon/barber booking app using HTML, CSS, JavaScript and Supabase.

## Included
- Responsive premium design
- Service menu and KES prices
- Appointment form and shared database
- Available time lookup from Supabase
- Admin email/password sign-in
- Admin booking dashboard, cancellation, search and CSV export
- SQL schema with row-level security (RLS)

## Important: Configure Supabase before testing
This project will not save bookings until you connect it to your own Supabase project.

### A. Create the database
1. Sign in to https://supabase.com/ and create a project.
2. Open **SQL Editor** in the Supabase dashboard.
3. Open `supabase_schema.sql` from this folder, copy all of its contents, paste into a new SQL query and run it.
4. Keep your project URL and anon/public key ready from **Project Settings → API** (sometimes labelled API Keys).

### B. Connect the website
1. Open `index.html` in a text editor.
2. Near the bottom, find:
   `const SUPABASE_URL = "YOUR_SUPABASE_PROJECT_URL";`
   `const SUPABASE_ANON_KEY = "YOUR_SUPABASE_ANON_PUBLIC_KEY";`
3. Replace the placeholders with your Supabase Project URL and anon/public key.
4. Save the file.

Only use the anon/public key in this browser app. **Never paste a service_role/secret key into HTML or GitHub.**

### C. Create an admin account
1. In Supabase, open **Authentication → Users**.
2. Add a user with your own email and a strong password (if the dashboard asks for confirmation, complete it).
3. Copy that user's UUID.
4. Open SQL Editor and run this, replacing the sample UUID:
   `insert into public.booking_admins (user_id) values ('PASTE-ADMIN-USER-UUID-HERE');`
5. Open the website and sign in under **Booking dashboard** using that email/password.

The admin allowlist is deliberately not publicly writable. Do not add public sign-up to the admin panel.

### D. Test locally
1. Open `index.html` in a browser. Internet is required for Supabase and its JavaScript library.
2. Create a test booking.
3. Open the admin dashboard and sign in.
4. Check the booking, cancel it, search, and export CSV.

If you open the page as a local file and the browser blocks any request, use Visual Studio Code with the Live Server extension, then click **Go Live**.

## Deploy free with GitHub Pages
1. Create a new GitHub repository, e.g. `salon-booking-system`.
2. Upload `index.html` and `supabase_schema.sql` (README is optional). Do not upload any secret/service-role keys.
3. In repository **Settings → Pages**, choose **Deploy from a branch**, select `main` and `/ (root)`, then save.
4. Wait for GitHub Pages to publish the URL.
5. Open the live URL and test a booking and admin sign-in.

## Add it to your portfolio
Use the snippet in `portfolio_project_card.html` as a starting point. Replace:
- `YOUR-LIVE-APP-URL` with the GitHub Pages URL
- `YOUR-GITHUB-REPO-URL` with your repository URL
- `YOUR-SCREENSHOT.png` with a screenshot image you add to your portfolio repo

If your portfolio is plain HTML, copy the card markup into the portfolio's Projects section and the CSS into its stylesheet (or keep the provided inline style). Make sure links open your actual live project and repository.

## Production checklist
This is a learning starter, not yet a fully audited commercial system. Before using with real customers:
- Set the correct timezone for the business and database.
- Add rate limiting / anti-spam protections for public booking inserts.
- Validate prices and service IDs on the server (currently the client sends the displayed price; use a server-side function for production).
- Implement overlap checks based on service duration and per-stylist schedules; this starter only prevents identical confirmed start times.
- Consider CAPTCHA, privacy notice, retention policy, backups, and appropriate local data-protection compliance.
- Add real confirmation emails/SMS and business contact details if required.
