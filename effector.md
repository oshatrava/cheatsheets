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

const unsubscribe = event.watch((params) => {
  console.log('>>', params)
})

event("Hi!") // >> Hi!
```
{: data-line="4"}

Unsubscribe from event updates

```js
event("hello") // >> hello

unsubscribe()

event("nothing")
```
{: data-line="3"}

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

### Filter event updates

```js
import { createEvent } from 'effector'
```
{: .-setup}

```js
const numberReceived = createEvent()

const positiveNumberReceived = numberReceived.filter({
  fn: (number) => number > 0,
})

positiveNumberReceived.watch(console.log)

numberReceived(0)
numberReceived(2) // 2
numberReceived(-1)
```
{: data-line="3,4,5"}

Сreates a new event, which will be called after the original event is called, if `fn` returns true.

[Try in playground](https://share.effector.dev/eqhvLcrK)

### Filter event by undefined

```js
import { createEvent } from 'effector'
```
{: .-setup}

```js
const formChanged = createEvent()

const userSelected = formChanged.filterMap(
  (form) => form.user,
)

userSelected.watch((user) => console.log("user", user))

formChanged({ field: 1 })
formChanged({ field: 1, user: "name" }) // user name
formChanged({ field: 1, user: null }) // user null
```
{: data-line="3,4,5"}

Сreates a new event, which will be called after the original event is called, if `fn` returns **not undefined**.

[Try in playground](https://share.effector.dev/xtbXUvKz)

### Modify event arguments

```js
const sortEvent = createEvent()

const sortASC = sortEvent.prepend((field) => ({ field, dir: "ASC" }))
const sortDESC = sortEvent.prepend((field) => ({ field, dir: "DESC" }))

sortEvent.watch(console.log)

sortASC("firstName") // { field: "firstName", dir: "ASC" }
sortDESC("lastName") // { field: "lastName", dir: "DESC" }
```
{: data-line="3,4,5"}

Creates a new event which call original events with modified payload.

[Try in playground](https://share.effector.dev/QOtuWSAK)

{%endraw%}
