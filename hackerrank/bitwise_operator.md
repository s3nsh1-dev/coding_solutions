# HackerRank – Day 6: Bitwise Operators (10 Days of JavaScript)

---

## 📘 Question Explanation

### Objective

Practice bitwise operations, specifically the **bitwise AND (`&`)** operator.

### Problem Statement

We define **S** as a sequence of distinct sequential integers from 1 to **n**:

> S = {1, 2, 3, …, n}

Find the **maximum** bitwise AND value of any two integers **a** and **b** (where `a < b`) from the sequence **S**, such that the result is **strictly less than** a given integer **k**.

In other words, find:

> **max(a & b)** such that `a < b`, both in S, and `(a & b) < k`

If no such pair exists, return `0`.

---

### Input Format

- The first line contains an integer **q** — the number of function calls (test cases).
- Each of the following **q** lines contains two space-separated integers: **n** and **k**.

### Constraints

- 1 ≤ q ≤ 10³
- 2 ≤ n ≤ 10³
- 2 ≤ k ≤ n

### Output Format

For each pair (n, k), print the maximum possible value of `a & b` where `a < b < k`.

---

### Sample Walkthrough

**Input:**

```
3
5 2
8 5
2 2
```

**Output:**

```
1
4
0
```

| n   | k   | Explanation                                                |
| --- | --- | ---------------------------------------------------------- |
| 5   | 2   | Pairs with AND < 2: `1&3=1`, `1&5=1`, etc. Max = **1**     |
| 8   | 5   | Pairs with AND < 5: `4&5=4`, `4&6=4`, `4&7=4`. Max = **4** |
| 2   | 2   | Only pair is `1&2=0`. No result ≥ 1 and < 2. Max = **0**   |

---

## ✅ My Submission

```javascript
"use strict";

function getMaxLessThanK(n, k) {
  let max = 0;
  for (let i = 1; i <= n; i++) {
    for (let j = i + 1; j <= n; j++) {
      const temp = i & j;
      if (temp < k && max < temp) {
        max = temp;
      }
    }
  }
  return max;
}

function main() {
  const q = 3;

  const arr = [
    [5, 2],
    [8, 5],
    [2, 2],
  ];

  for (let i of arr) {
    const n = i[0];
    const k = i[1];
    console.log(getMaxLessThanK(n, k));
  }
}
```

---

## 🧠 How It Works

1. **Initialize** `max = 0` — the default result if no valid pair is found.
2. **Double loop** — iterate over all pairs `(i, j)` from sequence S where `i < j ≤ n`.
3. **Compute** `temp = i & j` (bitwise AND of the two numbers).
4. **Check conditions**:
   - `temp < k` — the AND result must be less than k.
   - `max < temp` — it must beat the current maximum.
5. **Update** `max` if both conditions are satisfied.
6. **Return** `max` after all pairs are checked.

---

## 💡 Key Concept: Bitwise AND

The `&` operator compares two numbers **bit by bit**. A result bit is `1` only when **both** corresponding bits are `1`.

```
4 & 5 → 100 & 101 = 100 → 4
1 & 3 → 001 & 011 = 001 → 1
2 & 3 → 010 & 011 = 010 → 2
```

This is why AND results are always **≤ the smaller of the two numbers** — you can only turn bits off, never on.
