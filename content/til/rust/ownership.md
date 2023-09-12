---
title: "Ownership  and Borrowing in Rust"
date: 2023-09-12T10:52:47+02:00
draft: false
tags: ["Rust"]
---

# Ownership and Borrowing in Rust

## Ownership

The Book[^1] states the following as the three rules of ownership in Rust:

1. Each value in Rust has an owner.
2. There can only be one owner at a time.
3. When the owner goes out of scope, the value will be dropped.

Going out of scope essentially means coming to the end of the trailing curly brace '}' of the one in which a value was introduced in.

```rust
{
    let s = "hi";
} // Goes out of scope here
```

To prevent double ownership, Rust introduces the concept of a `move` that invalidates ownership if it is referenced by another.
Moving a variable essentially makes a shallow copy of the data whilst invalidating the original.

A secondary way of preventing multiple ownership is to copy data:

* Clone Trait: deep and expensive copy of heap data
* Copy Trait: cheap copy of stack data, variables that use it do not move.

## Borrowing

A value in Rust is borrowed through referencing, a special type of pointer that can refer to the underlying data of a value without taking ownership.

Rust has mutable and immutable references to indicate if the underlying borrowed data can be mutated or not:

* If you have a mutable reference to a value you cannot have any other references to that value.
    * At least simultaneous ones. A nuance here is that a reference scope lasts from where it was introduced up until where the reference is last used, not necessarily the end of the function scope.
* You can have any number of simultaneous immutable references.

Slices are essentially references that let you refer to a range of data. Slices are essentially pointers storing and index and a length. 
Being a type of reference they too do not take ownership

Interesting aside: string literals ``` let s: &str = "hi"; ``` are slices of the binary, pointing to an index in the binary with an associated length.

[^1]: [The Book](https://doc.rust-lang.org/book/ch04-01-what-is-ownership.html)

