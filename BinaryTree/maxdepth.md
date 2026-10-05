# Maximum Depth of Binary Tree - Solution

## Problem Statement
Given the root of a binary tree, find its maximum depth (height). The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

## Step-by-Step Logic

### Recursive Approach:
1. **Base Case**: If node is null, depth is 0
2. **Recursive Case**: 
   - Calculate depth of left subtree
   - Calculate depth of right subtree
   - Return 1 + maximum of left and right depths

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
    int maxDepth(TreeNode* root) {
        if(root == nullptr) {
            return 0;  // Base case: empty tree has depth 0
        }
        
        // Depth = 1 (current node) + max depth of subtrees
        return 1 + max(maxDepth(root->left), maxDepth(root->right));
    }
};
