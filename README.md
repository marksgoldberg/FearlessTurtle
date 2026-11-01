# The Fearless Turtle

A plain HTML/CSS website: a landing page, an essays index, and one page per
essay. No build tools, no frameworks, nothing to install — every file here
is exactly what a browser reads.

**GitHub username:** mrmarkgoldberg
**Domains:** the site itself is served at **thefearlessturtle.com**.
**fearlessturtle.com** is set up as a forward, so anyone who types that in
gets sent straight to thefearlessturtle.com. See Part 2 below for that.

## Files

```
index.html              the landing page
about.html               optional about page
css/style.css            all styling, shared by every page
essays/index.html        list of all essays
essays/essay-template.html   copy this to start a new essay
essays/first-essay.html      placeholder essay #1
essays/second-essay.html     placeholder essay #2
CNAME                    tells GitHub Pages which domain to serve on (already set to thefearlessturtle.com)
```

## Before you publish

The site name, footer credit, and domain are already filled in
(The Fearless Turtle / Mark Goldberg / thefearlessturtle.com). The only
placeholder left to deal with is the tagline near the top of `index.html`:

```html
<p class="tagline">Essays and articles on [whatever you write about].</p>
```

Edit that line (in `index.html`) to describe what the site's actually
about, then swap in your own essays in place of the two placeholders (see
"Adding a new essay" below).

---

## Part 1 — Get thefearlessturtle.com live on GitHub Pages

You already have a GitHub account (username **mrmarkgoldberg**), so this
starts at creating the repository.

### 1. Create a repository and upload these files

1. On github.com, click the "+" in the top right → "New repository."
2. Name it whatever you like — e.g. `fearless-turtle-site` (it doesn't need
   to match your GitHub username or your domain). Make it Public.
3. Click "Create repository."
4. On the new repo's page, click "Add file" → "Upload files," then drag in
   everything from this folder (keeping the `css/` and `essays/`
   subfolders intact), and commit the changes.

### 2. Turn on GitHub Pages

1. In your repo, go to Settings → Pages.
2. Under "Build and deployment," set Source to "Deploy from a branch,"
   branch `main`, folder `/ (root)`. Save.
3. Under "Custom domain," enter exactly `thefearlessturtle.com` and save —
   not `fearlessturtle.com`. (This should match the `CNAME` file already in
   this folder — it does.)
4. Wait a minute, then GitHub will show your temporary URL
   (`https://mrmarkgoldberg.github.io/reponame`) — confirm the site loads
   there first, before DNS is even touched.

### 3. Point thefearlessturtle.com's DNS at GitHub Pages

In GoDaddy: go to **thefearlessturtle.com** → DNS → Manage DNS, and set:

**A records** — add four A records, all with Name `@`, pointing at GitHub
Pages' IP addresses:

```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```

(Delete any existing A record or "parked" record on `@` first.)

**CNAME record** — for the `www` version, add:

```
Type: CNAME
Name: www
Value: mrmarkgoldberg.github.io
```

DNS changes can take anywhere from a few minutes to a few hours to take
effect. Once thefearlessturtle.com loads correctly, go back to GitHub →
Settings → Pages and check "Enforce HTTPS" so the site loads securely.

---

## Part 2 — Forward fearlessturtle.com to thefearlessturtle.com

This domain doesn't need any hosting, GitHub, or DNS records of its own —
GoDaddy has a built-in "Domain Forwarding" feature that's built exactly for
this ("send visitors of domain A to domain B").

1. In GoDaddy, go to **fearlessturtle.com** → DNS → **Forwarding**.
2. Click "Add" next to Domain forwarding.
3. Forward to: `https://thefearlessturtle.com`
4. Forwarding type: **Permanent (301)**
5. Forward settings: **Forward only** (not "Forward with masking" — masking
   hides the destination URL in the address bar, which looks sketchy to
   visitors and hurts SEO; you want plain forwarding).
6. Save.

That's it — no A records, no CNAME, nothing else to configure on
fearlessturtle.com. Give it a little while to propagate, then test by
typing fearlessturtle.com into a browser and confirming it lands on
thefearlessturtle.com.

---

## Troubleshooting: "NotServedByPagesError" / domain improperly configured

If GitHub Pages shows an error like "thefearlessturtle.com and its
alternate name are improperly configured... Domain does not resolve to the
GitHub Pages server," check these two things — this is exactly what
happened on this project the first time around:

1. **Make sure the custom domain field says `thefearlessturtle.com`, not
   `fearlessturtle.com`.** Settings → Pages → Custom domain. If it's wrong,
   clear it, save, then re-enter the correct domain and save again.
2. **Make sure there's no Domain Forwarding set up on thefearlessturtle.com
   itself.** Forwarding (Part 2 above) belongs only on fearlessturtle.com.
   If thefearlessturtle.com also has a forward configured in GoDaddy, it
   will keep overriding your A records and point visitors at GoDaddy's
   forwarding service instead of GitHub — which is indistinguishable from
   DNS just being wrong. Delete any forward found on thefearlessturtle.com,
   then re-check/re-add the four A records and the `www` CNAME from Part 1,
   step 3.

After fixing either of those, it can take a little while for DNS to
re-propagate before GitHub's check clears on its own.

---

## Adding a new essay later

1. Copy `essays/essay-template.html` to a new file, e.g.
   `essays/why-i-like-tuesdays.html`.
2. Edit the title, date, and body paragraphs in that file.
3. Add a matching `<li>` entry to `essays/index.html` (and optionally to the
   "Recent essays" list on `index.html`), linking to the new file.
4. Upload the changed/new files to GitHub (drag them into the repo again, or
   use GitHub Desktop / `git` if you get comfortable with it) and commit.
   The live site updates automatically within a minute or two.

That's the entire publishing workflow — no database, no CMS, no server to
maintain.
