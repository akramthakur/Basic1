# Sum of Left Leaves - Solution

## Problem Statement
Given the root of a binary tree, return the sum of all left leaves. A left leaf is a leaf node that is the left child of another node.

## Step-by-Step Logic

### Recursive DFS Approach:
1. **Base Case**: If node is null, return 0
2. **Left Leaf Check**: If current node has a left child that is a leaf, add its value
3. **Recursive Sum**: Recursively sum left leaves from left and right subtrees
4. **Return Total**: Return accumulated sum of left leaves

## Complexity Analysis

### Time Complexity: **O(n)**
- **O(n)** for visiting each node exactly once
- **n** = number of nodes in the tree

### Space Complexity: **O(h)**
- **Best Case**: O(log n) for balanced tree
- **Worst Case**: O(n) for skewed tree (recursion stack)
- **h** = height of the tree

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
    int sumOfLeftLeaves(TreeNode* root) {
        // Base case: empty tree has no left leaves
        if(!root)
            return 0;
        
        int sum = 0;
        
        // Check if left child exists and is a leaf node
        if (root->left && !root->left->left && !root->left->right)
            sum += root->left->val;  // Add left leaf value
        
        // Recursively sum left leaves from left and right subtrees
        sum += sumOfLeftLeaves(root->left);
        sum += sumOfLeftLeaves(root->right);
        
        return sum;
    }
};
