# ProfitTable — www

The public information site about the ProfitTable product. No GUI yet: the root `index.html` is Tarek's standard
noSite placeholder (see global CLAUDE.md).

## The ProfitTable repos

ProfitTable follows the standard project structure in the global CLAUDE.md (sta → dist → app).

```
~/Sites/
│
├── ProfitTable-sta/  ─────────→  profit-table/sta
│   │ Source of the <tags/> (Vue 3 custom HTML tags). sta/index.html previews them as wireframes.
│   │ Has its own CLAUDE.md — read it before touching sta.
│   │
│   └── dist/  ────────────────→  profit-table/dist   →  dist.profittable.ai
│         Local checkout of the dist repo (gitignored in sta).
│         The built runtime (app.js) that other sites load.
│
├── app  ──────────────────────→  profit-table/app    →  app.profittable.ai
│     The real public-facing product, built with the tags.
│     Loads <script src="https://dist.profittable.ai/app.js">. No local checkout yet.
│
├── ProfitTable-www/  ─────────→  profit-table/www    →  profittable.ai
│     Public information site. Does not depend on sta, dist or app.
│
└── ProfitTable-icon/  ────────→  profit-table/icon   →  icon.profittable.ai
      Favicons and app icons. Everything links to https://icon.profittable.ai/…
```

## Domains (profittable.ai)

Proxied CNAMEs to `cdn.profittable.ai`, whose A records are GitHub Pages' IPs (185.199.108–111.153).
Pages picks the repo by hostname, from each repo's `CNAME`.

| Hostname | Repo | CNAME file |
|---|---|---|
| `profittable.ai` | www | `profittable.ai` |
| `www.profittable.ai` | → redirect to `profittable.ai` (Cloudflare) | — |
| `dist.profittable.ai` | dist | `dist.profittable.ai` |
| `app.profittable.ai` | app | — |
| `icon.profittable.ai` | icon | `icon.profittable.ai` (live) |
| `api.profittable.ai` | api (server side) | Not set up yet |
| `sta.profittable.ai` | — | Undecided |

## Open

- sta's `yarn deploy` (tests → build → publish dist) isn't built yet; see the global CLAUDE.md "Build & publish".
  Until it is, `vite build` empties `sta/dist`, removing the dist repo's `CNAME` and `index.html` from the working copy.

## Working here

- Worktrees live in `.claude/worktrees/` (gitignored). Follow the global git Flow.
- sta, dist and icon are usually attached as plain folders on their own `master`: branch there before editing.
- With several repos attached, check `pwd` before every git command.
