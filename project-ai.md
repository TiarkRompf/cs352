---
title: "Bonus Project: AI-Assisted Compiler Extension"
usetable: true
layout: template
---

> Up to 10% extra credit toward your overall course grade.
>
> Due 11:59pm Sunday Apr 26.

## Overview

Pick any advanced compiler topic not covered in Projects 1–6 and extend the course compiler to demonstrate it. You are expected to use an AI coding assistant throughout. The goal is to build something real, reflect honestly on the experience, and develop a nuanced understanding of what AI tools can and cannot do for compiler engineering.

## Topic

You have full freedom in choosing a topic. Some starting points:

- Topics covered in lecture but not in any project (e.g., register allocation, instruction scheduling, tail-call optimization)
- Language features not in MiniScala (e.g., floating-point numbers, classes and objects, generic types)
- A backend targeting a different platform (e.g., LLVM IR, WebAssembly)
- Anything else from the compiler/PL literature that interests you

If you are unsure whether a topic is in scope, ask on Piazza.

## AI Tools

You are expected to use an AI coding assistant. [GitHub Copilot](https://github.com/features/copilot) is available free to students via the [GitHub Student Developer Pack](https://education.github.com/pack). Claude and ChatGPT are also suitable.

## Submission

Submit a ZIP file containing four parts.

### 1. Solution Description

A short document (one page max) covering:

- What you implemented and what it adds to the compiler
- How to run the code
- What the 10 test programs exercise and how output should be interpreted
- Your AI setup: tool(s), model(s), IDE, etc.
- Any known limitations

### 2. Code

Your extension to the compiler. If your project requires anything beyond the standard course setup, include detailed installation instructions.

### 3. Transcript

Export of your AI session(s), best effort. Not all tools support this easily; include what you can.

### 4. Reflection

Answer the following three questions concisely; a focused paragraph each is enough.

**Q1.** Across different tasks (understanding, design, coding, debugging), where did AI help and where did it fall short? What pattern do you notice?

**Q2.** How did you verify correctness — what did you test, what did you look at beyond pass/fail, and how did you try to break your own implementation?

**Q3.** Describe a moment when AI was heading in a wrong direction across multiple turns. How did you detect it and steer it back — or did you give up and work independently?

## Grading

Grading is holistic; we are looking for:

- A nontrivial compiler extension with good test coverage
- Genuine and honest engagement with AI tools throughout
- Insight in the reflection — concrete examples, not generalities

Everyone who makes a serious attempt will receive meaningful credit. Higher scores reflect work that is technically strong and shows genuine insight into working with coding agents.
