# Path Sum - Solution

## Problem Statement
Given the root of a binary tree and an integer `targetSum`, return true if the tree has a root-to-leaf path such that the sum of all node values along the path equals `targetSum`.

## Step-by-Step Logic

### Recursive DFS Approach:
1. **Base Case 1**: If node is null, no path exists (return false)
2. **Base Case 2**: If node is leaf, check if node value equals remaining targetSum
3. **Recursive Case**: 
   - Subtract current node value from targetSum
   - Check if either left or right subtree has path with remaining sum

## Complexity Analysis

### Time Complexity: **O(n)**
- Visit each node exactly once in worst case
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
    bool hasPathSum(TreeNode* root, int targetSum) {
        // Base case: empty tree has no paths
        if(root == nullptr) {
            return false;
        }
        
        // Base case: leaf node - check if path sum equals target
        if(root->left == nullptr && root->right == nullptr) {
            return root->val == targetSum;
        }
        
        // Recursive case: check left and right subtrees with reduced target
        int remainingSum = targetSum - root->val;
        return hasPathSum(root->left, remainingSum) || 
               hasPathSum(root->right, remainingSum);
    }
};
