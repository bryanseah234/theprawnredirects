# PRD: theprawnredirects

## Overview
A Vercel redirect configuration repo that maps short vanity URLs to their canonical destinations on `hong-yi.me`. Used by "The Prawn" brand/collective to provide memorable short links for members and content. Zero code — entirely Vercel-native redirects.

## Goals
- Map short slugs (e.g. `/bryan`, `/bs234`) to full canonical URLs
- Map content paths (e.g. `/photos`, `/blog`) to blog sub-paths
- Map collective member paths to their dedicated pages
- Support both short and long slug variants for each destination

## Non-Goals
- Dynamic redirects (all are static)
- Analytics on redirect clicks
- Custom domain management
- Backend server

## User Stories
- As Bryan, I want to share `theprawnredirects.vercel.app/bryan` and have it redirect to my collective page.
- As a viewer, I want `/photos` to go directly to the photo collection blog post.

## Tech Stack
- **Config**: Vercel `vercel.json` redirects (no code)
- **Deployment**: Vercel

## Architecture
```
theprawnredirects/
└── vercel.json     # all redirect rules
```

## Redirect Map

| Source | Destination |
|--------|-------------|
| `/` | `https://hong-yi.me/` |
| `/about`, `/theprawnabout` | `https://hong-yi.me/theprawnabout` |
| `/collective`, `/theprawncollective` | `https://hong-yi.me/theprawncollective` |
| `/blog`, `/theprawnblog` | `https://hong-yi.me/theprawnblog` |
| `/privacy`, `/theprawnprivacy` | `https://hong-yi.me/theprawnprivacy` |
| `/my-two-cents` | `https://hong-yi.me/blog/my-two-cents` |
| `/video`, `/videos` | `https://hong-yi.me/blog/video-showcase` |
| `/photos` | `https://hong-yi.me/blog/photo-collection` |
| `/bryanseah234`, `/bryanseah`, `/bryan`, `/bs234`, `/bs` | `https://hong-yi.me/theprawncollective/bryanseah234` |
| `/shotsbyseah234`, `/shotsbyseah`, `/sbs`, `/shotbyseah` | `https://hong-yi.me/theprawncollective/shotsbyseah234` |
| `/prawnproductions234`, `/prawnproductions`, `/prawnproduction` | `https://hong-yi.me/theprawncollective/prawnproductions234` |

All redirects are `permanent: true` (HTTP 308).

## Deployment / Run
```bash
# No code to run — deploy via Vercel
vercel --prod
# or push to main and let Vercel auto-deploy
```

## Constraints & Notes
- **Permanent redirects**: `permanent: true` = HTTP 308; browsers and search engines cache these — changing a destination requires clearing browser cache
- **Destination domain**: `hong-yi.me` is the canonical home site; this repo just proxies short URLs to it
- **Maintenance**: add new redirect rules in `vercel.json` and redeploy
- **No fallback**: unmatched routes return Vercel's default 404
