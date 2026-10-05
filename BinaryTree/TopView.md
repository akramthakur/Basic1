# Binary Tree Top View - Solution

## Problem Statement
Given a binary tree, return the top view of the tree - the nodes visible when looking from the top of the tree.

## Step-by-Step Logic

### Algorithm:
1. **Vertical Traversal with Depth Tracking**: 
   - Use DFS to traverse the tree
   - Track both horizontal distance (column) and depth (row)
2. **Map Storage**: 
   - Key: Horizontal distance (column)
   - Value: Pair of (depth, node value)
3. **Selection Criteria**: 
   - For each column, keep only the node with smallest depth (closest to top)

### Key Concepts:
- **Horizontal Distance**: 
  - Root = 0
  - Left child = parent - 1
  - Right child = parent + 1
- **Depth**: Distance from root (root depth = 0)

## Complexity Analysis

### Time Complexity: **O(n log n)**
- DFS traversal: O(n)
- Map operations: O(log n) per insertion
- Total: O(n log n)

### Space Complexity: **O(n)**
- Recursion stack: O(h) where h is tree height
- Map storage: O(n) in worst case

## Final Code with Comments

```cpp
/*
class Node {
  public:
    int data;
    Node* left;
    Node* right;

    Node(int val) {
        data = val;
        left = nullptr;
        right = nullptr;
    }
};
*/

class Solution {
    // DFS helper function
    void dfs(Node* root, map<int, pair<int, int>>& mp, int col, int row) {
        if (root == nullptr)
            return;
            
        // If this column hasn't been visited, or current node is higher (smaller row)
        if (mp.find(col) == mp.end() || row < mp[col].first) {
            mp[col] = {row, root->data};
        }
        
        // Recursively traverse left and right subtrees
        dfs(root->left, mp, col - 1, row + 1);  // Left: column decreases
        dfs(root->right, mp, col + 1, row + 1); // Right: column increases
    }
    
  public:
    vector<int> topView(Node *root) {
        vector<int> ans;
        map<int, pair<int, int>> mp; // column -> (row, value)
        
        dfs(root, mp, 0, 0);
        
        // Extract values in column order (left to right)
        for (auto &x : mp) {
            ans.push_back(x.second.second);
        }
        return ans;
    }
};
