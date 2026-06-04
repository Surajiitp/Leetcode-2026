# LeetCode 105 - Construct Binary Tree from Preorder and Inorder Traversal

## Problem Statement

Given two integer arrays `preorder` and `inorder` where:

- `preorder` is the preorder traversal of a binary tree (`Root → Left → Right`)
- `inorder` is the inorder traversal of the same tree (`Left → Root → Right`)

Construct and return the binary tree.

---

## Approach

### Key Observations

1. The first element in preorder is always the root.
2. In inorder traversal:
   - Left side of root = left subtree
   - Right side of root = right subtree
3. Recursively build left and right subtrees.

---

## C++ Solution

```cpp
class Solution {
public:
    unordered_map<int, int> inorderMap;
    int preIndex = 0;

    TreeNode* build(vector<int>& preorder, int left, int right) {
        if (left > right) return nullptr;

        int rootVal = preorder[preIndex++];
        TreeNode* root = new TreeNode(rootVal);

        int mid = inorderMap[rootVal];

        root->left = build(preorder, left, mid - 1);
        root->right = build(preorder, mid + 1, right);

        return root;
    }

    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        for (int i = 0; i < inorder.size(); i++) {
            inorderMap[inorder[i]] = i;
        }

        return build(preorder, 0, inorder.size() - 1);
    }
};
```

---

## Complexity Analysis

- Time Complexity: O(n)
- Space Complexity: O(n)

---

## Topics

- Binary Tree
- DFS
- Recursion
- Hash Map

