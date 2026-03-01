# Sunray Ecosystem Feedback Integration

This repo now contains a deploy-ready **Google Form style feedback system** with:

- 3-step feedback collection flow
- AI review analysis (OpenRouter)
- Direct admin email delivery (EmailJS)
- Optional Google Sheets sync via Apps Script webhook
- Simple in-app feedback dashboard for triage

## Files

- `index.html` — Complete React/Tailwind single-file app for feedback form + dashboard.
- `.github/workflows/vercel-auto-deploy.yml` — Vercel production deployment on push to `main` or `master`.

## Configure keys (required)

Do **not** hardcode secrets in source. Configure at runtime:

```html
<script>
  window.__SUNRAY_CONFIG__ = {
    OPENROUTER_API_KEY: 'sk-or-...',
    EMAILJS_SERVICE_ID: 'service_xxxxx',
    EMAILJS_TEMPLATE_ID: 'template_xxxxx',
    EMAILJS_PUBLIC_KEY: 'public_xxxxx',
    GOOGLE_SHEETS_WEBHOOK: 'https://script.google.com/macros/s/.../exec'
  };
</script>
```

Add this snippet before the Babel script block in `index.html` or inject equivalent values from your hosting environment.

## Deploy flow

1. Push to `main`/`master`.
2. GitHub Actions workflow runs.
3. Vercel deploys production automatically.

## GitHub Actions secrets (for deploy workflow)

- `VERCEL_TOKEN`
- `VERCEL_ORG_ID`
- `VERCEL_PROJECT_ID`

## Notes

- If OpenRouter key is missing, the app falls back to neutral/manual AI analysis.
- If EmailJS fields are missing, email send is skipped but form submission still works in-app.
- If Google Sheets webhook is configured, each feedback submission is POSTed as JSON.
