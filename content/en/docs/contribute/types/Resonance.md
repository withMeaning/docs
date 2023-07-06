---
title: "_Resonance"
description: "Internal Type for storing quick user feedback"
lead: ""
date: 2020-10-06T08:49:31+00:00
lastmod: 2020-10-06T08:49:31+00:00
draft: false
images: []
menu:
  docs:
    parent: "types"
weight: 570
toc: true
---

## How meaningful was that?

The goal of with Meaning is to fill your entire day with meaningful experiences. This can only be achieved if you and your algorithm know what and what isn't meaningful to you. So we are asking after every recommendation: how much did this resonate with you?

In our hosted offering, you can give this simple feedback just by swiping left or right. Other clients might implement this entirely differently, for example with a simple like / dislike button. And not all algorithms have to take this data into account. We find it to be a useful tool though, so we decided to include it as part of the core protocoll.

This feedback is meant to be private, only in this way can we make sure it doen't get hacked or optimized against. But clients can offer to do additional things while measuring the resonance, for example post what you've read and really liked. For more on this see the "Use Case: Community Reader".

## Properties

```
RequiredLake: True
RequiredAlgo: True
RequiredClient: False

{
  "content": "number between 0-100"
  "extra": {
    "link": "
  }
  "type": "_resonance"
}
```

Clients CAN implement a collection

Algorithms CAN take this into account, when selecting experiences
Algorithms SHOULD include a property of "usesResonance: boolean" in there GET /info response

Lakes MUST allow the storage of this type
