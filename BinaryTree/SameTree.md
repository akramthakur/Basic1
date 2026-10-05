# Same Tree - Solution

## Problem Statement
Given the roots of two binary trees `p` and `q`, check if they are structurally identical and have the same node values.

## Step-by-Step Logic

### Recursive Approach:
1. **Base Cases**:
   - Both nodes null → identical (return true)
   - One node null, other not null → different structure (return false)
   - Values different → different content (return false)

2. **Recursive Case**:
   - Check if left subtrees are identical
   - Check if right subtrees are identical
   - Return logical AND of both results

## Complexity Analysis

### Time Complexity: **O(n)**
- Visit each node exactly once in both trees
- n = number of nodes in the smaller tree

### Space Complexity: **O(h)**
- **Best Case**: O(log n) for balanced trees
- **Worst Case**: O(n) for skewed trees (recursion stack)
- h = height of the tree

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
        // Both nodes are null - identical
        if(p == nullptr && q == nullptr) {
            return true;
        }
        // One node is null, other is not - different structure
        else if(p == nullptr || q == nullptr) {
            return false;
        }

        // Values are different - different content
        if(p->val != q->val) {
            return false;
        }
        
        // Recursively check left and right subtrees
        return isSameTree(p->left, q->left) && isSameTree(p->right, q->right);
    }
};
