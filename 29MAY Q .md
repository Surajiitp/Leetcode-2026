# LeetCode 3300 - Minimum Element After Replacement With Digit Sum

## 📝 Problem Statement

You are given an integer array `nums`.

You replace each element in `nums` with the **sum of its digits**.

Return the **minimum element** in `nums` after all replacements.

---

## 📌 Example 1

### Input:
```text
nums = [10,12,13,14]
```

### Output:
```text
1
```

### Explanation:

Replace each element with the sum of its digits:

- 10 → 1 + 0 = 1
- 12 → 1 + 2 = 3
- 13 → 1 + 3 = 4
- 14 → 1 + 4 = 5

After replacement:

```text
nums = [1,3,4,5]
```

Minimum element is `1`.

---

## 📌 Example 2

### Input:
```text
nums = [1,2,3,4]
```

### Output:
```text
1
```

### Explanation:

All numbers are already single digit.

Minimum element = `1`.

---

# 💡 Approach

1. Traverse through every number in the array.
2. Calculate the digit sum of each number:
   - Extract last digit using `% 10`
   - Remove last digit using `/ 10`
3. Compare every digit sum with the current minimum value.
4. Return the minimum digit sum.

---

# 🧠 Algorithm

```
Initialize ans = INT_MAX

For every number:
    sum = 0
    
    while number > 0:
        digit = number % 10
        sum += digit
        number /= 10
    
    ans = min(ans, sum)

Return ans
```

---

# 💻 C++ Code

```cpp
class Solution {
public:
    int minElement(vector<int>& nums) {

        int ans = INT_MAX;

        for(int i = 0; i < nums.size(); i++) {

            int num = nums[i];
            int sum = 0;

            while(num > 0) {

                int digit = num % 10;

                sum += digit;

                num /= 10;
            }

            ans = min(ans, sum);
        }

        return ans;
    }
};
```

---

# ⏱ Complexity Analysis

### Time Complexity

```
O(n * d)
```

Where:

- `n` = size of array
- `d` = number of digits in each number

---

### Space Complexity

```
O(1)
```

Only constant extra space is used.

---
