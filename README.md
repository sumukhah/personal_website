# Sumukha QR Founder Site

Single-page Astro landing page for `sumukhah.github.io`, designed for QR scans from the YC co-founder T-shirt.

## Stack

- Astro
- Tailwind CSS v4
- Static deployment for GitHub Pages
- Tally for the two-field contact flow

## Local development

```sh
npm install
cp .env.example .env
npm run dev
```

Add your published Tally form URL to `.env`:

```sh
PUBLIC_TALLY_FORM_URL=...
```

## Production build

```sh
npm run build
```

## Deployment notes

- The site is configured for the root GitHub Pages domain: `https://sumukhah.github.io`
- The contact section requires `PUBLIC_TALLY_FORM_URL` to be present at build time
- The Tally form itself should contain only the 2 agreed fields
