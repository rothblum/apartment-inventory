# Apartment Inventory — agent runbook

This folder is the **canonical source** for a single static web page listing apartment
items for sale. It is published with GitHub Pages. Edit the files here, then push — the
live site rebuilds automatically.

## Key facts
- **Canonical folder:** `/Users/rothblum/Downloads/apartment-inventory-site/` (this folder). Edit files HERE, nowhere else.
- **The page:** `index.html` (the master list — the only list; a former `for_joy.html` copy was deleted).
- **PDF:** `apartment_inventory.pdf` is a regenerated copy of `index.html`. Keep it in sync.
- **Photos:** the `WhatsApp Image *.jpeg` files. `index.html` references them by relative filename.
- **GitHub repo:** https://github.com/rothblum/apartment-inventory (public). Remote `origin` is already set.
- **Live site:** https://rothblum.github.io/apartment-inventory/
- **Auth:** `gh` is logged in (keyring) as `rothblum` and git uses the osxkeychain helper, so `git push` works with no setup *on this machine*.

## The update loop (do this for every change)
1. Edit `index.html` (see card structure below).
2. Regenerate the PDF:
   ```bash
   "/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --headless --disable-gpu \
     --no-pdf-header-footer --print-to-pdf="apartment_inventory.pdf" "file://$PWD/index.html"
   ```
3. Commit & push:
   ```bash
   git add -A && git commit -m "..." && git push origin main
   ```
4. GitHub Pages rebuilds in ~1 min. Verify if desired:
   `curl -s -o /dev/null -w '%{http_code}' https://rothblum.github.io/apartment-inventory/`

## Card structure
Each item is one `.card` div inside `<div class="grid">`:
```html
  <div class="card">
    <img src="WhatsApp Image ....jpeg" alt="">
    <div class="body">
      <div class="num">ITEM 07</div>
      <h2>Short title</h2>
      <p>Description.</p>
      <div class="price">$50</div>
    </div>
  </div>
```
- Item numbers are `ITEM 01`…`ITEM 09` (leading zero) then `ITEM 10`+.
- Prices are plain like `$30` or `$15 (both)`. Keep them consistent.
- The subtitle near the top reads `... &middot; N items` — update N when adding/removing items.

## Common tasks
- **Mark an item SOLD:** add the `sold` class to its card and a SOLD badge to the number line:
  - `<div class="card">` → `<div class="card sold">`
  - `<div class="num">ITEM 11</div>` → `<div class="num">ITEM 11 <span class="sold-badge">SOLD</span></div>`
  - The CSS for `.card.sold` (fades + strikes through price) and `.sold-badge` (red, print-safe) is already in the `<style>` block.
- **Add an item:** the new photo usually lands in `/Users/rothblum/Downloads/`. Copy **only that one file**
  into this folder (`cp "/Users/rothblum/Downloads/<file>" .`), add a new `.card` before the closing
  `</div>\n</body>`, give it the next item number, and bump the subtitle count.
- **Link a product:** wrap text in an `<a href="https://...">...</a>` inside the `<p>` (e.g. Amazon listing for a monitor).

## Rules
- Keep this folder limited to inventory files only — never `cp` unrelated files from Downloads in (the repo is public).
- After any content change, regenerate the PDF and push so the site, the PDF, and these files stay in sync.
