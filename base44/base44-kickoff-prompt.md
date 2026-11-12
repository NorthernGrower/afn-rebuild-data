# KICKOFF PROMPT (paste this into Base44)

---

You are building **The Autoflower Network (AFN)** — a modern, mobile-first
community site that recreates the old autoflower.net/forums (a XenForo forum,
offline since ~2022). Work from reference data hosted in a public GitHub repo.
Token discipline matters: do not read large files whole, do not crawl the web
for bulk data, and hand bulk work back to the user's external assistant.

## Read FIRST (in this order, once each — do not re-fetch)
1. https://raw.githubusercontent.com/NorthernGrower/afn-rebuild-data/main/base44/BRIEF.md
2. https://raw.githubusercontent.com/NorthernGrower/afn-rebuild-data/main/base44/forum-structure.json
3. https://raw.githubusercontent.com/NorthernGrower/afn-rebuild-data/main/base44/thread-content-format.md
4. https://raw.githubusercontent.com/NorthernGrower/afn-rebuild-data/main/base44/redirect-guide.md

## Token rules (strict)
- NEVER read these files in full or in bulk; they are data files, not docs:
  threads.txt, posts.txt, attachments.txt, forum-index-pages.txt,
  tags.txt, members.txt, legacy-vbulletin.txt (61k–79k lines each).
  If you think you need any of them: STOP, and output a DATA REQUEST
  block (format below). The user's external assistant will generate the
  exact file and push it to the repo for you.
- NEVER crawl the Wayback Machine (web.archive.org) yourself for bulk
  content. If archived thread content is needed, issue a DATA REQUEST
  listing the exact thread IDs/slug-ids — the external assistant fetches,
  extracts, and pushes cleaned content files to the repo.
- Never re-read a repo file you already read this session; keep a summary.
- Prefer one decisive build step over several exploratory ones. Do not
  generate sample data yourself when real data can be requested.

## DATA REQUEST block format (output exactly this when you need data)
DATA REQUEST
file: <suggested filename, e.g. redirect-map.csv>
columns: <exact columns>
source: <which repo file(s) to derive from, e.g. threads.txt>
filter/limit: <exact rules, e.g. unique thread ids only; first N=500 sorted by id>
purpose: <one line — what you will do with it>

## Build plan — Phase 1 (community scaffold)
Using forum-structure.json only (137 lines — read it fully):
- Data model: categories, forums (with parent/sub-forum relations,
  thread_count, message_count), threads (forum_id, slug, old_id, title,
  author_id, created_at, reply_count, view_count), posts (thread_id,
  author_id, body, created_at, likes), members (username, slug, old_id,
  title/rank, joined, post_count, likes_received, reputation), tags,
  media items.
- Pages: home (category blocks exactly mirroring the old hierarchy, with
  forum rows showing counts + latest-post), forum page (thread list with
  pagination), thread page (posts, author cards, likes, tags), member
  profile, member directory, tags page, search.
- Keep the old URL scheme (/forums/threads/<slug>.<old_id>/,
  /forums/forums/<slug>.<id>/, /forums/posts/<id>/, /forums/members/
  <slug>.<id>/, /forums/tags/<name>/) — old IDs must be stored on every
  record so redirects work (see redirect-guide.md).
- Style: modern take on classic vBulletin/XenForo — dense category blocks,
  clear section hierarchy, "Latest" column, member rank badges
  (Staff, Moderator, Product Tester tiers). Mobile-first.

## Build plan — Phase 2 (seed content, only after Phase 1 works)
- Request thread batches via DATA REQUEST (e.g. 200 threads per batch,
  cleaned from Wayback snapshots by the external assistant).
- Start with the richest sections: guides-tutorials, myth-busters,
  cultivar reviews, infirmary archive, top vendor forums (Mephisto,
  Dutch Passion, Sweet Seeds, Fast Buds).

## Build plan — Phase 3 (redirects)
- Once real content exists, request the generated redirect-map.csv via
  DATA REQUEST and load it as redirect rules; add the wildcard fallbacks
  from redirect-guide.md so nothing old 404s.

Start now with Phase 1. When you need data, output a DATA REQUEST block
and wait — do not fabricate or sample content on your own.
