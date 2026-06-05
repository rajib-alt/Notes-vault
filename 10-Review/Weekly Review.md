---
type: weekly
tags: [type/weekly, status/review]
created: 2026-06-04
---

# Weekly Review

## Wins
- 

## Open tasks
```dataview
TASK
FROM "03-Projects" OR "01-Daily" OR "10-Review"
WHERE !completed
SORT due asc
LIMIT 50
```

## New notes this week
```dataview
LIST
FROM ""
WHERE file.ctime >= date(today) - dur(7 days)
AND file.folder != "Templates"
AND file.folder != "99-Archive"
SORT file.ctime desc
LIMIT 30
```

## Notes to link
```dataview
LIST
FROM "06-Concepts"
WHERE length(file.inlinks) = 0 OR length(file.outlinks) = 0
SORT file.ctime desc
LIMIT 20
```

## Learning processing
- Books to convert into concepts.
- Courses to summarize.
- Articles to extract.
- Podcasts/videos to process.

## Next week
-
