# Symmetric Tree - Solution

## Problem Statement
Given the root of a binary tree, check whether it is a mirror of itself (symmetric around its center).

## Step-by-Step Logic

### Modified Tree Comparison Approach:
1. **Mirror Comparison**: Instead of comparing `left↔left` and `right↔right`, compare `left↔right` and `right↔left`
2. **Base Cases**:
   - Both nodes null → symmetric (return true)
   - One node null, other not null → asymmetric (return false)
   - Values different → asymmetric (return false)
3. **Recursive Case**:
   - Check if left subtree mirrors right subtree
   - Check if right subtree mirrors left subtree

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
    bool isSameTree(TreeNode* p, TreeNode* q) {
        // Both nodes are null - symmetric
        if(p == nullptr && q == nullptr) {
            return true;
        }
        // One node is null, other is not - asymmetric
        else if(p == nullptr || q == nullptr) {
            return false;
        }

        // Values are different - asymmetric
        if(p->val != q->val) {
            return false;
        }
        
        // Mirror comparison: left↔right and right↔left
        return isSameTree(p->left, q->right) && isSameTree(p->right, q->left);
    }
    
    bool isSymmetric(TreeNode* root) {
        // Empty tree is symmetric by definition
        if(root == nullptr) return true;
        
        // Check if left and right subtrees are mirrors
        return isSameTree(root->left, root->right);
    }
};
