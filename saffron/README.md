# Saffron Pop-up page: how to put it on abbymood-space.de

This folder is the finished page. It is plain HTML with no build step and no outside requests
(fonts and photos are stored here).

```
saffron/
  index.html   the page (all styles and script inside)
  img/         4 photos from the poster
  fonts/       Inter, Rakkas, Vazirmatn, Alex Brush (self-hosted)
```

The site is an Astro project, so the page goes in `public/`, which Astro copies as-is.

## 1. Add the folder to the site

1. Copy this whole `saffron` folder into the Astro project's `public` folder:
   `public/saffron/index.html`, `public/saffron/img/…`, `public/saffron/fonts/…`
2. Start the site locally:

   ```bash
   npm run dev
   ```

3. Open http://localhost:4321/saffron/ and check it in the browser's phone view
   (all three screens, the arrows, swiping, the sign-up form).

## 2. Connect the sign-up form

Right now sign-ups are not sent anywhere. In `index.html`, find:

```js
const WAITLIST_ENDPOINT = "";
```

Put a URL there that accepts a `POST` with a JSON body. The page sends:

```json
{ "name": "…", "email": "…", "interested": true, "submittedAt": "2026-11-06T12:00:00.000Z" }
```

The page shows the thank-you only when the URL answers with a 2xx status. Otherwise it
shows "We could not save your sign-up…" and keeps what the visitor typed.

Easiest option: a form service such as Formspree.
1. Create a free account and a new form, e.g. "Saffron waiting list".
2. Copy the form's endpoint, e.g. `https://formspree.io/f/abcdwxyz`.
3. Paste it into `WAITLIST_ENDPOINT`. Each sign-up arrives by email and can be exported as CSV.

If the site already has its own backend or newsletter tool (Brevo, Mailchimp, …), point
`WAITLIST_ENDPOINT` at an API route that adds the contact there instead.

## 3. Test

1. Sign up with your own email on http://localhost:4321/saffron/.
2. Check that it arrived in the form service.
3. Tap "Add another name" and confirm the empty form comes back.

## 4. Publish

1. Build and check the page is in the output:

   ```bash
   npm run build
   ```

   `dist/saffron/index.html` should exist.
2. Deploy the way the site is normally deployed.
3. Open https://abbymood-space.de/saffron/ on a phone. Also try it without the last slash
   (https://abbymood-space.de/saffron). If that one gives a 404, add a redirect from
   `/saffron` to `/saffron/` in the hosting settings.

## 5. Privacy (Germany)

- Fonts and photos load from the site itself; the page makes no Google or other outside requests.
- The page links to `/imprint` and `/datenschutz` at the bottom of every screen.
- Add a short section to the privacy policy: the waiting list collects name and email to send
  updates about the Saffron Pop-up, which service stores them, and how to unsubscribe or ask for
  deletion. If the form service is outside the EU, sign its data processing agreement (DPA).

## 6. Share it

- Point the QR code on the poster to https://abbymood-space.de/saffron/
- Add the link to Instagram and, if wanted, to the site's menu or homepage.
