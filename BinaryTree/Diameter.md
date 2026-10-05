# Diameter of Binary Tree - Solution

## Problem Statement
Given the root of a binary tree, return the length of the diameter of the tree. The diameter is defined as the length of the longest path between any two nodes in a tree (number of edges between them).

## Step-by-Step Logic

### Modified Depth Calculation:
1. **Calculate Depth**: For each node, compute the depth of left and right subtrees
2. **Update Diameter**: At each node, potential diameter = left depth + right depth
3. **Return Depth**: Return the depth of current subtree (1 + max(left, right))
4. **Track Maximum**: Maintain a reference to track the maximum diameter found

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
    int maxDepth(TreeNode* root, int& diameter) {
        if(root == nullptr) {
            return 0;  // Base case: empty subtree has depth 0
        }
        
        // Recursively get depths of left and right subtrees
        int left = maxDepth(root->left, diameter);
        int right = maxDepth(root->right, diameter);
        
        // Update diameter: longest path through current node
        diameter = max(diameter, left + right);
        
        // Return depth of current subtree
        return 1 + max(left, right);
    }
    
    int diameterOfBinaryTree(TreeNode* root) {
        int diameter = 0;
        maxDepth(root, diameter);
        return diameter;
    }
};
