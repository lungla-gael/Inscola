# Deploying the InScola website to Cloudflare Pages

This folder (`D:\Inscola\Inscola`) is ready to deploy as-is. `index.html` is the
homepage, and `site.css`, `shots/`, `assets/`, and `downloads/` are all
referenced with relative paths — no build step needed.

Exclude these from the deploy (already listed in `.gitignore`):
- `.claude/` — local Claude Code session config
- `.thumbnail` — OS-generated thumbnail cache
- `archive/` — the pre-edit copy of the original page, kept for reference only

The print collateral (`InScola Capabilities*.html`, `InScola Flyer.html`,
`InScola Trifold.html`, `booklet.css`, `marketing.css`) and `HANDOFF.md` aren't
linked from `index.html` other than the Capabilities document under
`downloads/`, so they're harmless to include or exclude.

## Option A — Direct upload (fastest, no git required)

1. Go to the [Cloudflare dashboard](https://dash.cloudflare.com/) → **Workers & Pages** → **Create application** → **Pages** → **Upload assets**.
2. Name the project (e.g. `inscola-website`).
3. Drag in everything from `D:\Inscola\Inscola` **except** `.claude`, `.thumbnail`, and `archive`.
4. Deploy. Cloudflare gives you a `*.pages.dev` URL immediately.
5. To update the site later, repeat: re-upload the folder as a new deployment.

## Option B — Git-based deploy (recommended for ongoing edits)

1. Initialize a git repo in `D:\Inscola\Inscola` and push it to GitHub/GitLab
   (the `.gitignore` already excludes the folders above).
2. In the Cloudflare dashboard → **Workers & Pages** → **Create application** →
   **Pages** → **Connect to Git** → pick the repo.
3. Build settings:
   - Framework preset: **None**
   - Build command: *(leave empty)*
   - Build output directory: `/`
4. Deploy. Every push to the connected branch will redeploy automatically.

## Custom domain (inscola.app)

Once the Pages project is live:

1. In the Pages project → **Custom domains** → **Set up a custom domain**.
2. Add `inscola.app` (and optionally `www.inscola.app`, redirecting to the apex).
3. If `inscola.app` is already on Cloudflare DNS, the CNAME/records are added
   for you automatically. Otherwise, Cloudflare will show the DNS records to
   add at your registrar.

**Note on `app.inscola.app`:** the browser-bar mockup in the hero section
shows `app.inscola.app` as the URL of the *InScola product* (the school's own
hosted instance), not this marketing site. It doesn't need to point at this
Pages project — leave it for whatever hosts the actual application, or update
the mockup text later if the product URL changes.

## Formspree

The contact form posts to `https://formspree.io/f/mojzrnvz`. The **first**
submission triggers a confirmation email to the Formspree account owner —
click the confirmation link there, or subsequent submissions won't be
delivered. After that, every submission emails the connected inbox and the
"Send via WhatsApp" button sends the same details to
`+237 677 386 779` via `wa.me`.
