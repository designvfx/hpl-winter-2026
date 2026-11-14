# HPL Winter Champion 2026

A static cricket tournament portal with Supabase cloud database and authentication.

## Features
- Public scoreboard and fixtures
- Four seeded teams: Pradeep, Bipin, Ronak, Krishna
- Admin login for player registration and match result entry
- Player-match scorecards (runs, balls, fours, sixes, wickets, bowling balls, runs conceded, maidens, catches, dismissal)
- Automatic batting and bowling leaderboards
- Points table: win 2, loss 0; tied results need a manually selected Super Over winner
- GitHub Pages-compatible static hosting

## 1. Create Supabase backend
1. Create a project at https://supabase.com/dashboard.
2. Open SQL Editor → New query.
3. Paste and run `schema.sql`.
4. Open Project Settings → API (or Connect) and copy the Project URL and publishable/anon key.
5. Edit `config.js`, replacing the two `YOUR_...` values.
6. In Authentication → Users, add an admin user with email and password. Public sign-up is not enabled in this portal.

The browser uses only the publishable key. Never place a `service_role` or secret key in frontend files.

## 2. Publish free on GitHub Pages
1. Sign in to GitHub and create a **public** repository named `hpl-winter-2026`.
2. Upload `index.html`, `config.js`, `schema.sql`, and `README.md` to the repository root.
3. Open repository Settings → Pages.
4. Under Build and deployment, choose **Deploy from a branch**, branch `main`, folder `/ (root)`, then Save.
5. Wait for GitHub Pages to publish. Your site URL will look like `https://YOUR-USERNAME.github.io/hpl-winter-2026/`.
6. Open that URL and test the public scoreboard, then sign in as admin to add players and results.

GitHub Pages hosts the frontend; Supabase stores the live data. GitHub Pages does not itself provide a database.

## Important notes
- This is a tournament starter, not a ball-by-ball scoring engine. Enter each player's innings figures once per match; leaderboards aggregate those saved scorecards.
- Bowling economy is calculated as runs conceded divided by overs (balls / 6). It assumes standard six-ball overs and does not model illegal deliveries separately.
- Points table currently ranks by points and wins. Net run rate is not calculated; record/resolve NRR externally if teams tie on points.
- Playoff team slots are seeded as format guidance; the playoff result-entry workflow should be extended before using the portal to administer live semi-final/final results.
- Supabase Free currently includes a 500 MB database and may pause projects after a week of inactivity. Check current limits on Supabase pricing before relying on it for a long-running season.
- For stronger production security, restrict write policies to a dedicated admin role/profile rather than allowing every authenticated account to write. Only create trusted admin accounts.
