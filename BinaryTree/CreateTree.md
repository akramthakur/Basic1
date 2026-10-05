# Create Binary Tree from Descriptions - Solution

## Problem Statement
Given a 2D array `descriptions` where each element is `[parent, child, isLeft]`, construct a binary tree and return its root.

## Step-by-Step Logic

### Approach:
1. **Track Children**: Use a set to track all child nodes
2. **Build Tree Map**: Use hash map to store parent-child relationships
3. **Find Root**: Root is the node that never appears as a child
4. **Recursive Construction**: Build tree recursively using the map

## Complexity Analysis

### Time Complexity: **O(n)**
- Process all descriptions: O(n)
- Find root: O(n) in worst case
- Build tree: O(n) recursive calls
- Total: O(3n) = O(n)

### Space Complexity: **O(n)**
- Hash map storage: O(n)
- Children set: O(n)
- Recursion stack: O(h) where h is tree height

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
    TreeNode* createBinaryTree(vector<vector<int>>& desc) {
        unordered_set<int> children;  // Track all child nodes
        unordered_map<int, pair<int, int>> tree;  // parent -> (left, right)
        
        // Process all descriptions
        for(int i = 0; i < desc.size(); i++) {
            int parent = desc[i][0];
            int child = desc[i][1];
            bool isleft = desc[i][2] == 1;
            
            // Initialize parent if not exists
            if(tree.find(parent) == tree.end()) {
                tree[parent] = {-1, -1};  // -1 indicates no child
            }
            
            // Mark child node
            children.insert(child);
            
            // Assign child to appropriate position
            if(isleft) {
                tree[parent].first = child;
            } else {
                tree[parent].second = child;
            }
        }
        
        // Find root (node that is never a child)
        int root;
        for(auto& [parent, child] : tree) {
            if(children.find(parent) == children.end()) {
                root = parent;
                break;
            }
        }
        
        // Construct tree recursively
        return construct(root, tree);
    }
    
    TreeNode* construct(int head, unordered_map<int, pair<int, int>>& tree) {
        TreeNode* root = new TreeNode(head);
        
        // Check if current node has children in the map
        if(tree.find(head) != tree.end()) {
            pair<int, int> children = tree[head];
            
            // Build left subtree if left child exists
            if(children.first != -1) {
                root->left = construct(children.first, tree);
            }
            
            // Build right subtree if right child exists
            if(children.second != -1) {
                root->right = construct(children.second, tree);
            }
        }
        
        return root;
    }
};
