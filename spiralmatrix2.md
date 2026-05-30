## 📌 Problem

Given a positive integer `n`, generate an `n x n` matrix filled with elements from `1` to `n²` in spiral order.

### Example

Input:

```text
n = 3
```

Output:

```text
[
 [1, 2, 3],
 [8, 9, 4],
 [7, 6, 5]
]
```

---

## 💡 Approach

We maintain four boundaries:

- Top
- Bottom
- Left
- Right

Starting from `1`, we fill the matrix layer by layer in spiral order:

1. Left → Right
2. Top → Bottom
3. Right → Left
4. Bottom → Top

After each traversal, the corresponding boundary is updated.

---

## 🚀 C++ Solution

```cpp
class Solution {
public:
    vector<vector<int>> generateMatrix(int n) {

        vector<vector<int>> matrix(n, vector<int>(n));

        int top = 0, bottom = n - 1;
        int left = 0, right = n - 1;

        int num = 1;

        while (top <= bottom && left <= right) {

            for (int j = left; j <= right; j++) {
                matrix[top][j] = num++;
            }
            top++;

            for (int i = top; i <= bottom; i++) {
                matrix[i][right] = num++;
            }
            right--;

            if (top <= bottom) {
                for (int j = right; j >= left; j--) {
                    matrix[bottom][j] = num++;
                }
                bottom--;
            }

            if (left <= right) {
                for (int i = bottom; i >= top; i--) {
                    matrix[i][left] = num++;
                }
                left++;
            }
        }

        return matrix;
    }
};
```

---

## 🔍 Dry Run (n = 3)

Final Matrix:

```text
1 2 3
8 9 4
7 6 5
```

---

## ⏱️ Complexity Analysis

| Complexity | Value |
|------------|--------|
| Time | O(n²) |
| Space | O(n²) |

---
