# Cireng Enin — How the Site Works & Why It's Built This Way

## Stack decision: plain HTML/CSS/JS, single file

No framework, no build step. Reasons:

1. **The update story.** The requirement "easy for a non-technical person to
   update prices/photos" rules out anything with a build step. Instead, all
   changeable content lives in one `PENGATURAN` (config) object at the top of
   the `<script>` block, written in plain Indonesian with comments. Editing a
   price = editing a string in Notepad. No terminal, ever.
2. **Performance.** The whole site is ~1 HTML file + 4 small SVGs + Google
   Fonts. First paint is fast even on a cheap Android phone on 3G — which is
   the actual audience, since most orders come via mobile WhatsApp.
3. **Hosting.** A static folder deploys free anywhere (Netlify Drop is
   literally drag-and-drop, documented in the README).

This also matches the pattern used across this workspace (PersonalApp,
MakanApa, the CVs): all CSS in `<style>` at top, all JS in `<script>` at
bottom, Google Fonts via CDN, no dependencies.

## The data-driven menu

Menu cards are **not** hand-written HTML. `PENGATURAN.menu` is an array of
objects; a loop builds each card with `document.createElement` and
`textContent` (not `innerHTML` for user-editable strings — avoids accidental
HTML injection if someone pastes odd characters into a description). Each
card's "Pesan" button gets its own WhatsApp deep link with the variant name
and price pre-filled via `encodeURIComponent`, so the incoming WA chat
already says exactly what the customer wants.

`wa.me/<number>?text=<encoded message>` is the official WhatsApp click-to-chat
format — works on mobile (opens the app) and desktop (opens WhatsApp Web).

## Design rationale

- **"Enin" is Sundanese for grandmother**, and cireng is a Sundanese snack —
  so the identity leans into "from Grandma's kitchen" as the premium angle.
  The signature element is the handwritten font (**Gochi Hand**) used for
  annotations, price stickers, and section eyebrows: it reads as Enin's own
  handwriting on kitchen labels.
- **Palette** is derived from the food itself, each variable named after it:
  `--santan` (coconut-milk cream background), `--gula-aren` (palm-sugar brown
  ink), `--kulit`/`--minyak` (fried-golden accents), `--sambal` (rujak-sauce
  red for CTAs), `--daun` (banana-leaf green).
- **Type pairing:** Bricolage Grotesque (display — warm, rounded, characterful)
  + **Plus Jakarta Sans** (body — a typeface actually designed in/for Jakarta,
  a nice fit for an Indonesian brand).
- The scalloped divider (`.renda`) between hero and menu mimics the edge of
  *kertas nasi* / food doily paper — done with a CSS `mask` of repeated radial
  gradients, no image needed.
- The "Kenapa Enin" section flips to dark palm-sugar brown to break the warm
  cream rhythm and make the page feel premium rather than pastel.

## Small technical notes

- Scroll-reveal uses one `IntersectionObserver` adding a `.tampil` class;
  `prefers-reduced-motion` disables all animation (steam, reveals, smooth
  scroll) via a global media query.
- The floating WhatsApp button (`.wa-apung`) is the standard Indonesian UMKM
  pattern — always reachable regardless of scroll position.
- All WA links share the class `.tautan-wa` and are wired from config on load,
  so changing the number in one place updates the header, hero, CTA, contact
  card, and floating button at once.
- Hero illustration and menu placeholders are hand-drawn SVG (banana leaf +
  golden cireng + rujak bowl) so the site looks finished before real photos
  exist; each placeholder says "ganti dengan foto asli" on its face.
