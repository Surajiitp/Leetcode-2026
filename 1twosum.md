# 1. Two Sum

**Difficulty:** Easy  
**Topic:** Array, Hash Table

## Problem Statement

Given an array of integers `nums` and an integer `target`, return the **indices** of the two numbers such that they add up to `target`.

You may assume that each input has **exactly one solution**, and you may not use the same element twice.

Return the answer in any order.

### Example

**Input:**
```text
nums = [2,7,11,15], target = 9
```

**Output:**
```text
[0,1]
```

**Explanation:**
- `nums[0] + nums[1] = 2 + 7 = 9`

---

## Approach 1: Brute Force

### Idea
- Check every possible pair of elements.
- If the sum equals the target, return their indices.

### Algorithm
1. Iterate through each element.
2. For every element, check all remaining elements.
3. If their sum equals the target, return the indices.

### Complexity Analysis

- **Time Complexity:** `O(N²)`
- **Space Complexity:** `O(1)`

### C++ Solution

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        int n = nums.size();

        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                if (nums[i] + nums[j] == target)
                    return {i, j};
            }
        }

        return {};
    }
};
```

---

## Approach 2: Hash Map (Optimal)

### Idea
- Store each number along with its index in a hash map.
- For every number, calculate its complement:
  ```
  complement = target - nums[i]
  ```
- If the complement already exists in the map, we've found the answer.

### Algorithm
1. Create an unordered map.
2. Traverse the array.
3. Compute the complement.
4. If the complement exists in the map, return both indices.
5. Otherwise, store the current element and its index.

### Complexity Analysis

- **Time Complexity:** `O(N)`
- **Space Complexity:** `O(N)`

### C++ Solution

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> mp;

        for (int i = 0; i < nums.size(); i++) {
            int complement = target - nums[i];

            if (mp.count(complement))
                return {mp[complement], i};

            mp[nums[i]] = i;
        }

        return {};
    }
};
```

---

## Comparison

| Approach | Time | Space |
|----------|------|-------|
| Brute Force | `O(N²)` | `O(1)` |
| Hash Map | `O(N)` | `O(N)` |

---

## Key Takeaways

- The brute force solution checks every possible pair and is easy to understand.
- The hash map approach stores previously seen numbers for constant-time lookups.
- Using an unordered map reduces the overall complexity from **O(N²)** to **O(N)**, making it the preferred solution for interviews and competitive programming.
