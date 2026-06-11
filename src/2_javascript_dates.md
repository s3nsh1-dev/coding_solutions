# HackerRank – Day 6: JavaScript Dates (10 Days of JavaScript)

---

## 📘 Question Explanation

### Task

Given a date string `dateString` in the format **MM/DD/YYYY**, find and return the **day name** for that date.

The day name must be one of:
`Sunday`, `Monday`, `Tuesday`, `Wednesday`, `Thursday`, `Friday`, `Saturday`

For example, the day name for `12/07/2016` is `Wednesday`.

---

### Input Format

- The first line contains an integer **d** — the number of dates to check.
- Each of the following **d** lines contains a date in `MM/DD/YYYY` format, passed as `dateString` to the function.

### Constraints

- It is guaranteed that the input only consists of **valid dates**.

### Output Format

Return a string denoting the **day of the week** corresponding to the date denoted by `dateString`.

---

### Sample Walkthrough

**Input:**

```
2
10/11/2009
11/10/2010
```

**Output:**

```
Sunday
Wednesday
```

**Explanation:**

- `10/11/2009` → was a **Sunday**
- `11/10/2010` → was a **Wednesday**

---

## ✅ My Submission

```javascript
"use strict";

// The days of the week are: "Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"
function getDayName(dateString) {
  const dayArr = [
    "Sunday",
    "Monday",
    "Tuesday",
    "Wednesday",
    "Thursday",
    "Friday",
    "Saturday",
  ];
  let dayName = dayArr[new Date(dateString).getDay()];
  return dayName;
}

function main() {
  const input = ["10/11/2009", "11/10/2010"];
  for (let i of input) {
    console.log(getDayName(i));
  }
}
```
