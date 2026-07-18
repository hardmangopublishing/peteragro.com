# peteragro.com

A static site. No build step, no dependencies, no framework. Edit the HTML, push, and it is live in about a minute.

```
index.html      home — catalog, the spine shelf, all twelve books
services.html   working together — published rates
style.css       all styling (colours and fonts are set at the top)
images/         cover thumbnails, 520px wide
CNAME           tells GitHub which domain to serve
```

---

## Put it online (about 20 minutes, once)

### 1. Make the repository

On GitHub, create a new **public** repository named exactly:

```
peteragro.github.io
```

Using that exact name matters — GitHub treats it as your user site and serves it from the root.

Upload every file in this folder to the repository (drag and drop into the browser works: **Add file → Upload files**). Keep the `images` folder as a folder.

### 2. Turn on Pages

In the repository: **Settings → Pages**. Under *Build and deployment*, set **Source** to `Deploy from a branch`, **Branch** to `main`, folder `/ (root)`. Save.

Wait a minute, then check `https://peteragro.github.io` — the site should be there.

### 3. Point the domain at it (GoDaddy)

Sign in to GoDaddy, open **My Products → Domains → peteragro.com → DNS**.

Delete any existing `A` records for `@`, and the `CNAME` for `www` if one exists. Then add these five:

| Type | Name | Value | TTL |
|---|---|---|---|
| A | @ | 185.199.108.153 | 1 hour |
| A | @ | 185.199.109.153 | 1 hour |
| A | @ | 185.199.110.153 | 1 hour |
| A | @ | 185.199.111.153 | 1 hour |
| CNAME | www | peteragro.github.io | 1 hour |

Those four IP addresses are GitHub's. They are correct as of this writing — if the site does not come up, check GitHub's current list at *Pages → Custom domain* in their documentation.

### 4. Tell GitHub about the domain

Back in **Settings → Pages → Custom domain**, enter `peteragro.com` and save. The `CNAME` file in this repository already contains it, so this should populate on its own.

Wait for the DNS check to pass — usually minutes, occasionally a few hours. Then tick **Enforce HTTPS**. Do not skip this; it is free and the site will be flagged as insecure without it.

---

## Three things to change before you launch

**1. The email address.** Every page uses `hello@peteragro.com`, which does not exist yet. Either set up forwarding in GoDaddy (Email → Forwarding) so it lands in your normal inbox, or search-and-replace it with an address you already have.

**2. The Amazon links.** Each book currently links to an Amazon *search* for its title, which works immediately but is not ideal. Once a book is live, replace the link with its direct product URL:

```html
<!-- from -->
<a href="https://www.amazon.com/s?k=The+Laundromat+Playbook+Peter+Agro">
<!-- to -->
<a href="https://www.amazon.com/dp/YOURASIN">
```

If you set up an Amazon Author Page, link the wordmark or add it to the footer.

**3. The rates.** They are ranges, deliberately. Narrow them once you have done two or three projects and know how long the work actually takes you.

---

## Editing later

**Adding a book** — copy an existing `<article class="book">` block, change the image name, title, volume, and link, and drop a 520px-wide cover into `images/`.

**Adding it to the shelf** — copy one `<a class="spine">` line in `index.html` and change the title, the volume numeral, and the anchor. Add `spine--sage` to the class for a book outside the Turnkey Library.

**Changing colours or fonts** — everything is in the `:root` block at the top of `style.css`. The navy, gold, and sage are the exact values used on the book covers, so they will stay in step with the print work.

**Checking your work** — open `index.html` in a browser by double-clicking it. What you see locally is what will be live.
