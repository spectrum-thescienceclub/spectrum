# Spectrum Science Club — website

A single-page site for Spectrum Science Club (Woxsen University) with
Team / Events / Registrations tabs, a UPI QR payment box, and
registrations that save to a Google Sheet.

## Files

- `index.html` — the whole site (HTML, CSS, and JS in one file)
- `team/` — put your teammates' photos here (see `team/README.md`)

## 1. Before you upload: three things to edit in `index.html`

**A. UPI payment details** — search for this block near the bottom of the file:

```js
const UPI_ID = "yourclub@upi";      // <-- replace with your real UPI ID
const PAYEE_NAME = "Spectrum Science Club";
const AMOUNT = "199";               // <-- replace with your fee
```

**B. Google Sheet URL** — search for this line:

```js
const SHEET_URL = "PASTE_YOUR_APPS_SCRIPT_WEB_APP_URL_HERE"; // ends in /exec
```

To get this URL:
1. Make a Google Sheet with header row: `Timestamp, Name, Email, Event, UTR, Note`
2. Extensions → Apps Script, paste:

   ```js
   function doPost(e) {
     var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
     var data = JSON.parse(e.postData.contents);
     sheet.appendRow([new Date(), data.name, data.email, data.event, data.utr, data.note]);
     return ContentService.createTextOutput(JSON.stringify({result: "success"}))
       .setMimeType(ContentService.MimeType.JSON);
   }
   ```
3. Deploy → New deployment → Web app → Execute as: **Me** → Who has access: **Anyone** → Deploy
4. Copy the URL ending in `/exec` and paste it in for `SHEET_URL`

**C. Team photos** — add files to `team/` per `team/README.md`.

## 2. Upload to GitHub

1. Go to github.com → **New repository** → name it (e.g. `spectrum-club`) → keep it **Public** → Create
2. **Add file → Upload files** → drag in `index.html` and the whole `team` folder (including the photos) → Commit
3. Go to **Settings → Pages** → Source: **Deploy from a branch** → Branch: **main**, folder **/(root)** → Save
4. Wait a minute, refresh that Pages settings page — your live link will appear as
   `https://<your-username>.github.io/<repo-name>/`

That's it — the site, payments box, and registration form are all live at that link.
