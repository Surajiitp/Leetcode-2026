# Merge Two BSTs into a Balanced BST

## Problem Statement

Given two Binary Search Trees (BSTs), merge them into a single balanced BST containing all elements from both trees.

---

## Approach

### Step 1: Store Inorder Traversal

Perform inorder traversal of both BSTs and store the nodes in two separate vectors.

Since inorder traversal of a BST gives elements in sorted order, both vectors will be sorted.

### Step 2: Merge Two Sorted Arrays

Merge the two sorted vectors into a single sorted vector using the two-pointer technique.

### Step 3: Build Balanced BST

Construct a balanced BST from the merged sorted array by choosing the middle element as the root recursively.

---

## Algorithm

1. Get inorder traversal of BST1 → `nodes1`
2. Get inorder traversal of BST2 → `nodes2`
3. Merge `nodes1` and `nodes2` into `nodes`
4. Convert `nodes` into a balanced BST
5. Return the root of the balanced BST

---

## C++ Solution

```cpp
class Solution {
public:
    void getInorder(TreeNode* root, vector<int>& nodes) {
        if (!root) return;

        getInorder(root->left, nodes);
        nodes.push_back(root->val);
        getInorder(root->right, nodes);
    }

    vector<int> mergeArrays(vector<int>& a, vector<int>& b) {
        vector<int> ans;
        int i = 0, j = 0;

        while (i < a.size() && j < b.size()) {
            if (a[i] < b[j])
                ans.push_back(a[i++]);
            else
                ans.push_back(b[j++]);
        }

        while (i < a.size())
            ans.push_back(a[i++]);

        while (j < b.size())
            ans.push_back(b[j++]);

        return ans;
    }

    TreeNode* buildBST(vector<int>& arr, int s, int e) {
        if (s > e) return NULL;

        int mid = s + (e - s) / 2;

        TreeNode* root = new TreeNode(arr[mid]);

        root->left = buildBST(arr, s, mid - 1);
        root->right = buildBST(arr, mid + 1, e);

        return root;
    }

    TreeNode* mergeBSTs(TreeNode* root1, TreeNode* root2) {
        vector<int> nodes1;
        vector<int> nodes2;
        vector<int> nodes;

        getInorder(root1, nodes1);
        getInorder(root2, nodes2);

        nodes = mergeArrays(nodes1, nodes2);

        return buildBST(nodes, 0, nodes.size() - 1);
    }
};
```

---

## Example

### Input

BST 1

```text
    2
   / \
  1   4
```

BST 2

```text
      9
     / \
    3   12
```

### Merged Sorted Array

```text
[1, 2, 3, 4, 9, 12]
```

### Balanced BST

```text
       3
      / \
     1   9
      \ / \
       2 4 12
```

---

## Complexity Analysis

### Time Complexity

- Inorder Traversal: `O(N + M)`
- Merging Arrays: `O(N + M)`
- Building BST: `O(N + M)`

**Overall:** `O(N + M)`

### Space Complexity

- Inorder Arrays: `O(N + M)`
- Recursion Stack: `O(log(N + M))`

**Overall:** `O(N + M)`

---

## Key Concepts

- Binary Search Tree (BST)
- Inorder Traversal
- Two Pointer Technique
- Merge Sorted Arrays
- Divide and Conquer
- Balanced BST Construction

--
