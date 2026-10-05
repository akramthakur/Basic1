# Binary Tree Right Side View - Solution

## Problem Statement
Given the root of a binary tree, imagine yourself standing on the right side of it, return the values of the nodes you can see ordered from top to bottom.

## Step-by-Step Logic

### Modified Pre-order DFS (Root → Right → Left):
1. **Traversal Order**: Process root, then right subtree, then left subtree
2. **Level Tracking**: Keep track of current depth using parameter `i`
3. **First Node Capture**: At each level, the first node encountered (rightmost) is added to result
4. **Result Size Check**: If result size equals current level, it means we're visiting this level for the first time
5. **Recursive Exploration**: Explore right subtree first to capture rightmost nodes

## Complexity Analysis

### Time Complexity: **O(n)**
- **O(n)** for visiting each node exactly once
- **n** = number of nodes in the tree

### Space Complexity: **O(h)**
- **O(h)** for recursion stack in worst case
- **Best Case**: O(log n) for balanced tree
- **Worst Case**: O(n) for skewed tree
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
    void rec(TreeNode* root, vector<int>& res, int i) {
        if(root == nullptr) return;
        
        // If this is the first node we're encountering at level i
        // (since we traverse right first, this will be the rightmost node)
        if(res.size() == i) {
            res.push_back(root->val);
        }
        
        // Traverse right subtree first (ensures we see rightmost nodes first)
        rec(root->right, res, i + 1);
        // Then traverse left subtree
        rec(root->left, res, i + 1);
    }
    
    vector<int> rightSideView(TreeNode* root) {
        vector<int> res;
        rec(root, res, 0);
        return res;
    }
};
