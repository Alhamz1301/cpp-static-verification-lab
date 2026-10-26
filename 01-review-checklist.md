# C++ Static Code Verification — Review Checklist

## Purpose
This checklist is used to inspect the C++ program for programming defects, unsafe memory operations, logical errors, and violations of standard C++ coding practices. The review is based on static inspection of the supplied source code without executing the program.

## Checklist Categories

| Category | Result (Issue / OK) | Defect |
|---|---|---|
| Initialization | Issue | `sum` in `averageAttack()` is declared but not initialized, and the `monsters` array elements are not explicitly initialized to `nullptr`. |
| Pointers | Issue | `attackMonster()` and `getMonsterLabel()` dereference null pointers when a requested monster is missing, `defeatMonster()` dereferences a pointer after deletion, and `getMonsterLabel()` returns a reference to a local variable. |
| Arrays / Buffers | Issue | `spawnMonster()` does not check capacity, `main()` creates six monsters when the maximum is five, `readBoss()` uses a fixed-size character buffer that can overflow, and `totalMonsterHealth()` reads beyond the valid range. |
| Loops | Issue | `totalMonsterHealth()` uses an incorrect upper bound, and the destructor loops over `monsterCount` assuming every element is valid and owned. |
| Arithmetic | Issue | `attackMonster()` converts negative damage to `unsigned int`, health comparisons mix signed and unsigned values, `averageAttack()` divides by zero when the count is zero, and `calculateDamage()` performs integer arithmetic before converting to `double`. |
| Control Flow | Issue | `findMonster()` uses assignment instead of comparison, `playerRank()` lacks a return path for some score values, and `attackMonster()` does not handle a missing monster before reading its health. |
| Functions | Issue | `getMonsterLabel()` returns a dangling reference, `playerRank()` has a missing return path, `readBoss()` uses unsafe input handling, and `calculateDamage()` has precision and arithmetic problems. |
| Classes | Issue | `Game` owns dynamically allocated `Monster` objects but does not define safe copy semantics, `defeatMonster()` does not remove the defeated object from the array or update the count, and the constructor does not initialize the pointer array. |

## Checklist Findings

### Initialization
- `sum` in `averageAttack()` is declared but not initialized.
- `monsters` array elements are not explicitly initialized to `nullptr`.

### Pointers
- `attackMonster()` dereferences a null pointer if the requested monster does not exist.
- `getMonsterLabel()` dereferences a null pointer if the requested monster does not exist.
- `defeatMonster()` dereferences a pointer after deleting the object.
- `getMonsterLabel()` returns a reference to a local variable.
- `readBoss()` uses `delete` instead of `delete[]` for dynamically allocated character storage.

### Arrays / Buffers
- `spawnMonster()` does not check whether the array has reached `MAX_MONSTERS`.
- `main()` attempts to create six monsters although `MAX_MONSTERS` is five.
- `readBoss()` uses a fixed-size character buffer that can overflow when reading an excessively long name.
- `totalMonsterHealth()` accesses `monsters[monsterCount]` because its loop condition uses `i <= monsterCount`.

### Loops
- `totalMonsterHealth()` uses an incorrect upper boundary.
- The destructor loops over `monsterCount`, which is appropriate only while the count accurately represents the number of valid owned pointers.

### Arithmetic
- `attackMonster()` converts potentially negative damage to `unsigned int`.
- The health comparison mixes signed and unsigned arithmetic.
- `averageAttack()` divides by zero if the monster count is zero.
- `calculateDamage()` uses integer arithmetic before returning a `double`, which may truncate the result.

### Control Flow
- `findMonster()` uses assignment (`=`) instead of comparison (`==`) in its condition.
- `playerRank()` does not return a value for scores of 100 or less.
- `attackMonster()` does not handle a missing monster before accessing its health.

### Functions
- `getMonsterLabel()` returns a dangling reference.
- `playerRank()` has a missing return path.
- `readBoss()` uses unsafe input handling.
- `calculateDamage()` has a potential precision and arithmetic issue.

### Classes
- `Game` owns dynamically allocated `Monster` objects but does not define safe copy semantics.
- `Game copy = game;` performs a shallow copy of the pointers, creating ownership and double-deletion risks.
- `defeatMonster()` does not remove the defeated monster from the array or update `monsterCount`.
- The `Game` constructor initializes `monsterCount` but not the pointer array.

## Static Verification Summary
Multiple categories contain defects, including unsafe pointer handling, invalid array access, missing capacity checks, uninitialized data, and ownership errors. The program requires correction before it can be considered safe, reliable, and maintainable.
