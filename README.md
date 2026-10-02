# web/

Static pages that need a public URL. `web/legal/` is generated from the app's own legal copy
(`app/src/features/legal/content.ts`) by `node --experimental-strip-types tools/legal-pages.mjs` (plain `node` on Node 24+),
so the app and the web pages never drift. Re-run after editing the copy; commit the output.

Hosting: GitHub Pages through the `pages` workflow (`.github/workflows/pages.yml`) — it publishes this folder on every
push to `main` that touches `web/`. One-time switch on GitHub: repo **Settings → Pages → Build and deployment → Source:
GitHub Actions** (the "Deploy from branch" option cannot publish a `/web` folder — only `/` or `/docs`). The first run then
gives `https://lux33bot.github.io/versy/legal/privacy.html` (the Actions run shows the exact URL). App Store Connect wants
the privacy URL; the Play Console wants both. A custom domain later changes nothing but the URL you paste there.

Until counsel replaces the `[COUNSEL]` sections the pages carry a "Draft" banner. App review wants a real policy at the
privacy URL, so that replacement is on the launch checklist.

`go.html` is the landing page for shared links: `…/go.html?to=/entry/<id>` opens the app when it is installed and offers
the download when it is not. Set `EXPO_PUBLIC_WEB_ORIGIN=https://lux33bot.github.io/versy` in `app/.env` and every
share from the app uses it (needs an `eas update` after the change). Fill the App Store link in `go.html` once the app
is listed.
