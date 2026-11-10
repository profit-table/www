# ProfitTable — www

The public information site about the ProfitTable product. Today it's a blank placeholder (`index.html`, "noSite").

## The ProfitTable repos

```
~/Sites/
│
├── ProfitTable-www/  ──────────────→  github.com/profit-table/www
│     Public information site about the ProfitTable product.
│     Blank placeholder for now.
│
├── ProfitTable-sta/  ──────────────→  github.com/profit-table/sta
│   │ Source for the Vue 3 custom HTML tags (STA).
│   │ Has its own CLAUDE.md — read it before touching sta.
│   │
│   └── dist/  ─────────────────────→  github.com/profit-table/app
│         Its own git repo (sta's .gitignore excludes dist).
│         `yarn build` in sta writes here; commit and push from dist/ to the app repo.
│
└── ProfitTable-icon/  ─────────────→  github.com/profit-table/icon
      Favicons and app icons, published publicly on GitHub Pages.
      www, app, sta and anything else link to it:

            www ──┐
            app ──┼──→  icon (GitHub Pages)
            sta ──┘
```

The only links between repos:

- **sta → app**: sta's build output is published as the app repo.
- **everything → icon**: icon links (`<link rel="icon">`, `apple-touch-icon`, manifest) point at the icon repo's
  GitHub Pages URL, not at copies in each repo.

www does not depend on sta or app.

## Known loose ends

- Icon Pages isn't enabled yet. The expected URL is `https://profit-table.github.io/icon/` — confirm once it's live.
- `index.html` still loads icons from `thebackoffice.github.io` (an old source). Switch to the icon repo once Pages is live.
- `vite build` empties `sta/dist` before writing. Vite should keep `dist/.git`, but other files there (e.g.
  `dist/README.md`) will be deleted. Check this before the first real build/publish.
- In the icon repo, `icon-512.png` and `icon-maskable.png` are the same byte size — probably the same file. A real
  maskable icon needs safe-zone padding.

## Working here

- Worktrees live in `.claude/worktrees/` (gitignored). Branch names follow `feat/… fix/… chore/… docs/…`.
- sta and icon are usually attached to the session as plain folders on their own `master`: branch there before editing.
