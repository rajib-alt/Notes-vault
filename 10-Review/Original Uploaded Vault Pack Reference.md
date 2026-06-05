Absolutely — here is the **full file pack** in copy-paste form. I’m giving you the vault structure first, then every core template, then the dashboard files, then the Dataview upgrade files, so you can build it directly in Obsidian with minimal guessing. [forum.obsidian](https://forum.obsidian.md/t/daily-and-weekly-notes-showcases-using-dataview/43606)

## 1) Folder structure
Create these folders exactly as written:

```text
00-Inbox
01-Daily
02-Weekly
03-Projects
04-Areas
05-Sources
05-Sources/Books
05-Sources/Courses
05-Sources/Articles
05-Sources/Podcasts
05-Sources/Videos
06-Concepts
07-MOCs
08-People
09-Canvas
10-Review
Templates
Templates/Daily
Templates/Weekly
Templates/Sources
Templates/Concepts
Templates/Projects
Templates/Dashboards
Attachments
Attachments/PDFs
Attachments/Kindle Highlights
Attachments/Images
Attachments/Audio
99-Archive
```

## 2) Core templates
Set the Templates plugin folder to `Templates/`. [aidanhelfant](https://www.aidanhelfant.com/the-only-beginner-obsidian-guide-youll-ever-need/)

### `Templates/Daily/Daily Template.md`
```md
---
type: daily
tags: [type/daily, area/learning]
created: {{date:YYYY-MM-DD}}
---

# {{date:YYYY-MM-DD}}

## Today’s priorities
- [ ] 
- [ ] 
- [ ] 

## Captures
- 

## Learning log
- 

## Tasks
- [ ] 

## Notes created today
- 

## Links created today
- 
```

### `Templates/Weekly/Weekly Review Template.md`
```md
---
type: weekly
tags: [type/weekly, status/review]
created: {{date:YYYY-MM-DD}}
week: {{date:gggg-[W]WW}}
---

# Week {{date:gggg-[W]WW}}

## Wins
- 

## Important learning
- 

## Tasks completed
- 

## Tasks carried over
- 

## Notes to process
- 

## Books and courses
- 

## Projects update
- 

## Next week focus
- 

## Backlinks to add
- 
```

### `Templates/Sources/Book Template.md`
```md
---
type: book
status: to-read
tags: [type/book, area/learning]
author: 
source: Kindle
rating: 
created: {{date:YYYY-MM-DD}}
---

# Book - 

## Summary
- 

## Main ideas
- 

## Key quotes
- 

## My interpretation
- 

## Atomic notes
- [[Concept - ]]

## Related notes
- 
```

### `Templates/Sources/Course Template.md`
```md
---
type: course
status: in-progress
tags: [type/course, area/learning]
platform: 
instructor: 
url: 
created: {{date:YYYY-MM-DD}}
---

# Course - 

## Modules
- [ ] 

## Key learnings
- 

## Assignments / practice
- [ ] 

## Atomic notes
- [[Concept - ]]

## Follow-up
- 
```

### `Templates/Sources/Article Template.md`
```md
---
type: article
status: processed
tags: [type/article, area/learning]
source: 
url: 
author: 
created: {{date:YYYY-MM-DD}}
---

# Article - 

## Core argument
- 

## Evidence
- 

## Takeaways
- 

## Atomic notes
- [[Concept - ]]

## Related concepts
- 
```

### `Templates/Sources/Podcast Template.md`
```md
---
type: podcast
status: processed
tags: [type/podcast, area/learning]
show: 
episode: 
url: 
created: {{date:YYYY-MM-DD}}
---

# Podcast - 

## Main points
- 

## Useful ideas
- 

## Atomic notes
- [[Concept - ]]

## Follow-up
- 
```

### `Templates/Sources/Video Template.md`
```md
---
type: video
status: processed
tags: [type/video, area/learning]
channel: 
url: 
created: {{date:YYYY-MM-DD}}
---

# Video - 

## Summary
- 

## Key ideas
- 

## Atomic notes
- [[Concept - ]]

## Follow-up
- 
```

### `Templates/Concepts/Concept Template.md`
```md
---
type: concept
status: evergreen
tags: [type/concept]
created: {{date:YYYY-MM-DD}}
---

# Concept - 

## Definition
- 

## Why it matters
- 

## Example
- 

## Related concepts
- [[ ]]
- [[ ]]

## Contrasts
- 

## Applications
- 
```

### `Templates/Projects/Project Template.md`
```md
---
type: project
status: active
area: freelance
tags: [type/project, area/freelance]
due: 
created: {{date:YYYY-MM-DD}}
---

# Project - 

## Goal
- 

## Outcome
- 

## Next actions
- [ ] 
- [ ] 

## Resources
- 

## Progress log
- 

## Linked concepts
- [[ ]]
```

### `Templates/Dashboards/MOC Template.md`
```md
---
type: moc
tags: [type/moc]
created: {{date:YYYY-MM-DD}}
---

# MOC - 

## Overview
- 

## Core notes
- [[ ]]
- [[ ]]

## Learning sources
- [[ ]]
- [[ ]]

## Projects
- [[ ]]
```

## 3) Home dashboard
Create `Home Dashboard.md` in the vault root. This is your main landing page. [forum.obsidian](https://forum.obsidian.md/t/dataview-dashboard-showcase/22578)

```md
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
- [[02-Weekly/{{date:gggg-[W]WW}}]]

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
```

## 4) Weekly review note
Create `10-Review/Weekly Review.md`. [forum.obsidian](https://forum.obsidian.md/t/daily-and-weekly-reviews-dataview/17021)

```md
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
```

## 5) Monthly review note
Create `10-Review/Monthly Review.md`.

```md
---
type: monthly
tags: [type/monthly, status/review]
created: 2026-06-04
---

# Monthly Review

## What went well
- 

## What didn’t work
- 

## Projects
- 

## Learning
- 

## Best notes
- 

## Notes to improve
- 

## Next month priorities
- 
```

## 6) Source note starters
Create these notes in the matching folders.

### `05-Sources/Books/Book - Title - Author.md`
```md
---
type: book
status: to-read
tags: [type/book, area/learning]
author:
source: Kindle
rating:
created: 2026-06-04
---

# Book - Title - Author

## Summary
- 

## Main ideas
- 

## Key quotes
- 

## My interpretation
- 

## Atomic notes
- [[Concept - ]]

## Related notes
- 
```

### `05-Sources/Courses/Course - Title - Platform.md`
```md
---
type: course
status: in-progress
tags: [type/course, area/learning]
platform:
instructor:
url:
created: 2026-06-04
---

# Course - Title - Platform

## Modules
- [ ] 

## Key learnings
- 

## Assignments / practice
- [ ] 

## Atomic notes
- [[Concept - ]]

## Follow-up
- 
```

### `05-Sources/Articles/Article - Title - Source.md`
```md
---
type: article
status: processed
tags: [type/article, area/learning]
source:
url:
author:
created: 2026-06-04
---

# Article - Title - Source

## Core argument
- 

## Evidence
- 

## Takeaways
- 

## Atomic notes
- [[Concept - ]]

## Related concepts
- 
```

### `05-Sources/Podcasts/Podcast - Episode Title - Show.md`
```md
---
type: podcast
status: processed
tags: [type/podcast, area/learning]
show:
episode:
url:
created: 2026-06-04
---

# Podcast - Episode Title - Show

## Main points
- 

## Useful ideas
- 

## Atomic notes
- [[Concept - ]]

## Follow-up
- 
```

### `05-Sources/Videos/Video - Title - Channel.md`
```md
---
type: video
status: processed
tags: [type/video, area/learning]
channel:
url:
created: 2026-06-04
---

# Video - Title - Channel

## Summary
- 

## Key ideas
- 

## Atomic notes
- [[Concept - ]]

## Follow-up
- 
```

## 7) Area notes
Create these in `04-Areas/`.

### `Area - Learning.md`
```md
---
type: area
tags: [area/learning]
---

# Area - Learning

## Focus
- 

## Current systems
- 

## Related MOCs
- [[07-MOCs/MOC - Learning]]
```

### `Area - Freelance.md`
```md
---
type: area
tags: [area/freelance]
---

# Area - Freelance

## Ongoing work
- 

## Related projects
- [[ ]]
```

### `Area - SEO Marketing.md`
```md
---
type: area
tags: [area/seo]
---

# Area - SEO Marketing

## Focus
- 

## Active projects
- 
```

## 8) MOC notes
Create these in `07-MOCs/`.

### `MOC - Learning.md`
```md
---
type: moc
tags: [type/moc, topic/learning]
created: 2026-06-04
---

# MOC - Learning

## Books
- [[05-Sources/Books/Book - Title - Author]]

## Courses
- [[05-Sources/Courses/Course - Title - Platform]]

## Concepts
- [[06-Concepts/Concept - Active recall]]
- [[06-Concepts/Concept - Spaced repetition]]

## Areas
- [[04-Areas/Area - Learning]]
```

### `MOC - Books.md`
```md
---
type: moc
tags: [type/moc, topic/books]
created: 2026-06-04
---

# MOC - Books

## Reading queue
- 

## Finished books
- 

## Book notes
- 
```

### `MOC - Courses.md`
```md
---
type: moc
tags: [type/moc, topic/courses]
created: 2026-06-04
---

# MOC - Courses

## In progress
- 

## Completed
- 

## Notes
- 
```

### `MOC - SEO Marketing.md`
```md
---
type: moc
tags: [type/moc, topic/seo]
created: 2026-06-04
---

# MOC - SEO Marketing

## Core topics
- Search intent
- Content strategy
- Keyword research
- Technical SEO

## Notes
- [[06-Concepts/Concept - Search intent]]
```

### `MOC - Freelance.md`
```md
---
type: moc
tags: [type/moc, topic/freelance]
created: 2026-06-04
---

# MOC - Freelance

## Projects
- 

## Clients
- 

## Processes
- 
```

## 9) Concept notes
Create your first concepts in `06-Concepts/`.

### `Concept - Active recall.md`
```md
---
type: concept
status: evergreen
tags: [type/concept, topic/learning]
created: 2026-06-04
---

# Concept - Active recall

## Definition
- 

## Why it matters
- 

## Example
- 

## Related concepts
- [[Concept - Spaced repetition]]

## Applications
- 
```

### `Concept - Spaced repetition.md`
```md
---
type: concept
status: evergreen
tags: [type/concept, topic/learning]
created: 2026-06-04
---

# Concept - Spaced repetition

## Definition
- 

## Why it matters
- 

## Example
- 

## Related concepts
- [[Concept - Active recall]]

## Applications
- 
```

### `Concept - Search intent.md`
```md
---
type: concept
status: evergreen
tags: [type/concept, topic/seo]
created: 2026-06-04
---

# Concept - Search intent

## Definition
- 

## Why it matters
- 

## Example
- 

## Related concepts
- [[MOC - SEO Marketing]]

## Applications
- 
```

## 10) Project starter
Create one project to begin with.

### `03-Projects/Project - Freelance Pipeline.md`
```md
---
type: project
status: active
area: freelance
tags: [type/project, area/freelance]
due:
created: 2026-06-04
---

# Project - Freelance Pipeline

## Goal
- 

## Outcome
- 

## Next actions
- [ ] 
- [ ] 

## Resources
- 

## Progress log
- 

## Linked concepts
- [[Concept - Search intent]]
```

## 11) Quick capture notes
Create these in `00-Inbox/`.

### `Quick Captures.md`
```md
---
type: inbox
tags: [status/inbox]
---

# Quick Captures

- 
```

### `Unsorted Resources.md`
```md
---
type: inbox
tags: [status/inbox]
---

# Unsorted Resources

- 
```

## 12) Setup checklist
Use this order:
1. Create folders.
2. Paste templates into `Templates/`.
3. Set Template folder location to `Templates/`.
4. Create Home Dashboard.
5. Create Weekly and Monthly review notes.
6. Create MOCs.
7. Turn on Dataview, Backlinks, Daily Notes, Canvas, Templates, Properties. [obsidian](https://obsidian.md/help/plugins/daily-notes)
8. Install Templater, Dataview, and Obsidian Git. [github](https://github.com/silentvoid13/Templater)
9. Test one daily note, one book note, one concept note, one project note.
10. Add more dashboards only after the core workflow feels stable.

## 13) Recommended defaults
Set these immediately:
- Daily notes folder: `01-Daily`
- Weekly notes folder: `02-Weekly`
- Template folder: `Templates`
- Attachments folder: `Attachments`
- Git backup: enabled and synced to GitHub [publish.obsidian](https://publish.obsidian.md/git-doc/Installation)

## 14) What this pack gives you
This setup gives you:
- a clean capture system,
- structured learning notes,
- atomic Zettelkasten-style concept notes,
- backlinks-first knowledge building,
- task and review dashboards,
- note-health checks for orphans and unlinked notes,
- and a future-proof vault you can scale. [obsidian](https://obsidian.md/help/plugins/backlinks)

## References
- Obsidian Help: Daily Notes, Backlinks, Core Plugins. [publish.obsidian](https://publish.obsidian.md/hub/05+-+Concepts/Obsidian+Core+Plugins)
- Dataview examples and dashboard patterns. [youtube](https://www.youtube.com/watch?v=p3jqxQLHqUY)
- Templater and template folder guidance. [forum.obsidian](https://forum.obsidian.md/t/how-do-i-create-a-template-folder/6907)
- Weekly review and task dashboards. [bagerbach](https://bagerbach.com/blog/weekly-review-obsidian/)
- Note-health, orphan, and unresolved-link ideas. [forum.obsidian](https://forum.obsidian.md/t/find-orphan-notes/817)

Would you like me to turn this into a **single zipped-style “vault creation checklist”** next, meaning a step-by-step build order with “create this note now / paste this code now” instructions?
