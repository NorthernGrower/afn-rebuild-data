# Autoflower.net /forums — archived URL lists (from the Wayback Machine CDX index)

Every file is one URL per line. These are all URLs that were crawled by the
Wayback Machine AND returned HTTP 200 (real content, not error pages), with
duplicate URLs collapsed. This is what Google/Bing had indexed over the years
and what now 404s.

## Files

| File | Lines | What it is |
|---|---|---|
| threads.txt | 61,897 | Thread pages: /forums/threads/<slug>.<id>/ (+ page-N pagination) |
| forum-index-pages.txt | 7,335 | Forum section pages: /forums/forums/<slug>.<id>/ (+ pagination + RSS) |
| members.txt | 512 | Member profiles |
| posts.txt | 55,991 | Post permalinks /forums/posts/<id>/ (+ /likes variants) |
| tags.txt | 6,453 | Tag pages (XenForo /tags/ and legacy vBulletin tags.php) |
| legacy-vbulletin.txt | 840 | Pre-XenForo vBulletin URLs: showthread.php/... |
| attachments.txt | 78,607 | Uploaded images/files: /forums/attachments/<name>.<id>/ |

## How to use them for the rebuild + redirects

1. **Thread IDs are the key.** Every thread URL ends in `<slug>.<id>`.
   Extract the IDs (a one-line script: strip everything after the last dot
   before the trailing slash). Same for attachments (`.NNNNNN` suffix) and
   posts (`/posts/<id>/`).
2. **Redirect maps.** If the rebuild keeps the same thread IDs (e.g. a
   XenForo import preserves IDs), redirects are trivial. Otherwise build a
   map file (nginx `map {}` or Apache `RewriteMap`) of
   `old path -> new URL`, generated from the ID lists.
3. **Bulk fallback rules** (put these in nginx/htaccess so nothing
   un-mapped 404s):
   - `/forums/threads/*` and `/forums/showthread.php/*` -> search or forum index
   - `/forums/forums/*` -> matching new forum section, else forum index
   - `/forums/members/*`, `/forums/tags/*`, `/forums/posts/*` -> closest equivalent
   - `/forums/attachments/*` -> you can redirect straight to the archived copy:
     `https://web.archive.org/web/2020/<old url>` to keep old posts' images alive
4. **Search engines.** After the rebuild ships, submit a fresh sitemap in
   Google Search Console and watch the Pages / "Not found (404)" report;
   the 301s above will drop the errors out of the index over weeks.
5. **Caveat:** the Wayback Machine only lists what it crawled. Cross-check
   Google Search Console's 404 report for pages it never archived. The
   URL scheme also contains protocol/host variants (http:80, https, www) —
   normalize to one host when building the map.

## Where the content itself lives

Wayback Machine snapshots of any URL: https://web.archive.org/web/2024/<URL>
Full capture timeline for any URL: https://web.archive.org/web/*/autoflower.net/forums/threads/*


## Base44 package

See the `base44/` subfolder — start with `base44/BRIEF.md`:
- `base44/forum-structure.json` — the complete old forum tree (17 categories, ~90 forums, IDs, descriptions, counts) plus site-wide stats
- `base44/thread-content-format.md` — how old thread pages/posts were structured (with a real archived example)
- `base44/redirect-guide.md` — the 3-rule redirect plan (same scheme + IDs, explicit map, fallbacks)
