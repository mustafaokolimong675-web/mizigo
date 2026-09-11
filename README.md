# Mizigo — legal pages

Static pages for the Mizigo Android app (`ug.mizigo`), published by Moonsoftware.

| File | Purpose | Play Console field |
|---|---|---|
| `index.html` | Privacy policy | **Policy → App content → Privacy policy** |
| `delete-account.html` | Account deletion request page | **Policy → App content → Data deletion → web URL** |

No build step. Plain HTML, one web font, nothing else.

---

## Publish

### 1. Push to GitHub

Run these **inside this `privacy-site` folder** — it is a standalone repo, deliberately separate
from the Android project, which contains a keystore path and a large heap dump that must not be
pushed anywhere public.

```bash
git init -b main
git add .
git commit -m "Mizigo privacy policy and account deletion pages"
gh repo create mizigo-privacy --public --source=. --push
```

No `gh`? Create an empty repo named `mizigo-privacy` on github.com, then:

```bash
git remote add origin https://github.com/<your-username>/mizigo-privacy.git
git push -u origin main
```

### 2. Deploy on Vercel

1. [vercel.com/new](https://vercel.com/new) → **Import** the `mizigo-privacy` repo
2. Framework preset: **Other**. Leave build command and output directory empty — it is already static.
3. **Deploy**

You get `https://mizigo-privacy.vercel.app`, and every later `git push` redeploys it.

Resulting URLs (`cleanUrls` is on, so the `.html` is optional):

- `https://mizigo-privacy.vercel.app/` — privacy policy
- `https://mizigo-privacy.vercel.app/delete-account` — deletion request page

### GitHub Pages instead

Repo → **Settings → Pages → Source: main / root**. Served at
`https://<username>.github.io/mizigo-privacy/`. Vercel is preferable: instant deploys, and a
custom domain later without changing the URL you gave Google.

---

## Before you submit to Google

- [ ] Open both URLs in a private window — Play rejects a policy behind a login or a 404
- [ ] Confirm the contact address `moonsoftware7@gmail.com` is correct and monitored
- [ ] Confirm the in-app route named on both pages (**Settings → Password and security → Delete account**) exists in the build you upload
- [ ] Re-read the retention paragraph ("generally up to five years") against your accountant's advice

## Editing

Content is plain HTML inside `<div class="sheet">` on each page. The palette is set once in
`:root` — Mizigo blue is `#1264F5`. Update the "Last updated" pill in `index.html` whenever the
policy changes materially.
