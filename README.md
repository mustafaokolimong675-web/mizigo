# Mizigo — legal pages

Static pages for the Mizigo Android app (`ug.mizigo`), published by Moonsoftware.

| File | Purpose | Play Console field |
|---|---|---|
| `index.html` | Privacy policy | **Policy → App content → Privacy policy** |
| `delete-account.html` | Account deletion request page | **Policy → App content → Data deletion → web URL** |

No build step. Plain HTML, one web font, nothing else.

---

## Publish

### 1. GitHub — done

Live at **https://github.com/mustafaokolimong675-web/mizigo** on `main`. This folder is the repo
root, deliberately separate from the Android project: that one carries a keystore path and an
800 MB heap dump and must not be pushed anywhere public.

To update the pages later, from this folder:

```bash
git add . && git commit -m "Update privacy policy" && git push
```

### 2. Vercel — needs your login

1. Go to **https://vercel.com/new**
2. **Import** the `mizigo` repo (authorise Vercel for the `mustafaokolimong675-web` account if
   it asks)
3. Framework preset **Other**. Leave build command and output directory empty — the site is
   already static, and the repo root is the site.
4. **Deploy**

You get `https://mizigo.vercel.app`, and because Vercel watches the repo, every later `git push`
redeploys it with no further steps.

Resulting URLs (`cleanUrls` is on, so the `.html` is optional):

- `https://mizigo.vercel.app/` — privacy policy
- `https://mizigo.vercel.app/delete-account` — deletion request page

Prefer the terminal? `npx vercel login` then `npx vercel --prod` from this folder. The dashboard
route is better: it wires up redeploy-on-push, which the one-shot CLI deploy does not.

### GitHub Pages instead

Repo → **Settings → Pages → Source: main / root**. Served at
`https://mustafaokolimong675-web.github.io/mizigo/`. Vercel is preferable: instant deploys, and a
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
