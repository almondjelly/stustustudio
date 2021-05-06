
---
title: Javascript
---

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

# What does `...` mean in Javascript?
**How do I pronounce this? Do I just say "dot dot dot"?**
This is called [spread syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax).

### What does it do?
It expands an iterable into its individual elements.

### Why do people use it?
It's an easy, concise, and readable way to make shallow copies of Javascript objects. This creates a totally new and separate object that contains the same elements. Making changes to one object does not affect the other object.
  
### How tho?
```javascript
let cats = ['Roger', 'Andrew', 'Jazzy', 'Meimei']
let copyCats = [...cats]

console.log(copyCats)
// expected output: ['Roger', 'Andrew', 'Jazzy', 'Meimei']
```

If we'd made a copy via `let copyCats = cats`, then making changes in `cats` would affect `copyCats` since `copyCats` would've been assigned a reference to `cats` rather than a new object.
