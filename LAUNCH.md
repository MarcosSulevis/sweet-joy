# Sweet & Joy — Launch Checklist

Everything Vanessa (or Thales) needs to do to take the site live.

---

## Step 1 — Deploy to Cloudflare Pages

1. Go to [dash.cloudflare.com](https://dash.cloudflare.com) and log in (or create a free account).
2. Click **Workers & Pages** → **Create application** → **Pages** → **Upload assets**.
3. Project name: `sweet-joy` (this sets your free URL: `sweet-joy.pages.dev`).
4. Drag and drop the entire `/Volumes/SecondBrain/Claude/Sweet & Joy/` folder **excluding** `docs/`, `References/`, and any `.md` files if you want to keep it clean. At minimum, you need:
   - `index.html`
   - `style.css`
   - `script.js`
   - `_headers`
   - `assets/` folder (logo files)
5. Click **Deploy site**.
6. Visit `https://sweet-joy.pages.dev` to confirm it loads.

> **Alternative (GitHub auto-deploy):** Push the repo to a GitHub repository, then connect it in Cloudflare Pages → **Connect to Git**. Every `git push` will auto-deploy. This is the recommended long-term setup.

---

## Step 2 — Set Up Web3Forms (Order Form Email)

Web3Forms sends Vanessa an email every time someone submits the order form.

1. Go to [web3forms.com](https://web3forms.com) and enter **vanessa.sulevis@gmail.com**.
2. Check Vanessa's inbox for the confirmation email → click the link to get the **Access Key**.
3. Open `index.html` and find (Ctrl+F):
   ```
   PLACEHOLDER_WEB3FORMS_KEY
   ```
4. Replace it with the actual key. It appears **twice** — replace both.
5. Save and re-upload / re-deploy.
6. Test by submitting the order form on the live site. Vanessa should receive a test email within a minute.

> Free plan: 250 submissions/month. Upgrade if needed.

---

## Step 3 — Set Up Behold.so (Instagram Feed)

1. Go to [behold.so](https://behold.so) and sign up for a free account.
2. Connect the **@sweetjoync** Instagram account.
3. Behold will generate an embed snippet — it looks like:
   ```html
   <behold-widget feed-id="YOUR_FEED_ID"></behold-widget>
   <script src="..."></script>
   ```
4. Open `index.html` and find:
   ```html
   <div id="behold-placeholder" ...>
   ```
5. Replace that entire `<div>` block with the Behold embed snippet.
6. Save and re-deploy.

---

## Step 4 — Add Real Product Photos

All image slots are placeholders. Replace them with real photos:

| File path | What it should be |
|---|---|
| `assets/images/founder.jpg` | Vanessa's portrait photo |
| `assets/images/hero-bg.jpg` | Hero background (optional, currently not used) |
| `assets/images/cake-custom-01.jpg` | Custom cake photo 1 |
| `assets/images/cake-custom-02.jpg` | Custom cake photo 2 |
| `assets/images/docinhos-01.jpg` | Docinhos / gourmet sweets photo 1 |
| `assets/images/docinhos-02.jpg` | Docinhos / gourmet sweets photo 2 |

**Photo tips:**
- JPEG format, under 400 KB each (use [squoosh.app](https://squoosh.app) to compress).
- Minimum 800×800px for product photos.
- Founder photo: portrait orientation, good lighting, warm/natural setting.

After adding photos, re-upload `assets/images/` to Cloudflare Pages.

---

## Step 5 — Set Up Google Business Profile

This gets the bakery showing on Google Maps and local search results.

1. Go to [business.google.com](https://business.google.com) and sign in with Vanessa's Google account.
2. Search for **"Sweet & Joy Kernersville NC"** — if it doesn't exist, click **Add your business**.
3. Fill in:
   - Business name: **Sweet & Joy by Vanessa Sulevis**
   - Category: **Bakery** (or **Custom Cake Shop**)
   - Location: Kernersville, NC (service area, not a storefront)
   - Phone: **(336) 989-1342**
   - Website: `https://sweetjoync.com` (or your Cloudflare URL until domain is set)
4. Verify ownership (Google will mail a postcard or offer phone verification).
5. Once verified, upload photos and encourage first customers to leave reviews.

---

## Step 6 — Point a Custom Domain (Optional but recommended)

If Vanessa wants `sweetjoync.com` instead of `sweet-joy.pages.dev`:

1. Buy the domain at [Cloudflare Registrar](https://www.cloudflare.com/products/registrar/) (cheapest, no markup) or any registrar (Namecheap, Google Domains, etc.).
2. In Cloudflare Pages → your project → **Custom domains** → **Set up a custom domain**.
3. Enter `sweetjoync.com` and follow the DNS instructions (usually just point nameservers to Cloudflare).
4. SSL is automatic and free.

---

## Step 7 — Submit to Google Search Console

Helps Google index the site faster and shows search performance data.

1. Go to [search.google.com/search-console](https://search.google.com/search-console) and sign in.
2. Add property → **URL prefix** → enter `https://sweetjoync.com` (or your pages.dev URL).
3. Verify ownership (easiest: use the **HTML tag** method — paste a `<meta>` tag into `index.html` inside `<head>`, re-deploy, then verify).
4. After verification: **Sitemaps** → submit `https://sweetjoync.com/sitemap.xml`.

> Note: The site doesn't have an auto-generated sitemap since it's a single page. You can skip this or create a one-line `sitemap.xml` manually:
> ```xml
> <?xml version="1.0" encoding="UTF-8"?>
> <urlset xmlns="http://www.sitemaps.org/schemas/0.9">
>   <url><loc>https://sweetjoync.com/</loc></url>
> </urlset>
> ```

---

## Quick Reference

| Item | Value |
|---|---|
| WhatsApp | (336) 989-1342 |
| Email | vanessa.sulevis@gmail.com |
| Instagram | @sweetjoync |
| Web3Forms | web3forms.com |
| Behold.so | behold.so |
| Cloudflare | dash.cloudflare.com |
| Google Business | business.google.com |

---

## Local Preview (before deploying)

To preview the site locally on your Mac:

```bash
cd "/Volumes/SecondBrain/Claude/Sweet & Joy"
python3 -m http.server 8080
```

Then open `http://localhost:8080` in your browser.
