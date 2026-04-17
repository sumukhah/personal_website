# Co-Founder OS Template

A minimal, no-nonsense one-page personal website template optimized for capturing signals from solid connections (e.g., potential co-founders) rather than serving as a traditional resume or portfolio. Built to run incredibly fast using **Astro**, styled with **Tailwind CSS**, and pre-configured for automated **GitHub Pages** deployment.

## Tech Stack
- [Astro](https://astro.build/) - Web framework optimized for speed.
- [Tailwind CSS](https://tailwindcss.com/) - Utility-first styling with a dark-mode, terminal-inspired glassmorphism theme.
- **Tally Forms** - Pre-configured layout for a seamless, headless lead qualification form.
- **Google Analytics** - Quick and easy pipeline hook setup (`gtag.js`).
- **GitHub Actions** - Automated deployment pipeline baked into `.github/workflows/deploy.yml`.

## Features
- **Micro-Interactions**: Subtle, responsive CSS animations to bring personality to the hero section.
- **Form Integration**: Skip building backend infrastructure. The contact section elegantly frames an external submission form.
- **Progressive Timeline**: Visualize professional and build history cleanly.

## Getting Started

1. Clone the repository
2. Run `npm install` to install dependencies
3. Replace the placeholder Google Analytics ID in `src/layouts/BaseLayout.astro`
4. Run `npm run dev` to start the local development server at `localhost:4321`

## Deployment

This repository is strictly configured to deploy directly to GitHub Pages. 

Whenever you push to the `main` branch, the Astro custom action intercepts the build, optimizes assets, and distributes to GitHub Pages. 
To launch your version, simply navigate to your repository's **Settings > Pages** and switch the build source to **GitHub Actions**.
