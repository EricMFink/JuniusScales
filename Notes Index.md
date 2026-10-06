---
modified: 2026-08-26
---
```dataview
TABLE 
title as Title,
author as Author, 
year as Year,
type as Item, 
tags as Tags
FROM "notes"
SORT status DESC, read DESC
```