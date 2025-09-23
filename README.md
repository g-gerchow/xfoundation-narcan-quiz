# XFoundation – Fentanyl & Narcan Training Quiz (Gmail-first)

Single‑page HTML quiz for community training. **Learning Mode** lets a learner retry after the first miss, and passing requires **100% mastery**. On completion, the page can:
- Open a **Gmail compose** window (default), plus Outlook Web or the default Mail app
- **Download** a JSON payload
- **Copy** the payload to clipboard
- **POST** the payload to an optional **webhook**

No backend is required for the quiz itself.

## Live with GitHub Pages
1. Create a repo, for example `xfoundation-narcan-quiz`.
2. Upload **index.html** and this **README.md**.
3. Enable **Settings → Pages → Deploy from a branch → main / (root)**.
4. Your link will be `https://<user>.github.io/xfoundation-narcan-quiz/`.

## Configure
Open `index.html` and edit the config at the top:
```js
const EMAIL_TO = "xfoundationmjgx@gmail.com";  // inbox for certificate emails
const CERT_WEBHOOK_URL = "https://xfoundationx.org/api/xfoundation-cert-webhook"; // optional: your endpoint
const CERT_WEBHOOK_SECRET = ""; // optional: adds X-Quiz-Secret header
```
> If `CERT_WEBHOOK_URL` is not empty, a **Send to webhook** button shows on pass.

## Webhook placeholder
This repo includes a **webhook/** folder with starter code for two common platforms:

- **Netlify Functions**: `webhook/netlify/functions/xfoundation-cert-webhook.js`
- **Vercel Serverless**: `webhook/vercel/api/xfoundation-cert-webhook.js`

Both versions:
- Validate `POST`
- Optionally check the `Origin` and a shared header `X-Quiz-Secret`
- Return CORS headers so the browser can POST from the quiz page
- TODO: you wire the payload to email, Google Sheet, database, or your certificate system

### Netlify (quickest for static sites)
1. If your site is on Netlify, copy `webhook/netlify/functions/xfoundation-cert-webhook.js` into your site repo at `netlify/functions/xfoundation-cert-webhook.js`.
2. In **Netlify → Site settings → Functions**, ensure functions are enabled.
3. Deploy. Your function URL will look like:
   `https://YOUR_NETLIFY_SITE.netlify.app/.netlify/functions/xfoundation-cert-webhook`
4. Put that URL into `CERT_WEBHOOK_URL` in `index.html`.

### Vercel (API routes)
1. If your site is on Vercel, copy `webhook/vercel/api/xfoundation-cert-webhook.js` to `api/xfoundation-cert-webhook.js` in the repo root (or inside `/api` for Next.js).
2. Deploy. Your endpoint will be:
   `https://YOUR-VERCEL-APP.vercel.app/api/xfoundation-cert-webhook`
3. Put that URL into `CERT_WEBHOOK_URL` in `index.html`.

## Test the webhook
- Complete the quiz to 100% → click **Send to webhook**.
- Check your platform logs. You should see the JSON payload:
```json
{
  "quiz": "XFoundation – Fentanyl & Narcan Training Quiz",
  "completedAt": "...",
  "startedAt": "...",
  "user": { "name": "First Last", "email": "person@example.org" },
  "mastery": "100%",
  "score": "10/10",
  "secondTriesUsed": 1,
  "version": "v2"
}
```

## Privacy
Name and email are used for certificate delivery and are transmitted only if the learner chooses the email/JSON/webhook action. Host your webhook on HTTPS and restrict the origin in code.

## License
Copyright © XFoundation.
