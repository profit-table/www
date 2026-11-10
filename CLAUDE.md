# ProfitTable — www

The public information site about the ProfitTable product. No GUI yet: the root `index.html` is Tarek's standard
noSite placeholder (see global CLAUDE.md).

## The ProfitTable repos

```
~/Sites/
│
├── ProfitTable-www/  ──────────────→  github.com/profit-table/www
│     Public information site about the ProfitTable product.
│     No GUI yet (noSite placeholder).
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
- **everything → icon**: icon links (`<link rel="icon">`, `apple-touch-icon`, manifest) point at
  `https://icon.profittable.ai/…`, not at copies in each repo.

www does not depend on sta or app.

## Domains (profittable.ai)

All records are proxied CNAMEs to `cdn.profittable.ai`, whose A records are GitHub Pages' IPs
(185.199.108–111.153). Pages picks the repo by hostname, from each repo's `CNAME` file / Pages setting.

| Hostname | Repo | Status |
|---|---|---|
| `icon.profittable.ai` | icon | **Live** (CNAME fixed in icon `0b6b04c`) |
| `profittable.ai`, `www.profittable.ai` | www | Pages not confirmed yet |
| `app.profittable.ai` | app (`sta/dist`) | Pages not confirmed yet |
| `sta.profittable.ai` | sta | Purpose undecided — the sta repo is source and won't serve as-is |

## Known loose ends

- **app CNAME vs builds**: `vite build` empties `sta/dist`, so a `CNAME` file there is deleted on every build. Put
  `CNAME` (`app.profittable.ai`) in `sta/public/` so each build copies it into `dist/`. Vite should keep
  `dist/.git`, but other files in `dist/` are deleted — check before the first real build/publish.
- **Domain verification**: verify `profittable.ai` in the profit-table org (Pages → verified domains) so no other
  account can claim a subdomain pointed at GitHub.
- **Proxy + HTTPS**: if a Pages domain check fails or no certificate is issued, set that record to DNS-only until
  GitHub issues the cert, then re-enable the proxy and tick **Enforce HTTPS**.
- In the icon repo, `icon-512.png` and `icon-maskable.png` are the same byte size — probably the same file. A real
  maskable icon needs safe-zone padding.

## Working here

- Worktrees live in `.claude/worktrees/` (gitignored). Branch names follow `feat/… fix/… chore/… docs/…`.
- sta and icon are usually attached to the session as plain folders on their own `master`: branch there before editing.
- Shell commands may run from a different repo than you expect when several are attached — check `pwd` before git commands.
