# her girls club — Website

## How to add or update an event

Open **`events-data.js`** in any text editor (Notepad, TextEdit, VS Code…).

Copy this block and paste it at the **top of the UPCOMING section**:

```js
{
  id: "my-event-june-2026",        // unique ID — no spaces, use dashes
  status: "upcoming",              // "upcoming" or "past"
  featured: false,                 // true = shown large on homepage (max 1 at a time)
  title: "Your Event Title",
  date: "June 14, 2026",
  dateSort: "2026-06-14",          // YYYY-MM-DD — used for sorting
  location: "Venue, Basel",
  description: "One or two sentences about the event.",
  ticketUrl: "",                   // paste Eventfrog link here, or leave ""
  image: "images/your-photo.jpg",  // drop photo into images/ folder, write filename here
  tags: ["Social", "Community"],   // choose from: Social, Sport, Wellness, Beauty, Culture, Art, Charity, Active, Party, Community
  partners: ["Brand Name"],        // optional — leave out if no partners
},
```

Save the file. The website updates automatically — no other file needs to change.

---

## When an event is over

Change `status: "upcoming"` → `status: "past"`. Save. Done.

---

## How to add photos

1. Save the photo from Instagram (screenshot or download)
2. Drop it into the **`images/`** folder
3. In `events-data.js`, set `image: "images/your-filename.jpg"`

If no image is set, a branded pink gradient shows automatically.

**Founder photos:** drop `images/lisa.jpg` and `images/katharina.jpg` into the images folder — they appear on the About page and Homepage automatically.

---

## File overview

```
her-girls-club/
├── events-data.js   ← EDIT THIS to add/update events
├── index.html       ← Homepage
├── events.html      ← All events page
├── about.html       ← About / founders
├── for-brands.html  ← Brand partnerships
├── contact.html     ← Contact form
├── style.css        ← All styles (don't edit unless you know CSS)
├── main.js          ← All logic (don't edit)
└── images/          ← Drop all photos here
    └── logo.png
```

---

## How to go live (free hosting in 2 minutes)

**Option A — Netlify (recommended, free)**
1. Go to [netlify.com](https://netlify.com) → Sign up free
2. Drag the entire `her-girls-club/` folder onto the Netlify dashboard
3. Done — you get a URL like `her-girls-club.netlify.app`
4. In Netlify settings → Domains → add your own domain (`hergirlsclub.ch`)

**Option B — GitHub Pages (free)**
1. Push the folder to a GitHub repo
2. Settings → Pages → Deploy from main branch

---

## Contact form setup (takes 5 min)

Currently the form shows a success message but doesn't actually send emails.
To make it work, connect **Formspree** (free):

1. Go to [formspree.io](https://formspree.io) → create free account
2. Create a new form → copy your Form ID (looks like `xrgvabcd`)
3. In `contact.html`, find this line and replace `YOUR_FORM_ID`:
   ```html
   action="https://formspree.io/f/YOUR_FORM_ID"
   ```
4. Done — form submissions go to your email.

Alternatively: if you host on Netlify, add `data-netlify="true"` to the `<form>` tag — no other setup needed.

---

## Newsletter setup

Currently shows a success message but doesn't save emails.
To connect to Mailchimp / Brevo / other:
- Replace the `<form class="newsletter-form">` element with the embed code from your email provider.

---

## Brand colors (for reference)

| Name | Hex |
|---|---|
| Brand Red | `#D8001D` |
| Brand Pink | `#F9C8D5` |
| Pink Light | `#FDF0F5` |
| Dark | `#141414` |
| White | `#FFFFFF` |
