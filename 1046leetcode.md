# 1046. Last Stone Weight

## Problem Statement

You are given an array of integers `stones` where `stones[i]` is the weight of the `iᵗʰ` stone.

We are playing a game with the stones. On each turn, we choose the two heaviest stones and smash them together.

- If both stones have the same weight, both stones are destroyed.
- If the stones have different weights, the lighter stone is destroyed, and the heavier stone's new weight becomes the difference between the two weights.

Continue this process until there is at most one stone left.

Return the weight of the last remaining stone. If no stones remain, return `0`.

---

## Approach

A **Max Heap (Priority Queue)** is ideal for this problem because we repeatedly need access to the two heaviest stones.

### Steps
1. Insert all stone weights into a max heap.
2. While the heap contains more than one stone:
   - Extract the two largest stones.
   - If they are not equal, insert their difference back into the heap.
3. Return:
   - The remaining stone's weight if the heap is not empty.
   - Otherwise, return `0`.

---

## C++ Solution

```cpp
class Solution {
public:
    int lastStoneWeight(vector<int>& stones) {
        priority_queue<int> pq;

        for (int stone : stones) {
            pq.push(stone);
        }

        while (pq.size() > 1) {
            int y = pq.top();
            pq.pop();

            int x = pq.top();
            pq.pop();

            if (y != x) {
                pq.push(y - x);
            }
        }

        return pq.empty() ? 0 : pq.top();
    }
};
```

---

## Example

### Input
```text
stones = [2,7,4,1,8,1]
```

### Process
```text
8 and 7 -> 1
4 and 2 -> 2
2 and 1 -> 1
1 and 1 -> 0
```

### Output
```text
1
```

---

## Complexity Analysis

| Complexity | Value |
|------------|--------|
| Time | O(n log n) |
| Space | O(n) |

---

## Key Takeaway

This problem is a classic application of a **Max Heap (Priority Queue)** where the largest elements must be accessed repeatedly in an efficient manner.
