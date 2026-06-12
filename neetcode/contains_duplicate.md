# Contains Duplicate

Given an integer array `nums`, return `true` if any value appears more than once in the array, otherwise return `false`.

## Examples

**Example 1:**

> **Input:** `nums = [1, 2, 3, 3]`
>
> **Output:** `true`

**Example 2:**

> **Input:** `nums = [1, 2, 3, 4]`
>
> **Output:** `false`

## Constraints

- `0 <= nums.length <= 10^5`
- `-10^9 <= nums[i] <= 10^9`

## Solution

```typescript
class Solution {
  hasDuplicate(nums: number[]) {
    const s = new Set(nums);
    return s.size !== nums.length;
  }
}

const obj1 = new Solution();
console.log(obj1.hasDuplicate([1, 2, 3, 3, 5, 6]));
console.log(obj1.hasDuplicate([-2, -1, 0, 1, 2, -1]));
console.log(obj1.hasDuplicate([-2, -1, 0, 1, 2]));
```

### Complexity

- **Time Complexity:** $O(n)$
- **Space Complexity:** $O(n)$

