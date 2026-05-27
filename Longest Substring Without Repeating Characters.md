## Problem Statement

Given a string `s`, find the length of the longest substring without repeating characters.

A substring is a contiguous sequence of characters.

---

# Examples

## Example 1

```text
Input: s = "abcabcbb"

Output: 3
```

Explanation:

```text
The answer is "abc", with the length of 3.
```

---

## Example 2

```text
Input: s = "bbbbb"

Output: 1
```

Explanation:

```text
The answer is "b", with the length of 1.
```

---

## Example 3

```text
Input: s = "pwwkew"

Output: 3
```

Explanation:

```text
The answer is "wke", with the length of 3.
```

---

# Constraints

```text
0 <= s.length <= 5 * 10^4

s consists of English letters, digits, symbols and spaces.
```

---

# Intuition

We need to find:

```text
Longest substring without repeating characters
```

A substring must be continuous.

To solve efficiently:

- use Sliding Window
- use Hash Set

---

# Approach

We maintain:

```text
left  -> starting index of window
right -> ending index of window
```

We expand the window using `right`.

If duplicate character appears:

- shrink window from left
- remove characters until duplicate is removed

---

# Algorithm

## Step 1

Create:

- unordered_set
- left pointer
- maximum answer variable

---

## Step 2

Traverse string using `right`

### If character is duplicate:

```text
remove characters from left
move left forward
```

---

## Step 3

Insert current character into set.

---

## Step 4

Update maximum length.

---

# Dry Run

## Input

```text
s = "abcabcbb"
```

---

## Execution

| Left | Right | Window | Length |
|------|-------|---------|--------|
| 0 | 0 | a | 1 |
| 0 | 1 | ab | 2 |
| 0 | 2 | abc | 3 |
| duplicate a | shift left | |
| 1 | 3 | bca | 3 |

Maximum length = `3`

---

# C++ Solution

```cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) {

        unordered_set<char> st;

        int left = 0;
        int maxi = 0;

        for(int right = 0; right < s.length(); right++) {

            // duplicate character found
            while(st.find(s[right]) != st.end()) {

                st.erase(s[left]);
                left++;
            }

            // insert current character
            st.insert(s[right]);

            // update answer
            maxi = max(maxi, right - left + 1);
        }

        return maxi;
    }
};
```

---

# Code Explanation

## unordered_set<char> st

Stores unique characters of current window.

---

## left pointer

Represents start of sliding window.

---

## right pointer

Represents end of sliding window.

---

## while loop

```cpp
while(st.find(s[right]) != st.end())
```

Runs until duplicate character removed.

---

## Window Size

```cpp
right - left + 1
```

Calculates current substring length.

---

# Time Complexity

```text
O(n)
```

Each character is inserted and removed at most once.

---

# Space Complexity

```text
O(n)
```

Hash set stores characters.

---

# Key Concepts Used

- Sliding Window
- Two Pointers
- Hash Set
- String Traversal

---

# Why Sliding Window?

Because:

```text
Substring must be continuous
```

Sliding window efficiently handles continuous ranges.

---

# Edge Cases

## Case 1

```text
Input: s = ""
Output: 0
```

---

## Case 2

```text
Input: s = "aaaaa"
Output: 1
```

---

## Case 3

```text
Input: s = "abcdef"
Output: 6
```

---

# Optimized Approach

This solution is already optimized.

Why?

- Linear traversal
- No nested traversal
- Each character processed once

---
