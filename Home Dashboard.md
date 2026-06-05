---
type: dashboard
tags: [status/home]
created: 2026-06-04
---

# Home Dashboard

## Capture
- [[00-Inbox/Quick Captures]]
- [[00-Inbox/Unsorted Resources]]

## Today
- [[01-Daily/{{date:YYYY-MM-DD}}]]

```dataview
TASK
FROM "03-Projects" OR "01-Daily" OR "10-Review"
WHERE due = date(today)
SORT due asc
```

## Next actions
```dataview
TASK
FROM "03-Projects" OR "01-Daily"
WHERE !completed
SORT due asc
LIMIT 20
```

## This week
- [[02-Weekly/{{date:gggg-[W]WW}]]

## Active projects
```dataview
TABLE status, area, due
FROM "03-Projects"
WHERE type = "project" AND status != "done"
SORT due asc
```

## Books in progress
```dataview
TABLE author, status, rating
FROM "05-Sources/Books"
WHERE type = "book" AND status != "done"
SORT file.ctime desc
```

## Courses in progress
```dataview
TABLE platform, status
FROM "05-Sources/Courses"
WHERE type = "course" AND status != "done"
SORT file.ctime desc
```

## Other sources
```dataview
TABLE source, status
FROM "05-Sources"
WHERE type = "article" OR type = "podcast" OR type = "video"
SORT file.ctime desc
LIMIT 12
```

## Recent atomic notes
```dataview
LIST
FROM "06-Concepts"
SORT file.ctime desc
LIMIT 10
```

## Notes needing links
```dataview
LIST
FROM "06-Concepts"
WHERE length(file.inlinks) = 0 OR length(file.outlinks) = 0
SORT file.ctime desc
LIMIT 10
```

## Orphan notes
```dataview
LIST
FROM ""
WHERE length(file.inlinks) = 0 AND length(file.outlinks) = 0
AND file.folder != "Templates"
AND file.folder != "99-Archive"
SORT file.ctime desc
```

## People to review
```dataview
LIST
FROM "08-People"
SORT file.ctime desc
LIMIT 10
```

## Review
- [[10-Review/Weekly Review]]
- [[10-Review/Monthly Review]]

## Main MOCs
- [[07-MOCs/MOC - Learning]]
- [[07-MOCs/MOC - Books]]
- [[07-MOCs/MOC - Courses]]
- [[07-MOCs/MOC - SEO Marketing]]
- [[07-MOCs/MOC - Freelance]]
