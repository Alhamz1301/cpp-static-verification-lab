# C++ Static Verification and Code Review Lab

## Project Purpose
This repository documents a static verification review of the C++ program `game.cpp`, which implements a small text-based monster battle game.

The objective is to inspect the supplied source code without executing it, identify defects, explain the likely consequences, and recommend safer fixes. This lab focuses on reviewing the code for memory safety issues, logic faults, and violations of good C++ practices.

## Monster Battle Game Overview
The game creates and manages a collection of monsters, tracks their health and attack values, and allows the player to fight monsters, calculate rankings, and assess damage. The review is based on inspecting the code as written rather than modifying the original program.

## Static Code Verification
Static verification is the review of source code to find defects before runtime. It is used to detect issues such as null-pointer misuse, array bounds errors, unsafe memory management, uninitialized values, and incorrect control flow.

## Included Review Files
- [README.md](README.md)
- [game.cpp](game.cpp)
- [01-review-checklist.md](01-review-checklist.md)
- [02-code-review-report.md](02-code-review-report.md)

## Review Categories
The checklist reviews the following eight categories:
1. Initialization
2. Pointers
3. Arrays / Buffers
4. Loops
5. Arithmetic
6. Control Flow
7. Functions
8. Classes

## How to Review the Reports
1. Read the checklist to understand the key categories and defects.
2. Review the detailed line-by-line findings in the code review report.
3. Compare the reported defects against the exact source in `game.cpp`.
4. Use the proposed fixes as guidance for a safer and more correct implementation.

## Important Note
These documents describe defects and recommended repairs. They do not change the original source program automatically. Any code repair should be performed intentionally and validated separately.
