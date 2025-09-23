# XFoundation – Fentanyl & Narcan Training Quiz

Single‑page HTML quiz for community training. **Learning Mode** gives a short tip after the first miss and lets the learner try again. Passing requires **100% mastery**. When complete, the learner can hand off their details for certificate processing (email link, JSON download, copy to clipboard, or optional webhook). **No backend required.**

https://github.com/g-gerchow

## Features
- Mobile‑first, accessible (semantic HTML, keyboard friendly, ARIA feedback)
- Two tries per item with coaching on the first miss
- **Retake Missed Only** or **Start Over**
- Name + Email collected up front (for certificate delivery)
- Certificate handoff options (mailto, JSON, clipboard, optional webhook)
- No PII stored server‑side (everything runs in the browser)

## Quick start
1. Download this repo or just `index.html`.
2. Open `index.html` in any modern browser.

## Configure (edit at the top of `index.html`)
```js
const EMAIL_TO = "certificates@xfoundationx.org"; // inbox for certificate requests
const CERT_WEBHOOK_URL = ""; // optional Zapier/Make/Apps Script endpoint
```
- **EMAIL_TO** is used by the “Email certificate request” button after a pass.
- **CERT_WEBHOOK_URL** (optional) enables a “Send to webhook” button that POSTs a JSON payload.

## Edit questions
Search for `QUESTION_BANK` inside `index.html`. It’s a compact JSON‑style array:
```json
{
  "id": "q1",
  "type": "mcq",
  "prompt": "Fentanyl is especially dangerous because:",
  "choices": [
    {"text": "It is less potent than heroin"},
    {"text": "It is often mixed...", "correct": true},
    {"text": "It can only be found in prescription form"},
    {"text": "It has no effect on the central nervous system"}
  ],
  "hint": "Counterfeit pills...",
  "explanation": "Fentanyl is extremely potent..."
}
```
Types supported: `mcq`, `tf`, and `text` (fill‑in‑the‑blank). For `text`, add an `acceptable` list and set `normalize: true` to allow minor variations.

## Deploy to GitHub Pages (no CLI)
1. Go to your GitHub account and click **New repository**.
2. Name it, for example `xfoundation-narcan-quiz` (public).
3. Upload **`index.html`** and **`README.md`** (this file).
4. Go to **Settings → Pages**. Under *Build and deployment*, choose **Deploy from a branch**.
5. **Branch:** `main` • **Folder:** `/ (root)` → **Save**.
6. Wait ~1–2 minutes. Your site will be live at:  
   `https://<your-username>.github.io/xfoundation-narcan-quiz/`

## Deploy with Git (optional)
```bash
git clone https://github.com/<your-username>/xfoundation-narcan-quiz.git
cd xfoundation-narcan-quiz
# copy index.html & README.md into this folder
git add .
git commit -m "Initial commit: XFoundation Narcan quiz"
git push origin main
```

## Privacy
- The page runs entirely in the browser. Name/email are kept in memory for the current session and included only if the learner selects one of the handoff actions or if you configure a webhook.

## License
Copyright © XFoundation. All rights reserved. If you prefer an open‑source license (e.g., MIT), replace this section accordingly.
