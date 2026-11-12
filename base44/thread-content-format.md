# Old thread page format (from a real archived thread)

Use this as the template for how thread pages and posts must look and behave
in the rebuild. Source: https://web.archive.org/web/2021/https://www.autoflower.net/forums/threads/00-afghan-mass.46262/

## Thread page anatomy
- Page title: "<thread title> | The AutoFlower Network - AFN"
- Thread title: derived from the slug in /threads/<title-slug>.<id>/
  ("00-afghan-mass" -> "00 afghan mass")
- Posts in order, numbered (#1, #2, ...), each with:
  - Author: username, custom title/rank ("Auto Warrior", "Staff Member,
    Global Moderator"), join date, post count, likes received, reputation
  - Post body: rich text (may contain structured review fields, images,
    external embeds)
  - Date, permalink to /forums/posts/<post-id>/
  - Likes: named list of members who liked the post
- Tags listed at the end of the thread

## Structured first posts (strain reviews)
Review threads use labeled fields inside the first post — model these as
structured data in the rebuild:
- SeedBank / Strain / Did it autoflower?: Y|N
- Soil/hydro / Nutes / Light
- From seed to harvest date
- Dry Yield / High/Effect Duration
- Plant descriptions, RATE SCALE (1-10), BAG APPEAL, THE SMELL, THE HIGH,
  THE GROWTH, last thoughts
These same fields appear in /forums/rms/<slug>.<id>/ review items.

## Member profile fields seen on thread pages
username, slug, member id (from /members/<slug>.<id>/), custom title,
staff/role badges (Staff Member, Global Moderator, Product Tester tiers),
joined date, message count, likes received, reputation count,
"Currently Smoking" free-text field.

## Activity patterns worth recreating
- Reputation/rep points given between members with short messages
- Live chat mega-threads ("Live Stoner Chat - Oct-Dec '21")
- Grow journals as long-running photo threads
- Vendor sections with competitions (solo cup challenges, grow & show)
- User blogs at /forums/ubs/<slug>.<id>/ and media gallery at /forums/media/

## Getting full content for any thread
Wayback snapshot of that thread:
https://web.archive.org/web/2021/https://www.autoflower.net/forums/threads/<slug>.<id>/
Not every thread was captured; check availability with
https://web.archive.org/web/*/https://www.autoflower.net/forums/threads/<slug>.<id>/
