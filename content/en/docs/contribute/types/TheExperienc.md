---
title: "The Experience"
description: "Or Spiles"
lead: ""
date: 2020-10-06T08:49:31+00:00
lastmod: 2020-10-06T08:49:31+00:00
draft: false
images: []
menu:
  docs:
    parent: "types"
weight: 550
toc: true
---

## The Default Type

```
{
    "things": [
        {
            "id": "uuid",
            "author": "name of creator (name, username, twitter handle, nostr pubkey)",
            "content": "text for most types, title for articles, number if type resonance",
            "extra": {
              "main_content?": "Markdown of the main content",
              "link?": "url to external website, or id of event if type _*",
              "summary?": "AI or human generated summary of content",
              ...
            }
            "type": "experience",
            "created_at": 1679940469,
        },
    ]
}
```