# Rust Ownership Explained

<img src="https://img.shields.io/badge/Rust-ownership-blue?style=for-the-badge&logo=rust&logoColor=white" alt="Rust Ownership">

A clear, example-driven guide to **Rust's ownership system** — one of the language's most powerful (and initially challenging) features.

Rust achieves memory safety **without** a garbage collector through its ownership rules, enforced at compile time. This repo contains:

- Plain-English explanations
- Step-by-step code examples (with comments)
- Common pitfalls & how the compiler protects you
- Visual analogies (stack vs heap, moving vs copying)
- Small exercises to practice ownership concepts

## Why Ownership Matters

Rust takes a radically different approach to memory management:

| Approach              | Language examples       | Runtime cost | Safety guarantees          | Manual management |
|-----------------------|--------------------------|--------------|-----------------------------|-------------------|
| Garbage Collection    | Java, Go, Python         | Yes          | Yes                         | No                |
| Manual (malloc/free)  | C, C++                   | No           | No (use-after-free, leaks…) | Yes               |
| **Ownership**         | **Rust**                 | **No**       | **Yes** (at compile time)   | **No**            |

Ownership gives Rust **C-like performance** with **modern-language safety**.

## Table of Contents

- [What is Ownership?](#what-is-ownership)
- [The Three Rules](#the-three-rules)
- [Stack vs Heap](#stack-vs-heap)
- [Move Semantics](#move-semantics)
- [Clone and Copy](#clone-and-copy)
- [Ownership in Functions](#ownership-in-functions)
- [Returning Values & Ownership](#returning-values--ownership)
- [Common Patterns & Idioms](#common-patterns--idioms)
- [Exercises](#exercises)
- [Further Reading](#further-reading)

## What is Ownership?

Ownership is a set of rules that govern how a Rust program manages memory. All programs must manage memory somehow. Some languages use garbage collection; others require manual allocation and freeing. Rust uses a **third approach**: memory is managed through a system of **ownership** with rules that the compiler checks at compile time.

> If any rule is violated → program doesn't compile.  
> No runtime overhead — zero-cost abstractions.

## The Three Rules

Rust’s ownership system is built on three core rules:

1. **Each value has a single owner** (a variable).
2. **There can only be one owner at a time**.
3. **When the owner goes out of scope, the value is dropped** (memory is automatically freed).

These simple rules prevent:

- dangling pointers
- double frees
- data races (in safe Rust)
- use-after-free bugs

## Stack vs Heap

Understanding the difference between stack and heap is key to grokking ownership.

- **Stack**: fast, fixed-size, LIFO, automatically managed (scope-based)
- **Heap**: dynamic size, slower allocation, manually managed in most languages
