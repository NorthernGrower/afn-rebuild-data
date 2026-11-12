# BRIEF FOR BASE44 — Rebuilding The Autoflower Network (AFN)

Give this file (and the files it references) to Base44 first. It explains every
file in the /scratchpad/afn-urls/ folder and what to build from it.

## What we are building
A modern, mobile-first rebuild of the old Autoflower Network forums
(autoflower.net/forums — a XenForo site that replaced the original
vBulletin in ~2012, and went offline in ~2022). The look: a modern take on the
classic vBulletin/XenForo community — category blocks, forum sections with
thread/message counts, "latest post" rows, thread lists with pagination,
thread pages with posts, member profiles, tags, and a media gallery.

## Reference data files (all one URL per line unless noted)

| File | Contents | Use it for |
|---|---|---|
| base44/forum-structure.json | The complete old forum tree: categories, forums, IDs, descriptions, activity counts | Build the community section exactly like the original |
| base44/thread-content-format.md | A real archived thread, showing post structure, member info, strain-review fields | Template for how thread pages and posts should look/behave |
| base44/redirect-guide.md | How to map old URLs to new ones | Set up the redirect plan from day 1 |
| threads.txt | 61,897 archived thread URLs (each ends in /threads/<title-slug>.<id>/) | Thread catalog: title (from slug) + old thread ID for redirects |
| forum-index-pages.txt | 7,335 forum section URLs (+ pagination, RSS) | Forum slugs/IDs, pagination pattern |
| members.txt | 512 member profile URLs | Member directory seed |
| posts.txt | 55,991 post permalink URLs (/posts/<id>/) | Post-level permalinks for redirects |
| tags.txt | 6,453 tag URLs (incl. legacy vBulletin tags.php?tag=) | Tag pages + legacy tag redirects |
| legacy-vbulletin.txt | 840 pre-2012 vBulletin showthread.php URLs | Redirect the site's very oldest links too |
| attachments.txt | 78,607 attachment URLs (/attachments/<name>.<id>/) | Old images/files; see image strategy below |

Site totals from the last archived index (Nov 2021): 63,639 threads,
2,232,623 messages, 43,141 members, 41 gallery categories, 860 albums,
20,169 uploaded media.

## URL scheme to copy
Old XenForo scheme (keep it — it makes redirects nearly free):
- Forum: /forums/forums/<slug>.<id>/
- Thread: /forums/threads/<slug>.<id>/
- Post permalink: /forums/posts/<id>/
- Member: /forums/members/<slug>.<id>/
- Tag: /forums/tags/<name>/
- Attachment: /forums/attachments/<name>.<id>/
The trailing number IS the old content ID. Preserve IDs wherever possible so
every old URL maps 1:1 to a new one.

## Image strategy (do not try to rehost 78k images)
Serve archived copies straight from the Wayback Machine as a fallback:
https://web.archive.org/web/2021im_/<original attachment URL>
If an attachment URL now 404s, redirect it to that Wayback form. If we later
import images locally, the redirect map changes target — no old-URL change.

## Where the actual old content lives
Any archived page: https://web.archive.org/web/2021/<original URL>
Priority pages to recreate first (richest, most-linked content):
guides & tutorials, myth busters, strain/cultivar reviews, infirmary archives,
the biggest vendor sections (Mephisto, Dutch Passion, Sweet Seeds, Fast Buds).
