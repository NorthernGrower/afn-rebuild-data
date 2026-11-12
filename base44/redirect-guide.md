# Redirect plan: old AFN URLs -> new site URLs

Goal: nothing that used to work should 404. Every old URL either maps to the
rebuilt page with the same content ID, or falls back to the closest section.

## Rule 1 — same path scheme, same IDs (best case)
Build the new site on the old XenForo scheme and keep old IDs:
- /forums/forums/<slug>.<id>/  (forum sections)
- /forums/threads/<slug>.<id>/ (threads; trailing number = old thread ID)
- /forums/posts/<id>/          (post permalinks)
- /forums/members/<slug>.<id>/ (members)
- /forums/tags/<name>/         (tags)
If Base44 can generate URLs like /forums/threads/<anything>.<old-id>/, then a
single wildcard redirect per section fixes thousands of URLs at once, because
the old ID is embedded in every old URL.

## Rule 2 — explicit map for changed IDs
Where new IDs differ, generate a map from the lists in this folder:
- threads.txt        -> old thread IDs (parse "<slug>.<id>" before the /)
- posts.txt          -> old post IDs (/posts/<id>/)
- members.txt        -> old member slugs/ids
- tags.txt           -> old tags, incl. legacy tags.php?tag=<name>
- legacy-vbulletin.txt -> showthread.php/<id>-<slug> (oldest links)
Format (nginx map / edge-worker / Cloudflare bulk redirect):
  /forums/threads/00-afghan-mass.46262/  ->  /forums/threads/<new>.<new-id>/
  /forums/showthread.php/1013-...        ->  /forums/threads/<new>.<new-id>/

## Rule 3 — fallbacks (no 404 ever)
  /forums/threads/*        -> search page or forum index
  /forums/forums/*         -> forum index (or matching new section)
  /forums/members/*        -> member directory
  /forums/tags*|tags.php*  -> tags page
  /forums/attachments/*    -> Wayback copy (see below)
  /forums/showthread.php/* -> forum index
Everything else under /forums/ -> forum index (301, not 404).

## Images
Old attachments: /forums/attachments/<name>.<id>/ (78,607 listed in
attachments.txt). Redirect each to the archived copy:
  https://web.archive.org/web/2021im_/https://www.autoflower.net<old path>
Do this at the redirect layer, not in post HTML — then posts can reference
images by their old paths and they keep working.

## Search engines
- Ship redirects before/with launch, same-day.
- Submit a fresh sitemap in Google Search Console; watch Pages > 404 report
  decline over the following weeks.
- 301s pass link equity; never use JS/client-side redirects for these.

## Caveats
- Lists only cover what the Wayback Machine crawled (status 200).
  Cross-check Google Search Console's 404 report for gaps.
- Normalize host variants (http/https, www, :80) to one canonical host.
- Pagination variants (page-2, ?page=2, /page2) redirect with their parent.
