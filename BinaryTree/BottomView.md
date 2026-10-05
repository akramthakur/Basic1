# Binary Tree Bottom View - Solution

## Problem Statement
Given a binary tree, return the bottom view of the tree - the nodes visible when looking from the bottom of the tree.

## Step-by-Step Logic

### Algorithm:
1. **Level Order Traversal with Horizontal Distance Tracking**: 
   - Use BFS to traverse the tree level by level
   - Track horizontal distance (column) for each node
2. **Map Storage**: 
   - Key: Horizontal distance (column)
   - Value: Node value (last node seen in that column)
3. **Selection Criteria**: 
   - For each column, keep the **last** node encountered (deepest node in that column)

### Key Concepts:
- **Horizontal Distance**: 
  - Root = 0
  - Left child = parent - 1
  - Right child = parent + 1
- **Bottom View**: The deepest node in each vertical column

## Complexity Analysis

### Time Complexity: **O(n log n)**
- BFS traversal: O(n)
- Map operations: O(log n) per insertion
- Total: O(n log n)

### Space Complexity: **O(n)**
- Queue storage: O(w) where w is maximum width
- Map storage: O(n) in worst case

## Final Code with Comments

```cpp
/*
class Node {
public:
    int data;
    Node* left;
    Node* right;

    Node(int x) {
        data = x;
        left = right = NULL;
    }
};
*/

class Solution {
  public:
    vector<int> bottomView(Node *root) {
        vector<int> ans;
        if (!root) return ans;
        
        map<int, int> map; // column -> node value
        queue<pair<int, Node*>> que; // (column, node)
        
        que.push({0, root});
        
        while (!que.empty()) {
            auto it = que.front();
            que.pop();
            
            int col = it.first;
            Node* node = it.second;
            
            // Always update with the latest node in this column
            // This ensures we get the bottom-most node
            map[col] = node->data;
            
            // Process left and right children
            if (node->left) {
                que.push({col - 1, node->left});
            }
            if (node->right) {
                que.push({col + 1, node->right});
            }
        }
        
        // Extract values in column order (left to right)
        for (auto [key, val] : map) {
            ans.push_back(val);
        }
        return ans;
    }
};
