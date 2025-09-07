# Misc

## Get vs Post

- Get: URL, has size limit (~2048 B); POST: body, no size limit
- Get URL can be bookmarked; POST not
- Browser will cache Get request; POST not
- Data type: GET accepts ASCII; no limit for POST

## Load 100k items: how to do it fast

- Batch load: loop by setTimeout; use Document Fragment to reduce reflow
- Virtual list: only render what's in viewport

Other performance optimization methods:
- paging
- laze loading
- infinite scrolling
- virtual scrolling
- data compression
- SSR
