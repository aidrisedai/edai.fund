# edai.fund

Coming-soon landing page for the **EdAI Fund**: a fund with a $100M target to back principled and ambitious teen founders.

It's one self-contained static page (`index.html`); the EdAI mark is inlined as SVG, and a standalone copy lives in `assets/edai-mark.svg`. It needs no build step.

## Preview locally

```sh
python3 -m http.server 8000   # then open http://localhost:8000
```

## Where sign-ups go

The form collects **name**, **email** and an optional **role** (teen founder, parent, investor, partner).

- **Netlify (zero config):** deploy this folder to Netlify. Sign-ups show up under *Forms → edai-fund-waitlist*, and you can turn on email notifications there.
- **Anywhere else (Vercel, GitHub Pages, etc.):** set `FORM_ENDPOINT` near the bottom of `index.html` to an endpoint that accepts a JSON POST, for example:
  - a [Formspree](https://formspree.io) form URL, or
  - a Google Apps Script web app that appends rows to a Google Sheet:

    ```js
    function doPost(e) {
      const d = JSON.parse(e.postData.contents);
      SpreadsheetApp.getActiveSheet().appendRow([new Date(), d.name, d.email, d.role, d.source]);
      return ContentService.createTextOutput(JSON.stringify({ ok: true }))
        .setMimeType(ContentService.MimeType.JSON);
    }
    ```

    Deploy it as a web app with access set to *Anyone*, then paste its `/exec` URL into `FORM_ENDPOINT`.
