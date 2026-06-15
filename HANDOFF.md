# InScola Website — Handoff Brief for Claude Code

This is a finished, responsive marketing website built as plain HTML/CSS/JS.
**No build step. No framework.** It can be hosted on any static host as-is.
Your job is to host it and wire up the placeholders below — please do NOT
redesign it; keep the existing look, brand, and structure exactly.

## Files that make up the website
- `InScola Website.html`  ← the page itself (rename to `index.html` when hosting)
- `site.css`              ← all styles
- `shots/`                ← screenshots used on the page (keep this folder next to the HTML)
- `assets/`               ← brand logos (svg)
- `downloads/InScola-Capabilities.html`  ← the downloadable capabilities document (self-contained)

The other files in this project (`InScola Capabilities*.html`, `InScola Flyer.html`,
`InScola Trifold.html`, `booklet.css`, `marketing.css`) are the PRINT collateral —
not part of the website. You only need them if you also want to host the booklet.

## Tasks (in priority order)

### 1. Make it the homepage
Rename `InScola Website.html` → `index.html` (update the download links if you move files).
Deploy the folder to a static host (Netlify / Vercel / Cloudflare Pages / GitHub Pages all work).

### 2. Wire up the contact form
The form is in the `#contact` section. It currently just shows a thank-you message
on submit (see the inline `onsubmit` handler) and does NOT send anything.
Connect it to ONE of:
- An email service (e.g. Formspree, Web3Forms, or a small serverless function), OR
- A WhatsApp deep link that pre-fills the enquiry, OR
- The school's own backend endpoint.
Fields: name, school, phone, city. Keep the existing thank-you state on success.

### 3. Fill in real contact details
Search the HTML for `data-field` attributes and replace the placeholder text:
- `data-field="phone"`        → real phone number
- `data-field="whatsapp"`     → real WhatsApp number
- `data-field="whatsapp-link"`→ the header WhatsApp button (point its href at https://wa.me/2376XXXXXXXX)
- `data-field="email"`        → real email
Also update "Douala, Cameroon", the footer year, and the browser-bar URL "app.inscola.cm" in the hero if needed.

### 4. Hook up the videos
Two video areas:
(a) The big "#demo" block — replace its `href="#"` (id `videoLink`) with the YouTube URL,
    or swap it for a real YouTube embed/lightbox.
(b) The "#deliverables" gallery — six cards, each an `<a class="vcard" href="#" data-video="...">`.
    Replace each `href="#"` with the real clip URL (opens in a new tab), OR implement a
    lightbox that plays the video in-page. The `data-video` attribute names each clip for reference.
The QR image in the demo section (`shots/yt-qr.png`) already encodes your YouTube link — leave or replace as needed.

## How to ADD MORE CONTENT LATER (it's designed to be easy)

### Add an FAQ
The JS auto-wires every `.faq-item`, so just copy one block inside `<div class="faq">`:
```html
<div class="faq-item reveal">
  <button class="faq-q" type="button">Your question?<span class="qi"><svg><use href="#i-plus"></use></svg></span></button>
  <div class="faq-a"><div class="faq-a-inner">Your answer text.</div></div>
</div>
```
No JavaScript changes needed.

### Add a video card
Copy one card inside `<div class="vgrid">` and change the thumbnail, tag, title, duration, and href:
```html
<a class="vcard reveal" href="REAL_URL" target="_blank" rel="noopener" data-video="my-clip">
  <span class="vthumb"><img src="shots/SOME-IMAGE.png" alt="...">
    <span class="pp"><span><svg><use href="#i-play"></use></svg></span></span><span class="dur">1:10</span></span>
  <span class="vbody"><span class="vtag">Category</span><h4>Card title</h4><p>One-line description.</p></span>
</a>
```

### Add a feature / benefit / pricing card
Same pattern — copy an existing `.fcard`, `.bcard`, or `.price` block and edit the text.
The `reveal` class gives it the scroll-in animation automatically.

### Edit pricing
The Annual/Lifetime toggle is JS-driven. Each price lives on the `.amt` element as
`data-annual="..."` and `data-life="..."`. To change a price, edit those two attributes
(and the visible `<span class="num">` for the default/annual amount). The maintenance line
(`.maint`) and the two setup notes (`.setup-item`) are plain text — edit directly.
Current model: Annual 400k / 600k / 1,000,000 XAF (Finance / School / Unified); Lifetime is 5×;
+50,000 XAF/year maintenance (always); 100,000 XAF one-time setup & training; internet
features quoted separately (domain included).

## Sections already on the page (for reference)
Header · Hero · Problem statement · 3 Benefits · 8-card Feature grid · Screenshots ·
Pricing (with Annual/Lifetime toggle) · "Who it's for" · Demo video + QR ·
Deliverables video gallery (6 cards) · Download band (capabilities document) ·
FAQ (7 items, accordion) · Contact (form + direct details) · Footer.

## Notes
- Everything is responsive (desktop / tablet / phone) and respects "reduced motion".
- Animations are pure CSS + a tiny IntersectionObserver; nothing to configure.
- Fonts load from Google Fonts (Poppins + Inter). If the host must be fully offline, self-host them.
- Colours and type live as CSS variables at the top of `site.css` (`:root { ... }`).
