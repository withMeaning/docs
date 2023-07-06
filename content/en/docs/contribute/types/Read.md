---
title: "Read"
description: "Type for longform articles, like blogposts"
lead: ""
date: 2020-10-06T08:49:31+00:00
lastmod: 2020-10-06T08:49:31+00:00
draft: false
images: []
menu:
  docs:
    parent: "types"
weight: 554
toc: true
---

## The big question of what to read next

Books, blogposts, news? There is so much content to choose from! So with Meaning offers the core type `read`. This is just what you would expect, something to read, mainly sourced from RSS feeds or your favorite "Read Later" app.


## Properties

```
RequiredLake: True
RequiredAlgo: True
RequiredClient: False
NostrKind: 30023

{
  content: "Title"
  extra: {
    "source": "where the text is from, link to the RSS feed, if fetched"
    "body": "Markdown | string (RSS name: content)"
    "link?": "url if external source, DOI if paper"
    "summary?": "human generated summary"
    "ai-summary?": "ai generated summary"
  }
  type: "read"
}

```

Clients SHOULD implement a way to display the body as markdown, or embed the link as an iFrame / webpage.

Algorithms CAN create store embeddings or summaries that help the Algorithms to make decisions without having to parse the entire text.

Lakes SHOULD try to fetch the core text from websites and store them as markdown, as embedding the content as a webpage is unreliable and does not work offline.

Clients, Algorithms and Lakes CAN write AI summaries, if there is none provided by the author. These should be stored in the Lakes, esp. for publicly pulled blogposts.

TODO: how are PDFs / ebooks handled?