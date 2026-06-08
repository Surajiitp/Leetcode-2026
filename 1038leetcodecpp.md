# 1038. Binary Search Tree to Greater Sum Tree

## Problem Statement

Given the root of a Binary Search Tree (BST), convert it to a Greater Sum Tree such that every key of the original BST is changed to the original key plus the sum of all keys greater than it in the BST.

LeetCode Link: https://leetcode.com/problems/binary-search-tree-to-greater-sum-tree/

---

## Approach

Since the tree is a **Binary Search Tree**, all values in the right subtree are greater than the current node.

Instead of using the normal inorder traversal (**Left → Root → Right**), we perform a **Reverse Inorder Traversal**:

```text
Right → Root → Left
```

During traversal:

1. Visit the right subtree first.
2. Maintain a running sum of visited nodes.
3. Add the current node's value to the running sum.
4. Update the current node with the running sum.
5. Traverse the left subtree.

This ensures that when a node is processed, the running sum already contains all greater values.

---

## Algorithm

1. Initialize `sum = 0`.
2. Perform Reverse Inorder Traversal.
3. For each node:
   - Add node value to `sum`.
   - Update node value with `sum`.
4. Return the modified root.

---

## C++ Solution

```cpp
class Solution {
public:
    int sum = 0;

    void solve(TreeNode* root) {
        if (!root) return;

        solve(root->right);

        sum += root->val;
        root->val = sum;

        solve(root->left);
    }

    TreeNode* bstToGst(TreeNode* root) {
        solve(root);
        return root;
    }
};
```

---

## Example

### Input

```text
       4
     /   \
    1     6
```

### Reverse Inorder Traversal

```text
6 → 4 → 1
```

### Running Sum

| Node | Running Sum | Updated Value |
|------|------------|--------------|
| 6 | 6 | 6 |
| 4 | 10 | 10 |
| 1 | 11 | 11 |

### Output

```text
       10
      /  \
    11    6
```

---

## Complexity Analysis

### Time Complexity

```text
O(n)
```

Each node is visited exactly once.

### Space Complexity

```text
O(h)
```

Where `h` is the height of the tree due to the recursion stack.

---

## Key Insight

For BST problems involving **greater values**, think of **Reverse Inorder Traversal (Right → Root → Left)** because it visits nodes in descending order.
