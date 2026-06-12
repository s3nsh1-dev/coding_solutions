# Group Anagrams

Given an array of strings `strs`, group all anagrams together into sublists. You may return the output in any order.

An anagram is a string that contains the exact same characters as another string, but the order of the characters can be different.

## Examples

**Example 1:**

> **Input:** `strs = ["act","pots","tops","cat","stop","hat"]`
>
> **Output:** `[["hat"],["act", "cat"],["stop", "pots", "tops"]]`

**Example 2:**

> **Input:** `strs = ["x"]`
>
> **Output:** `[["x"]]`

**Example 3:**

> **Input:** `strs = [""]`
>
> **Output:** `[[""]]`

## Constraints

- `1 <= strs.length <= 1000`
- `0 <= strs[i].length <= 100`
- `strs[i]` is made up of lowercase English letters.

## Solution (Sorting)

```typescript
class Solution {
  groupAnagrams(strs: string[]): string[][] {
    const map = new Map<string, string[]>();
    for (const str of strs) {
      const sortedStr = str.split("").sort().join("");
      if (!map.has(sortedStr)) {
        map.set(sortedStr, []);
      }
      map.get(sortedStr)!.push(str);
    }
    return Array.from(map.values());
  }
}

const obj = new Solution();
console.log(obj.groupAnagrams(["act", "pots", "tops", "cat", "stop", "hat"]));
// Output: [["act", "cat"], ["pots", "tops", "stop"], ["hat"]]
```

### Explanation

1. **Sort as Key**: Since anagrams contain the same characters, sorting their characters will yield the exact same string (e.g., `"act"` and `"cat"` both sort to `"act"`).
2. **Hash Map Grouping**: Use a hash map where the keys are the sorted strings, and the values are lists of the original strings.
3. **Collate Results**: Return all the values from the map as a list of sublists.

### Complexity

- **Time Complexity:** $O(N \cdot L \log L)$ where $N$ is the number of strings in `strs` and $L$ is the maximum length of a string. Sorting each string takes $O(L \log L)$ time.
- **Space Complexity:** $O(N \cdot L)$ to store the grouped strings in the map.

## Solution (Frequency Count)

```typescript
class Solution {
  groupAnagrams(strs: string[]): string[][] {
    const map = new Map<string, string[]>();
    for (const str of strs) {
      const count = new Array(26).fill(0);
      for (let i = 0; i < str.length; i++) {
        count[str.charCodeAt(i) - 97]++;
      }
      const key = count.join(",");
      if (!map.has(key)) {
        map.set(key, []);
      }
      map.get(key)!.push(str);
    }
    return Array.from(map.values());
  }
}

const obj = new Solution();
console.log(obj.groupAnagrams(["act", "pots", "tops", "cat", "stop", "hat"]));
// Output: [["act", "cat"], ["pots", "tops", "stop"], ["hat"]]
```

### Explanation

1. **Frequency Array Key**: Instead of sorting, we count the frequency of each character ($a$ to $z$) for each string using an array of size 26.
2. **Hash Map Grouping**: Convert the frequency array into a string (e.g., `"1,0,1,0,..."`) to use as the unique hash map key.
3. **Collate Results**: Group strings under their respective frequency string key and return the map values.

### Complexity

- **Time Complexity:** $O(N \cdot L)$ where $N$ is the number of strings and $L$ is the maximum length of a string. Counting frequencies takes $O(L)$ per string, avoiding the sorting overhead.
- **Space Complexity:** $O(N \cdot L)$ to store the mapped values. The keys themselves have a constant size of 26 integers.

## Note on Duplicates

There is no need to worry about removing duplicates from the input arrays when grouping anagrams, as duplicates within the input should be kept and grouped together into their respective anagram slots.

