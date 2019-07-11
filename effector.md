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
----------

{: .-three-column}

### Create event
{: .-prime}


```js
import { createEvent } from 'effector'
```
{: .-setup}

```js
// Just event
const first = createEvent()

// Event with the name
const second = createEvent('event name')
```

### Subscribe to event updates

```js
import { createEvent } from 'effector'
```
{: .-setup}

```js
const event = createEvent()

event.watch((params) => {
  console.log('>>', params)
})

event([1, 2, 3]) // >> [1, 2, 3]
```
{: data-line="4"}

### Unsubscribe from event updates

```js
import { createEvent } from 'effector'
```
{: .-setup}

```js
const event = createEvent()

const unsubscribe = event.watch((params) => {
  console.log('>>', params)
})

event("hello") // >> hello

unsubscribe()

event("nothing")
```
{: data-line="3,9"}

[Try in playground](https://share.effector.dev/4QlZGHfF)

### Map arguments of event to another event

```js
import { createEvent } from 'effector'
```
{: .-setup}

```js
const event = createEvent()

// data is an Event
const data = event.map((message) => message.data)

data.watch(console.log)

event({ data: "Hello world" }) // Hello world
```
{: data-line="4"}

Сreates a new event, which will be called after the original event is called, applying the result of a fn as a payload.

[Try in playground](https://share.effector.dev/aLDDZRtx)

{%endraw%}
