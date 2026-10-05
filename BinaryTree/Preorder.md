# Binary Tree Preorder Traversal - Solution

## Problem Statement
Given the root of a binary tree, return the preorder traversal of its nodes' values.

**Preorder Traversal**: Root → Left → Right

## Step-by-Step Logic

### Recursive Approach:
1. **Visit Root**: Process current node first
2. **Traverse Left**: Recursively traverse left subtree  
3. **Traverse Right**: Recursively traverse right subtree
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
    vector<int> preorder(TreeNode* root, vector<int>& ans) {
        if(root == nullptr) {
            return ans;  // Base case: null node
        }
        
        // Preorder: Root → Left → Right
        ans.push_back(root->val);           // Visit root
        preorder(root->left, ans);          // Traverse left subtree
        preorder(root->right, ans);         // Traverse right subtree
        
        return ans;
    }
    
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> ans;
        return preorder(root, ans);
    }
};
