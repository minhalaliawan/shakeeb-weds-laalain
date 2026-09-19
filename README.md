# Ahmed Shakeeb &amp; Dr. Laalain Fatima — Wedding Invitation

A single-file static invitation site. No build step, no dependencies, no backend.
Open `index.html` in a browser and it works.

---

## The events

| Event  | Day      | Date            | Time    | Venue |
|--------|----------|-----------------|---------|-------|
| Mehndi | Friday   | 23 October 2026 | 5:00 PM | Farmhouse opposite Street 17, F-11/2, Islamabad |
| Barat  | Saturday | 24 October 2026 | 5:30 PM | Fortress Events Complex, Islamabad Expressway, opposite PWD |
| Walima | Sunday   | 25 October 2026 | 5:30 PM | Aura Grande Event Complex, 2 Service Road E, Golra NPF, E-11/4 |

RSVPs are sent to WhatsApp **+92 333 5101170**.

---

## Personalised links (the useful bit)

The same page can greet each guest by name and show only the events they are
invited to. Add a query string to the link — the page reads it, then **wipes it
from the address bar**, so the guest never sees the code.

```
https://your-site.com/?to=Uncle%20Ali&event=w
```

### `to=` — the guest's name
Greets them in the hero (“Cordially inviting **Uncle Ali** to celebrate…”) and
pre-fills the RSVP form.

### `event=` — which events they see

| Code | Shows                | Countdown targets |
|------|----------------------|-------------------|
| *(omitted)* | All three events | Mehndi |
| `m`  | Mehndi only          | Mehndi |
| `b`  | Barat only           | Barat |
| `w`  | Walima only          | Walima |
| `mb` | Mehndi + Barat       | Mehndi |
| `bw` | Barat + Walima       | Barat |

With a single event the RSVP form drops the “which events” dropdown and the
WhatsApp message names that event directly.

The choice is remembered in `sessionStorage`, so a refresh keeps it.

### Examples

```
?to=Ahsan%20Bhai                  → all events, greeted by name
?to=Dr%20Sana&event=w             → Walima only
?to=Kamran%20Uncle&event=bw       → Barat + Walima
?event=m                          → Mehndi only, no name
```

Spaces must be written as `%20`.

---

## Optional files

Drop these into `assets/` — each one is optional and the site degrades cleanly
without it:

- `music.mp3` — replaces the online background track
- `mehndi.jpg`, `barat.jpg`, `walima.jpg` — the printed cards. When present, a
  **View Card** button appears on that event and opens the image full screen.
  When absent the button removes itself.

---

## Editing content

Everything lives in `index.html`.

- **Names, dates, venues** — in the `<article class="ev">` blocks
- **WhatsApp number** — `var PHONE = '923335101170';` near the bottom of the script
- **Colours** — the `:root` block at the top of the `<style>` (ivory + gold, light theme)
- **Map links** — the `Location` buttons currently use Google Maps *search*
  queries. Replace each `href` with an exact `maps.app.goo.gl/...` pin when you
  have one.
- **Countdown target** — `var target = new Date('2026-10-23T17:00:00+05:00')`,
  plus the per-event targets in the `evKey` branches

---

## Deploying

Static hosting, nothing to build.

**Vercel**

```bash
npx vercel --prod
```

Or drag the folder onto [vercel.com/new](https://vercel.com/new). `vercel.json`
is already set up.

**Netlify** — drag the folder onto [app.netlify.com/drop](https://app.netlify.com/drop).

---

## Local preview

```bash
npx --yes serve -l 4321 .
```

Then open `http://localhost:4321`.
