---
title: Effector
category: JavaScript
layout: 2017/sheet
ads: false
tags: [Featured]
updated: 2019-07-11
weight: 0
keywords:
  - createStore
  - createEvent
  - createEffect
  - sample
  - combine
  - createStoreObject
  - merge
  - getState
intro: |
  [Effector](https://effector.now.sh/) is a fast and powerful framework agnostic state manager.
---

{%raw%}

Event
---------
{: .-three-column}

### Create event

{: .-prime}

```js
import { createEvent } from "effector"
```

{: .-setup}

```js
// Just event
const first = createEvent()

// Event with the name
const second = createEvent("event name")
```

### Watch event

{: .-prime}

```js
import { createEvent } from "effector"
```

{: .-setup}

```js
const event = createEvent()

event.watch((params) => {
  console.log(">>", params)
})

event([1, 2, 3]) // >> [1, 2, 3]
```

{: data-line="4"}

