# Yalla website

The public About, Privacy and Terms pages for the Yalla app (CSC 490 senior project, Yamen Morcel and Hadi Khawand),
served by GitHub Pages at https://yalla-app-lb.github.io/. Google's sign-in screen links to these pages.

Plain HTML and one CSS file: no build step. Colours come from the app's `YallaPalette`
(`frontend/lib/core/theme/yalla_colors.dart` in the Yalla repo).

- `fonts/`: Plus Jakarta Sans (the app's font), from `@fontsource-variable/plus-jakarta-sans@5.3.0`, SIL Open Font
  License (`fonts/OFL.txt`). Served from here so the site loads nothing from other sites.
- `img/screens/` (the two phones at the top of About): rendered from the app's design mockups (`docs/design/mockups/` in the Yalla repo). Replace them
  with real phone screenshots (390 × 844 ratio, test accounts only) when we have them.

**Keep the `google<…>.html` file. It is Google Search Console's proof that we own this site; deleting it un-verifies the site.**

Never add a custom domain here: Google needs these exact addresses, with no redirect.

## When someone emails to delete their account

1. Check the email came from the account's own address; reply to confirm.
2. Supabase → Authentication → Users → find the email → Delete user. The database removes their rows with it
   (profile, interests, free time, friends, groups, hosted plans, invites, seats, votes, notifications, push
   addresses, searches, place submissions and reports), and their Google link.
3. Supabase → Storage → `avatars` → delete the folder named with their user id (photos aren't removed by step 2).
4. Supabase → SQL editor:
   `delete from notification where data->>'from_user_id' = '<their user id>';`
5. Admin panel → reject any place they added that is still waiting for approval.
6. Reply that it's done, within 30 days of the request.

If the privacy policy changes (for example the AI starts using an outside service), update `privacy.html` and its date
before that change goes live.
