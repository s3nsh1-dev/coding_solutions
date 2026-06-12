# Two Sum

Given an array of integers `nums` and an integer `target`, return the indices `i` and `j` such that `nums[i] + nums[j] == target` and `i != j`.

You may assume that every input has exactly one pair of indices `i` and `j` that satisfy the condition.

Return the answer with the smaller index first.

## Examples

**Example 1:**

> **Input:** `nums = [3, 4, 5, 6]`, `target = 7`
>
> **Output:** `[0, 1]`
>
> **Explanation:** `nums[0] + nums[1] == 7`, so we return `[0, 1]`.

**Example 2:**

> **Input:** `nums = [4, 5, 6]`, `target = 10`
>
> **Output:** `[0, 2]`

**Example 3:**

> **Input:** `nums = [5, 5]`, `target = 10`
>
> **Output:** `[0, 1]`

## Constraints

- `2 <= nums.length <= 1000`
- `-10,000,000 <= nums[i] <= 10,000,000`
- `-10,000,000 <= target <= 10,000,000`
- Only one valid answer exists.

## Solution (with Maps) memory size 10.1mb

```typescript
class Solution {
  twoSum(nums: number[], target: number) {
    const tsMap: Map<number, number> = new Map();
    for (let i = 0; i < nums.length; i++) {
      const difference = target - nums[i]!;
      if (tsMap.has(difference)) {
        return [tsMap.get(difference), i];
      }
      tsMap.set(nums[i]!, i);
    }
    return [];
  }
}

const obj = new Solution();
console.log(obj.twoSum([3, 4, 5, 6], 7)); // [0, 1]
console.log(obj.twoSum([4, 5, 6], 10)); // [0, 2]
console.log(obj.twoSum([5, 5], 10)); // [0, 1]
```

### Explanation

1. **Hash Map Creation**: Create a `map` to store the numbers we have seen so far as keys and their corresponding indices as values.
2. **One-Pass Iteration**: Iterate through the `nums` array. For each number:
   - Calculate the `complement` (`target - nums[i]`).
   - Check if the `complement` is already in the map. If it is, return its stored index along with the current index `i`.
   - If not, add the current number and its index to the map.
3. **Return**: The loop is guaranteed to find a solution and return early based on the problem constraints. An empty array is returned as a fallback.

### Complexity

- **Time Complexity:** $O(n)$ where $n$ is the number of elements in the `nums` array.
- **Space Complexity:** $O(n)$ to store elements in the hash map.

## Solution (Brute Force) memory size 10.4mb

```typescript
class Solution {
  twoSum(nums: number[], target: number): number[] | undefined {
    for (let i = 0; i < nums.length; i++) {
      const temp = target - nums[i]!;
      for (let j = i; j < nums.length; j++) {
        if (temp === nums[j] && i !== j) {
          return [i, j];
        }
      }
    }
  }
}

const obj = new Solution();
console.log(obj.twoSum([3, 4, 5, 6], 7)); // [0, 1]
```

### Explanation

1. **Outer Loop**: Loop through each element in the `nums` array.
2. **Complement Check**: For each element, calculate the required target complement (`target - nums[i]`).
3. **Inner Loop**: Iterate through the remaining part of the array to find if this complement value exists.
4. **Validation**: If found (and the indices are distinct), return the pair of indices.

### Complexity

- **Time Complexity:** $O(n^2)$ due to the nested loops checking all pairs of elements.
- **Space Complexity:** $O(1)$ as no extra memory structure is allocated.
