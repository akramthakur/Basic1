# Heap Validation - Solution

## Problem Statement
Check if a given binary tree is both:
1. **Complete Binary Tree**: All levels are completely filled except possibly the last level, which is filled from left to right
2. **Max Heap**: Every parent node has value greater than or equal to its children

## Step-by-Step Logic

### Algorithm:
1. **Level Order Traversal** using queue
2. **Completeness Check**: Track if we encounter any null node
   - Once a null node is found, all subsequent nodes must also be null
3. **Heap Property Check**: Verify parent ≥ children
   - Check both left and right children against parent

### Key Conditions:
- **Complete Tree**: No gaps in level order traversal
- **Max Heap**: Parent value ≥ both children values

## Complexity Analysis

### Time Complexity: **O(n)**
- We visit each node exactly once

### Space Complexity: **O(n)**
- Queue can store up to n/2 nodes in worst case

## Final Code with Comments

```cpp
/*
class Node {
   public:
    int data;
    Node *left;
    Node *right;

    Node(int val) {
        data = val;
        left = right = NULL;
    }
};
*/

class Solution {
  public:
    bool isHeap(Node* tree) {
        if (!tree) return true;
        
        queue<Node*> q;
        q.push(tree);
        bool foundNull = false;
        
        while (!q.empty()) {
            Node* curr = q.front();
            q.pop();
            
            // Check left child
            if (curr->left) {
                // If null node found before, tree is not complete
                if (foundNull) return false;
                // Check max heap property: left child ≤ parent
                if (curr->left->data > curr->data) return false;
                q.push(curr->left);
            } else {
                foundNull = true;
            }
            
            // Check right child
            if (curr->right) {
                // If null node found before, tree is not complete
                if (foundNull) return false;
                // Check max heap property: right child ≤ parent
                if (curr->right->data > curr->data) return false;
                q.push(curr->right);
            } else {
                foundNull = true;
            }
        }
        
        return true;
    }
};
