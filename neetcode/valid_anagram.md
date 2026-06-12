# Valid Anagram

Given two strings `s` and `t`, return `true` if the two strings are anagrams of each other, otherwise return `false`.

An anagram is a string that contains the exact same characters as another string, but the order of the characters can be different.

## Examples

**Example 1:**

> **Input:** `s = "racecar"`, `t = "carrace"`
>
> **Output:** `true`

**Example 2:**

> **Input:** `s = "jar"`, `t = "jam"`
>
> **Output:** `false`

## Constraints

- `1 <= s.length, t.length <= 5 * 10^4`
- `s` and `t` consist of lowercase English letters.

## Solution (with Maps) memory size 13mb

```typescript
class Solution {
  isAnagram(str1: string, str2: string): boolean {
    const anaMap = new Map();
    for (let i of str1.split("")) {
      if (!anaMap.has(i)) {
        anaMap.set(i, 1);
      } else {
        anaMap.set(i, anaMap.get(i) + 1);
      }
    }
    for (let i of str2) {
      if (!anaMap.has(i)) {
        return false;
      } else {
        anaMap.set(i, anaMap.get(i) - 1);
      }
      if (anaMap.get(i) === 0) {
        anaMap.delete(i);
      }
    }
    return anaMap.size === 0;
  }
}
```

### Explanation

1. **Map Creation**: Create a frequency map to count occurrences of each character in `str1`.
2. **Character Verification**: Iterate through `str2` and check each character against the map:
   - If a character is missing, return `false`.
   - Otherwise, decrement its count. If the count reaches `0`, remove the character from the map.
3. **Validation**: If `str1` and `str2` are of equal length and all characters match in frequency, the map size will be `0` at the end, returning `true`.

### Complexity

- **Time Complexity:** $O(n)$ where $n$ is the length of the strings.
- **Space Complexity:** $O(1)$ since the map size is bounded by the alphabet size (26 lowercase English letters).

## Solution (With Objects) memory size 11mb

```typescript
class Solution {
  isAnagram(str1: string, str2: string): boolean {
    if (str1.length !== str2.length) {
      return false;
    }
    const count: Record<string, number> = {};
    for (let i = 0; i < str1.length; i++) {
      count[str1[i]] = (count[str1[i]] || 0) + 1;
      count[str2[i]] = (count[str2[i]] || 0) - 1;
    }
    for (const key in count) {
      if (count[key] !== 0) {
        return false;
      }
    }
    return true;
  }
}
```

### Explanation

1. **Length Check**: If the lengths of `str1` and `str2` are different, they cannot be anagrams, so return `false` immediately.
2. **Frequency Counter**: Initialize a frequency counter object (`count`). Iterate through both strings simultaneously:
   - Increment the frequency for each character in `str1`.
   - Decrement the frequency for each character in `str2`.
3. **Validation**: Iterate through the keys in the `count` object. If the two strings are anagrams, the increments and decrements will cancel each other out, leaving all frequency values at `0`. If any character's count is not `0`, return `false`; otherwise, return `true`.

### Complexity

- **Time Complexity:** $O(n)$ where $n$ is the length of the strings.
- **Space Complexity:** $O(1)$ since the object size is bounded by the alphabet size (26 lowercase English letters).

