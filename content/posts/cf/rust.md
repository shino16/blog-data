---
title: Introduction to Rust
draft: true
---

// Hey this is my first post

I've been using Rust for competitive programming and getting some OK performances, so here's an introduction to Rust. This article mainly focuses on the difference from C++ and pros & cons in competitive programming.

## Overview

Rust is **as fast as C++** (or **faster**), **safe** and **expressive**. You probably enjoy it if you like a very clever and kind compiler or have interests in a beautiful library design. However, Rust is a 'good' system programming language and sometimes restricts potentially dangerous or unnecessarily complicated (but useful in CP) coding patterns.

Rust has been loved since its release in 2015 and it is the most popular programming language on StackOverflow for n years in a row.

## pros

### 1. Fast

Rust supports "zero-cost abstraction". While you can code in the similiar way you write C++, you can also choose more functional-programming style and achieve the same speed.

Its mechanics for speed is much the same as C++, so there's few to say.

### 2. Safe

Rust guarantees that there will never ever cause undefined behavior.

Taking dangling reference as an example, consider the following code snippets:

```cpp
std::vector<int> v = {42};
v.push_back(v[0]);
```

```cpp
std::pair p = std::minmax(1 + 4, 2 * 3);
printf("(min, max) = (%d, %d)", p.first, p.second);
```

The actual value `42` may have been moved when the memory is reallocated. `1+4` and `2*3` will be already destructed when we want their values. These are causing undefined behavior.

The Rust compiler check all references and guarantees that no invalid references exist using a unique **type system**, so these programs will not compile and there is no runtime overhead too.

Another example is error handling. Since Rust does not have exceptions, operations that can fail forces you to explicitly handle the errors or abort.

Let's say you want to `pop` from a `BinaryHeap` (akin to `std::priority_queue`). In Rust, you may have to write this:

```rust
let value = heap.pop().unwrap();
```

Because `pop` returns `Option<T>` (equivalent to `std::optional<T>`), you have to explicit the error (`unwrap` aborts the execution in that case). But they are not that bothersome. Control flow can nicely absorb error handling:

```rust
if let Some(value) = heap.pop() {
    println!("{} is popped out", value);
} else {
    println!("empty");
}
```

```rust
while let Some(value) = heap.pop() {
    println!("{} is popped out", value);
}
```

Also it's loaded with various combinators imported from functional languages — `map`, `and_then`, etc.

<!-- Actually under a certain setting you can do:

```rust
let value = vec.pop()?;
```

`?` operators propagate the error to the caller of the function. So you can write something like `obj.foo()?.bar()?.baz()?` but outside `main`. -->

Rust also catches integer overflow/underflow in debug mode and performs bound checking in array access (in many case it's marginal, see [StackOverflow](https://stackoverflow.com/questions/47542438/does-rusts-array-bounds-checking-affect-performance)).

Maybe you sometimes want to bypass some safety checks. In this case you can declare part of the code as `unsafe`. Under `unsafe` you can skip bound checks, cast a value to pretty arbitrary types, etc. which can lead to undefined behavior. It can be used almost anytime and anywhere, Rust just requires programmers to be explicit.

Another thing to note is that its standard library is made intentionally small, so Rust programms in the real world rely on numerous crates (external libraries). AtCoder has a nice set of de facto standard libraries, but Codeforces doesn't.
