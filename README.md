# Arabic Streaming & Video-Host Blocklist

A small, self-maintained DNS blocklist for AdGuard Home. It blocks free/pirate
**Arabic streaming portals** and the generic **video file-hosts and embed players**
they rely on, to cut down time and data spent on video streaming at home.

The list was built from real query-log analysis on a home network, not scraped
in bulk — so it's short, readable, and easy to prune.

## Add it to AdGuard Home

1. Open AdGuard Home → **Filters → DNS blocklists → Add blocklist → Add a custom list**.
2. Fill in:
   - **Name:** `Arabic Streaming`
   - **URL:**
     ```
     https://raw.githubusercontent.com/Sa6ry/arabic-streaming-blocklist/main/arabic-streaming.txt
     ```
3. Save. AdGuard fetches and enables it immediately.
4. Move the same domains **out** of *Filters → Custom filtering rules* so you're
   not maintaining them in two places. From here on, edit this repo instead.

AdGuard re-checks the list roughly daily (`! Expires: 1 day`). To force an update,
hit **Check for updates** on the Filters page.

## How it's organized

`arabic-streaming.txt` is grouped into commented sections:

| Section | What's in it |
| --- | --- |
| Arabic streaming / drama & series portals | Front-end sites she opens (q-drama, ahwaktv, MBC, Tubi, …) |
| Video file-hosts & embed players | The players the portals embed (mixdrop, voe, streamtape, dood, filemoon, vidmoly, vidhide, uqload, …) |
| StreamWish "wish" family | hlswish / obeywish embed players |
| Ad / pop-under / redirect domains | Malvertising domains bundled with those players |
| Broad — dual-use | `vk.com`, `ok.ru`, `workers.dev` — abused for embeds but also legitimate; review if something breaks |

## Maintaining it

- **Block a new site:** add a line `||newsite.com^`, bump `! Version:` and
  `! Last modified:` in the header, commit, and push. AdGuard picks it up on its
  next refresh.
- **Unblock a site:** delete or comment its line (prefix with `! `).
- **Syntax:** standard Adblock/AdGuard rules. `||domain^` blocks the domain and
  all its subdomains. A line starting with `!` is a comment (disabled).

## Notes / caveats

- `workers.dev` blocks **all** Cloudflare Workers apps — broad. Kept because a
  player was seen hosted there; remove it if a legitimate app stops working.
- `vk.com` and `ok.ru` are large social networks; blocking them fully is a
  deliberate, aggressive choice.
- Blocking is DNS-level: it stops the domains from resolving. A determined user
  on a VPN or with hard-coded DNS can bypass it — pair with router-level DNS
  enforcement if that matters.
