# Binary Tree Inorder Traversal - Solution

## Problem Statement
Given the root of a binary tree, return the inorder traversal of its nodes' values.

**Inorder Traversal**: Left → Root → Right

## Step-by-Step Logic

### Recursive Approach:
1. **Traverse Left**: Recursively traverse left subtree first
2. **Visit Root**: Process current node after left subtree
3. **Traverse Right**: Recursively traverse right subtree last
4. **Base Case**: Return when node is null

## Complexity Analysis

### Time Complexity: **O(n)**
- Visit each node exactly once
- n = number of nodes in tree

### Space Complexity: **O(h)**
- **Best Case**: O(log n) for balanced tree
- **Worst Case**: O(n) for skewed tree (recursion stack)
- h = height of tree

## Final Code with Comments

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    vector<int> inorder(TreeNode* root, vector<int>& ans) {
        if(root == nullptr) {
            return ans;  // Base case: null node
        }
        
        // Inorder: Left → Root → Right
        inorder(root->left, ans);          // Traverse left subtree first
        ans.push_back(root->val);          // Visit root
        inorder(root->right, ans);         // Traverse right subtree last
        
        return ans;
    }
    
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> ans;
        return inorder(root, ans);
    }
};
