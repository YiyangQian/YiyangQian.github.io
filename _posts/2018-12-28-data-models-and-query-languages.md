---
title: "Data Models and Query Languages"
layout: post
date: 2018-12-28
# image: /assets/images/adsk.JPG
headerImage: false
tag:
- markdown
- components
- extra
category: blog
author: YY
description: Markdown summary with different options
---

# Relational VS Document Databases
- Advantages of Documents Databases: 
    - schema flexibility, 
    - better performance due to locality, 
    - closer to the data structures used by the application
- Advantages of relational model:
    - better support for joins,
    - many-to-one and many-to-many relationships

### Schema flexibility in the document model
- Code that reads the data usually assumes some kind of structure, and implicit schema, but not enforced by the database
- schema-on-read vs schema-on-write(relational DB)
- For schema-on-write databases, schema changes are slow
    - MySQL copies the entire table on ALTER TABLE, taking long time

### Data locality for queries
Definition: a document is usually stored as a single continuous string.
- If your application often needs to access the entire document, data locality helps.
- If data is split across many tables, multiple index lookups are required, which may require more disk seeks. 

### Convergence of document and relational databases
- MySQL have supported XML 
- PostgreSQL, MySQL and IBM DB2 have supported JSON documents
- RethinkDB supports relational-like joins in its query language
- MongoDB drivers automatically resolve database references