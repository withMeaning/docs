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

The Meaning Protocol defines only one datatype: the Experience. They look like this:

```
{
    "id": "312312nfje1",
    "author": "The Meaning Team",
    "content": "Hello!",
    "extra": {
      "source": "Tutorial",
      "body": "# This is the beginning of your journey with Meaning!"
    }
    "type": "experience",
    "created_at": 1679940469
}
```

This is essentially a fork from the [Event in Nostr](https://nostr.com/the-protocol/events). We changed some of the names to avoid confusion, as the Experience is less strict
in enforcing field values. The author for example can be a nostr pubkey, but it can also be a human readable name, let's say if the source was a blog post, or even a Twitter handle.

The main difference is the introduction of types, a set of instructions like "read, [do]({{< ref "/docs/contribute/types/do" >}} "Do"), watch, answer, etc." that expand the capabilities of the nostrs `Kind`.
There are two main classes of types: exposed and internal. Exposed types MUST be assumed to be seen by people. Internal experiences give extra information or relate experiences to each other and start with a `_` like [_extract]({{< ref "/docs/contribute/types/extract" >}} "Extract")

### id

This is either a generated uuid, or any unique identifier that comes with an integration, such as nostr uid or a tweet id. It can also be a 32-bytes lowercase hex-encoded sha256 of the serialized event data, see [NIP-01](https://github.com/nostr-protocol/nips/blob/master/01.md). All that matters is, that it is unique.

Lakes MUST check for uniqueness. The combination of LakeID and id MUST resolve to a single experience.

### author

The author is just a name of whoever created the experience. This can be a unique identifier, like a nostr or Meaning pubkey, but does not have to be.

Lakes SHOULD store the human readable name in a linked database, so that `source + author` always resolves to a name, as they
MUST pass a readable value to algorthims. They SHOULD store the identifier as an author field though, for cases in which people change their usernames.

Reserved names are: \
`me` for private notes (from note taking tools, Saved Messages or similar)\
`none` if the author is unknown, and only then.

Lakes SHOULD try to always fill this field, and avoid using `none` often.

Clients COULD hide the author if it's a private experience (author: me).

TODO: how should algorithms handle username changes?

### content

The main payload of the Experience, an arbitrary string. Different types force different values here, for example [read]()

Lakes should keep this short


## Properties
```
RequiredLake: True
RequiredAlgo: True
RequiredClient: False
NostrKind: 1

{
    "id": "uuid or hash of message",
    "author": "name of creator (name, username, twitter handle, nostr pubkey)",
    "content": "text for most types, title for articles, number if type resonance",
    "extra": {
      "source?": "where the content comes from, required if content comes from an integration",
      "main_content?": "Markdown of the main content",
      "link?": "url to external website, or id of event if type _*",
      "summary?": "AI or human generated summary of content",
      ...
    }
    "type": "experience",
    "created_at": 1679940469
}
```