# LINE LIFF Flex Message Share Test

Minimal test app for LIFF `shareTargetPicker()` using the Flex bubble from `data/pdp.json`.

The real LINE test needs a public HTTPS URL. The `public/` directory is a complete static site:

- `public/index.html` is the LIFF page.
- `public/flex-message.json` is the static HTTPS endpoint that returns the full Flex Message.

Deploy `public/` to any HTTPS static host, then set that deployed URL as the LIFF endpoint URL in the LINE Developers Console.

## Run locally

```bash
npm start
```

Open:

```text
http://localhost:3000
```

The local URL is only useful for basic browser checks. LINE LIFF endpoint testing requires an HTTPS URL configured in the LINE Developers Console.

## Deploy as static HTTPS

### Recommended: GitHub Pages

This repo includes a GitHub Actions workflow at `.github/workflows/deploy-pages.yml`.

1. Create a new GitHub repo, for example:

```text
line-liff-flex-test
```

2. Push this project:

```bash
cd /Users/peng_gu/Desktop/Work/line-liff-flex-test
git init
git branch -M main
git add .
git commit -m "Add LIFF Flex Message share test"
git remote add origin git@github.com:YOUR_GITHUB_USER/line-liff-flex-test.git
git push -u origin main
```

3. In GitHub, open the repo settings:

```text
Settings -> Pages -> Build and deployment -> Source -> GitHub Actions
```

4. Open the Actions tab and wait for `Deploy to GitHub Pages` to finish.

5. Your HTTPS URL should look like:

```text
https://YOUR_GITHUB_USER.github.io/line-liff-flex-test/
```

Use that full URL as the LIFF endpoint URL in the LINE Developers Console.

Then use this URL from the Airbnb debug button. The picker opens automatically after LIFF init/login:

```text
https://liff.line.me/2010072810-4TWyKraj
```

Use this manual mode URL if you want to land on the test page first:

```text
https://liff.line.me/2010072810-4TWyKraj?auto=0
```

### Alternative: Vercel / Netlify / Cloudflare Pages

Deploy the `public/` directory. Examples:

```bash
cd /Users/peng_gu/Desktop/Work/line-liff-flex-test
```

Vercel:

```bash
vercel deploy --prod public
```

Netlify:

```bash
netlify deploy --prod --dir public
```

Cloudflare Pages:

```bash
wrangler pages deploy public --project-name line-liff-flex-test
```

After deploy, use the resulting HTTPS URL as the LIFF endpoint URL, for example:

```text
https://line-liff-flex-test.example.pages.dev/
```

## Endpoints

- `GET /` serves the LIFF test page.
- `GET flex-message.json` returns the full Flex Message from the same directory as the LIFF page:

```json
{
  "type": "flex",
  "altText": "Check out this Airbnb listing",
  "contents": {}
}
```

- `GET /api/flex-message` is also available only when running the local Node server.
- `GET /api/health` is also available only when running the local Node server.

## LIFF setup

Use LIFF ID:

```text
2010072810-4TWyKraj
```

Deploy this app to an HTTPS host, then configure the LIFF endpoint URL to that deployed root URL.

Use this test URL from the Airbnb debug button. The picker opens automatically after LIFF init/login:

```text
https://liff.line.me/2010072810-4TWyKraj
```

Use this manual mode URL if you want to land on the test page first:

```text
https://liff.line.me/2010072810-4TWyKraj?auto=0
```

## Notes

- The Flex JSON source is `data/pdp.json`.
- The page displays the current LINE user's display name, user ID, profile image, and email when those scopes are available.
- Email requires the LINE Login channel and LIFF app to include the email scope and requires the user to authorize it.
- This app intentionally does not use LINE Messaging API or LINE iOS SDK.
- The receiver is selected by the LINE user in the target picker.
