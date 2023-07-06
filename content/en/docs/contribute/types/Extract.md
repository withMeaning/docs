---
title: "_Extract"
description: "Internal Type for creating editable highlights"
lead: ""
date: 2020-10-06T08:49:31+00:00
lastmod: 2020-10-06T08:49:31+00:00
draft: false
images: []
menu:
  docs:
    parent: "types"
weight: 575
toc: true
---

## Editable Highlights

Extracts are one of the most powerful features of with Meaning. They allow you to interact only with the most important parts of anything.

At the core, an extract is just a highlight, a note that says: I have another experience saved for this word, sentence, paragraph. The power comes from the fact that an extract does NOT save the exact words, it is just a pointer. This means that you can link to anything, including any type.

Let's say you are getting this message from someone:

> One thing that could work is adding a 'Join the waitlist' button on our documentation and when people click on it, they'll be redirected to an Airtable form. Saw a couple of web-based apps doing that.

Now let's create two extracts:

> One thing that could work is adding a {{< highlighter color="#b1a32794" >}}'Join the waitlist' button{{</ highlighter >}} on our documentation and when people click on it, they'll be redirected to an {{< highlighter color="#b1a32794" >}}Airtable form{{</ highlighter >}}. Saw a couple of web-based apps doing that.


What our front-end should now have done is create **4** experiences, 2 of type `_extract`, linking our highlights to the original message, and 2 new experiences. It should look like this:

```
{
  "id": "1234"
  "author": "Original Message Author"
  "content": "'Join the waitlist' button"
  "created_at": 1679940469
  "type": "experience"
}
and
{
  "id": "5678"
  "author": "me"
  "content": "message_id:content:39:63"
  "extra": {
    "link": "1234"
  }
  "created_at": 1679940469
  "type": "_extract"
}
```

But now we can edit them, for example turn them into a to-do, or in this case even a GitHub issue:

```
{
  ...
  content: "Add a 'Join the waitlist' button to the docs"
  extra: {
    source: "GitHub, Repo: docs.withmeaning"
  }
  ...
  type: "resolve, do"
}
```
One of the main usecases is to extract action items from email, messages, etc. But it can also be used to create a read later list (extract a link and it will just get added to your Stream!) or to create flashcards, which turns with Meaning into an excellent [incremental reader](https://en.wikipedia.org/wiki/Incremental_reading). Note that this can all be done automatically by AI too!

## Properties

```
RequiredLake: True
RequiredAlgo: True
RequiredClient: False

content: "A colon joined string that uniquely identifies the highlights position like original_experience_id:content_or_body:char_position:char_position_end"
extra: {
  "link": "The id of the newly created extracted experience id"
}
```

Clients SHOULD implement an easy way to turn any selected text into an extract, and register

Algorithms CAN take the structure of extracts into account, for example only showing the action items of a mail, instead of the original mail.

Lakes MUST allow the storage of extracts, they SHOULD also handle edits of the original message and update any linked extract adresses.

Clients, Algorithms and Lakes can all create automated extracts.
