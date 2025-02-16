---
layout: post
title: "Pyramid of Doom"
date: 2024-11-24 12:10:55
description: Understanding the Pyramid of Doom and How to Avoid It.
tags: [javascript, code, patterns]
---

## Understanding the Pyramid of Doom and How to Avoid It

The "Pyramid of Doom" is a term used to describe deeply nested and hard-to-read code, particularly in JavaScript. While this pattern is less common today due to modern improvements in handling asynchronous operations, it’s still useful to understand the issue and how to refactor it effectively. If you've worked with callback-heavy JavaScript, you may have encountered this problem, which is similar to the excessive nesting often seen in poorly structured HTML (sometimes called "div soup").

This post revisits the concept of the Pyramid of Doom, originally covered in my book _Survive JavaScript - a Web Developer’s Guide_, which I wrote a decade ago. Although the book is outdated, some core ideas remain relevant today.

## What is the Pyramid of Doom?

The Pyramid of Doom arises from excessive callback nesting. This was especially common in early Node.js development when asynchronous operations relied heavily on callbacks, with each function handling an error-first parameter convention.

### Example of the Pyramid of Doom

```javascript
import db from "./db";

db.set("key1", "value1", (err) => {
  if (err) throw err;

  db.set("key2", "value2", (err) => {
    if (err) throw err;

    db.set("key3", "value3", (err) => {
      if (err) throw err;

      db.get("key1", (err, value) => {
        if (err) throw err;

        console.log(value + "bar");
      });
    });
  });
});
```

The deeply nested structure makes the code difficult to read and maintain. Thankfully, modern JavaScript provides better ways to handle asynchronous execution.

## Solution 1: Using Promises

The introduction of Promises allowed developers to replace deeply nested callbacks with a more manageable structure. Promises provide a `.then()` method to chain operations and a `.catch()` method for handling errors.

### Refactored Example with Promises

```javascript
import db from "./db";

db.set("key1", "value1")
  .then(() => db.set("key2", "value2"))
  .then(() => db.set("key3", "value3"))
  .then(() => db.get("key1"))
  .then((value) => console.log(value + "bar"))
  .catch((err) => console.error(err));
```

This refactored version significantly reduces nesting, improving readability and maintainability.

## Solution 2: Using async/await

Async/await further simplifies asynchronous code, making it look more like synchronous code while still being non-blocking. This syntax is built on top of Promises but eliminates chaining.

### Refactored Example with async/await

```javascript
import db from "./db";

async function main() {
  try {
    await db.set("key1", "value1");
    await db.set("key2", "value2");
    await db.set("key3", "value3");

    const value = await db.get("key1");
    console.log(value + "bar");
  } catch (err) {
    console.error(err);
  }
}

main();
```

This structure makes the control flow much easier to follow while handling errors using `try/catch`.

## Solution 3: Parallel Execution with Promise.all

One limitation of the previous solutions is that they execute each operation sequentially, potentially slowing down execution. If the operations do not depend on each other, they can be executed in parallel using `Promise.all`.

### Example with Promise.all

```javascript
import db from "./db";

async function main() {
  try {
    await Promise.all([
      db.set("key1", "value1"),
      db.set("key2", "value2"),
      db.set("key3", "value3"),
    ]);

    const value = await db.get("key1");
    console.log(value + "bar");
  } catch (err) {
    console.error(err);
  }
}

main();
```

This approach speeds up execution but introduces a tradeoff—if any promise fails, `Promise.all` will reject immediately, potentially leaving the system in an inconsistent state. In scenarios where partial failures must be handled gracefully, `Promise.allSettled` may be a better option.

## Handling Errors in Asynchronous Code

One of the most common mistakes when using async/await is neglecting proper error handling. Since `await` is just syntactic sugar over Promises, you can handle errors using:

- `.catch()` for Promise chains.
- `try/catch` for async functions.
- `Promise.allSettled` when handling multiple async operations with independent error handling needs.

## Conclusion

The Pyramid of Doom, once a prevalent issue in JavaScript development, has largely been mitigated by modern features like Promises and async/await. Understanding these techniques will not only improve your code readability but also help you write more efficient and maintainable applications.

While Promises and async/await cover most use cases, other models like reactive programming (e.g., RxJS) offer alternative solutions for handling complex asynchronous workflows. The key takeaway is to avoid unnecessary nesting, structure your code logically, and use the right tools for the job.
