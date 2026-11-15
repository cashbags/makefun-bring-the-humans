# bring-the-humans-01 — TESTS

Date: 2026-11-15 (WIB). Competition closes 2026-11-16T18:00:00Z (01:00 WIB 17 Nov).
Entry: ad page + screenshot carrying the account's own referral code.
No spend, no push, no submit in this task (local build only).

## Referral code (rank-1: live API)
- `GET /api/me/referrals` returned status 200, code `6sknhk5z`,
  link `https://make.fun/r/6sknhk5z` (rewards: signup $0.25, limit 20,
  counted 0). Script: `../get-referral.js` (reads the agent API key from
  `~/.makefun/credentials`, prints only the referral payload, never the key).
- Note: the user's invite link `https://make.fun/r/qrg7fvky` is a DIFFERENT
  code (the invite the user came in on). The page must carry the ACCOUNT's
  own code, so `6sknhk5z` is used, not `qrg7fvky`.

## Ad page (index.html, 12,201 bytes)
- Own design (not the starter copy): press-kit palette (accent #bc0c7c,
  ink #191419, canvas #faf8fa), make.fun logo SVG from the kit's press
  assets, headline "Put your AI agent in the running.", invite card with
  the bare code `6sknhk5z` in 44px mono and the full link
  `https://make.fun/r/6sknhk5z` as visible text + href, CTA button to the
  same link, 3-step "how it works" strip, "Live now" tag strip, footer.
- Referral code present in the page: 4 occurrences of `6sknhk5z`
  (bare code, `https://make.fun/r/6sknhk5z` x2 in hrefs, 1 visible link
  text, 1 in the meta description).
- Written in 2 passes: full draft, then a revision adding the "Live now"
  strip, then two spacing trims to fit the 800px viewport exactly.

## Screenshot (ad.png, 116,672 bytes, PNG 1280x800)
- `/opt/meta-chromium/chrome` (the VM's bundled Chromium) REFUSES to start
  from shell: `Hatch WebGL domain policy is required for browser startup`
  (both `--headless` and `--headless=new`). It is harness-launched only.
- Workaround: `npm install puppeteer` in `/tmp/shot` (3 min, downloads
  Chrome for Testing to `~/.cache/puppeteer`), then `/tmp/shot/shot.js`
  (viewport 1280x800, deviceScaleFactor 1, `headless: 'shell'`).
- Final render: `scrollW=1280, scrollH=800, innerW=1280, innerH=800` — the
  whole page fits the viewport with no scroll, no horizontal overflow.
  PNG is 116,672 bytes (< 2 MB limit from the starter comment).
- Verified by reading the image: headline, lede, CTA, invite card with
  code `6sknhk5z` and link `https://make.fun/r/6sknhk5z` all visible;
  3 step cards, "Live now" tags, footer all render correctly.

## Kit check (from the unpacked kit, no --transcripts)
Command: `node cli/makefun.mjs check --kit . --repo <entry>`
Full output in CHECK.md. Final run (commit 3abf8b4e):
- **4 passed:** competition_open, snapshot (5 files, 140,178 bytes),
  license_osi (MIT, after adding the `SPDX-License-Identifier: MIT` line —
  the first run FAILED license_osi because the LICENSE lacked it),
  ad_page (index.html carries referral link 6sknhk5z; ad.png is a PNG).
- **1 failed:** transcripts_present — expected, no bundle was created in
  this local-only task (parent bundles at submit time).
- **12 skipped:** strategy_note, committed_secret, all transcript checks.
- **5 checked at submission (pending push):** repo_public, repo_owner
  (owner.json present with the agent wallet), repo_created_after_open,
  commit_in_repo, duplicate_snapshot.
- Verdict: "not ready: fix transcripts_present, then check again"

## Files (entry dir)
- index.html (12,201 bytes) — entrypoint
- ad.png (116,672 bytes, PNG 1280x800) — screenshot of the page
- LICENSE (MIT, with SPDX line)
- .makefun/owner.json — {"wallet": "4vJXnxMrsBrtXoHRWkDUXh2ydserPugEKeDyF7CPMB8L"}
- TESTS.md (this file), CHECK.md (full check output)
- Local git commit: 3abf8b4e4fd727cba626c5164e19798ef6d43616
