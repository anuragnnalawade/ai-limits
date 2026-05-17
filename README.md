# AI Limits — production build

A static, single-page working paper. Two files plus this README.

```
deploy/
├── index.html      ← the page
├── styles.css      ← base styles (typography, layout, colour)
└── README.md       ← this file
```

Production overrides (editorial detailing, folios, asymmetric layout,
tail stamps, masthead grid) live inline in `index.html` so the file is
self-sufficient if you ever lose `styles.css`.

---

## 1. Before you deploy — two things to fill in

### a) Cloudflare Web Analytics token

Open `index.html`, search for `YOUR_TOKEN_HERE`, replace with the token
Cloudflare gives you.

How to get it:

1. Sign in to **dash.cloudflare.com** (free).
2. Left sidebar → **Analytics & Logs → Web Analytics**.
3. **Add a site** → enter your domain (e.g. `ai-limits.org`).
4. Cloudflare gives you a snippet that looks like
   `data-cf-beacon='{"token": "abc123…"}'`. Copy the token string only.
5. Paste it over `YOUR_TOKEN_HERE` in `index.html`.
6. Save, redeploy.

Until the token is filled in, the script loads but reports nothing —
no error, no breakage.

### b) Formsubmit activation (submission form)

The contribution form posts to `https://formsubmit.co/research@ai-limits.org`.
On the very first real submission Formsubmit sends a confirmation email
to that address with an activation link. **Click the link once** —
from then on every submission lands as a formatted email.

If the inbox `research@ai-limits.org` doesn't yet exist:
create it first (any mailbox provider — Google Workspace, Fastmail,
Zoho, ProtonMail), or temporarily change the form `action` to your
personal email until the mailbox is ready.

If you'd rather have a searchable dashboard, swap the form action for
one of:

| Service       | URL pattern                              | Free tier       |
|---------------|------------------------------------------|-----------------|
| Web3Forms     | `https://api.web3forms.com/submit`       | Unlimited       |
| Formspree     | `https://formspree.io/f/YOUR_ID`         | 50 / month      |
| Basin         | `https://usebasin.com/f/YOUR_ID`         | 100 / month     |

Each one has a signup flow that gives you the URL above.

---

## 2. Hosting — recommended path (Cloudflare Pages)

End to end: ~30 minutes. Free apart from the domain (~$10 / year).

1. **Buy `ai-limits.org`.** Cheapest at-cost option is Cloudflare
   Registrar (you have to be signed up to Cloudflare). Namecheap or
   Porkbun are fine alternatives.

2. **Create a GitHub repository** named `ai-limits-website` (private
   or public — your call). Upload the three files in this folder to
   the repo root.

3. **Sign in to Cloudflare → Workers & Pages → Create application →
   Pages → Connect to Git.** Pick the repo. Build settings:
   - Framework preset: **None**
   - Build command: *(leave blank)*
   - Build output directory: `/`

   Click **Save and Deploy.** Within ~1 minute you have a live URL like
   `ai-limits-website.pages.dev`.

4. **Attach the custom domain.** In the Pages project → **Custom
   domains → Set up a custom domain → `ai-limits.org`**. If the domain
   is at Cloudflare Registrar, the DNS records are added automatically.
   Add `www.ai-limits.org` too.

5. **Activate Cloudflare Web Analytics** (see section 1a) and
   **activate Formsubmit** (section 1b).

6. **Send a test submission** to confirm the end-to-end pipe.
   Submit the form; confirm the email arrives at
   `research@ai-limits.org`.

You're live.

### Alternative — Netlify Drop (no GitHub needed)

If you want to skip Git for now: zip the `deploy/` folder, go to
**app.netlify.com/drop**, drag the zip on. You get a live URL in
20 seconds and can attach a custom domain from Netlify's dashboard.
You lose version control — pushing updates means re-dragging the zip.

---

## 3. Updating content later

For text-only changes, edit `index.html` directly, commit to GitHub,
Cloudflare Pages re-deploys automatically.

The six case sections each have:
- a card teaser (in the hero `.cards` grid)
- a long-form section (`<section class="case" id="case-NN">`)
- a folio string (in the inline `<style>` block)
- a tail stamp (also in the inline `<style>` block)

Keep these four in sync when editing.

---

## 4. Submissions you receive — what to do with them

Each email contains: story (paragraph), name, role/organisation, and
email. If the submission becomes a future case study:

1. Reply within a week (you promised this in the form footer).
2. If accepted, draft a new case using the existing template
   (`<section class="case">` block) and credit by name.
3. Maintain a simple changelog at the bottom of `index.html` so
   contributors can see when their case appeared.

---

## 5. File checklist before deploying

- [ ] `YOUR_TOKEN_HERE` replaced with the actual Cloudflare token
- [ ] `research@ai-limits.org` mailbox exists and is monitored
- [ ] `_next` URL in the form (`https://ai-limits.org/?submitted=1`)
      matches the domain you'll actually host on
- [ ] Test submission sent and confirmation email received
- [ ] Custom domain DNS resolves and HTTPS works
