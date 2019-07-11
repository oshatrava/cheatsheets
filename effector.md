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
{: .-prime}

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
const event = createEvent()

// data is an Event
const data = event
  .map((message) => message.data)

data.watch(console.log)

event({ data: "Hello world" }) // Hello world
```
{: data-line="5"}

Сreates a new event, which will be called after the original event is called, applying the result of a fn as a payload.

[Try in playground](https://share.effector.dev/aLDDZRtx)

### Filter event updates

```js
const number = createEvent()

const positiveNumber = number.filter({
  fn: (number) => number > 0,
})

positiveNumber.watch(console.log)

number(0)
number(2) // 2
number(-1)
```
{: data-line="3,4,5"}

Сreates a new event, which will be called after the original event is called, if `fn` returns true.

[Try in playground](https://share.effector.dev/eqhvLcrK)

### Filter event by undefined

```js
const formChanged = createEvent()

const userSelected = formChanged.filterMap(
  (form) => form.user,
)

userSelected.watch(console.log)

formChanged({ field: 1 })
formChanged({ field: 1, user: "name" }) // name
formChanged({ field: 1, user: null }) // null
```
{: data-line="3,4,5"}

Сreates a new event, which will be called after the original event is called, if `fn` returns **not undefined**.

[Try in playground](https://share.effector.dev/xtbXUvKz)

### Modify event arguments

```js
const sortEvent = createEvent()

const sortASC = sortEvent
  .prepend((field) => ({ field, dir: "ASC" }))

const sortDESC = sortEvent
  .prepend((field) => ({ field, dir: "DESC" }))

sortEvent.watch(console.log)

sortASC("firstName") // { field: "firstName", dir: "ASC" }
sortDESC("lastName") // { field: "lastName", dir: "DESC" }
```
{: data-line="3,4,6,7"}

Creates a new event which call original events with modified payload.

[Try in playground](https://share.effector.dev/QOtuWSAK)

Store
----------
{: .-three-column}

### Create and update store
{: .-prime}

```js
import {
  createEvent,
  createStore
} from 'effector'
```
{: .-setup}

```js
// initial value — 0
const $counter = createStore(0)
const increment = createEvent()

$counter.on(increment,
  (state) => state + 1)

$counter.watch(console.log) // 0

increment() // 1
increment() // 2
```
{: data-line="6,8"}

Store watcher called immediately after creation.
All watchers called after all stores is updated.

[Try in playground](https://share.effector.dev/UyF9kUf4)

### Handle just updates of store

```js
// initial value — 0
const $counter = createStore(0)
const increment = createEvent()

$counter.on(increment,
  (state) => state + 1)

$counter.updates.watch(console.log)

increment() // 1
increment() // 2
```
{: data-line="8"}

`updates` called only on store updates.

[Try in playground](https://share.effector.dev/7hbJQ73h)

### Reset store to initial value

```js
// initial value — 0
const $counter = createStore(0)

const increment = createEvent()
const reset = createEvent()

$counter
  .on(increment, (state) => state + 1)
  .reset(reset)

$counter.watch(console.log) // 0

increment() // 1
increment() // 2
reset() // 0
```
{: data-line="5,9"}

[Try in playground](https://share.effector.dev/PN2BBuad)

### Map one store to another

Derived store

```js
const $title = createStore('')
const changed = createEvent()

const $length = $title
  .map(title => title.length)

$title.on(changed, (_, title) => title)

$length.watch(console.log) // 0

changed("hello") // 5
changed("world")
changed("hello world") // 11
```
{: data-line="5"}

It will call a provided function with the state, when the original store updates, and will use the result to update the derived store

[Try in playground](https://share.effector.dev/EZZbKUW9)

{%endraw%}
