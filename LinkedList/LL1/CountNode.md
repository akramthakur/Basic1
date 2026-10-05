# Count Nodes in Linked List - Solution

## Problem Statement
Given the head of a singly linked list, count and return the number of nodes in the list.

## Step-by-Step Logic

### Iterative Counting Approach:
1. **Initialize**: Start from head node with counter = 0
2. **Traverse List**: Move through each node using next pointers
3. **Increment Counter**: Count each node visited
4. **Terminate**: When reaching NULL (end of list)
5. **Return Count**: Total number of nodes

## Complexity Analysis

### Time Complexity: **O(n)**
- **O(n)** for single pass through the entire list
- **n** = number of nodes in linked list
- Must visit every node to count

### Space Complexity: **O(1)**
- **O(1)** - only using constant extra space for pointers and counter
- No additional data structures used

## Final Code with Comments

```cpp
/*
class Node {
  public:
    int data;
    Node *next;

    Node(int x) {
        data = x;
        next = NULL;
    }
};
*/

class Solution {
  public:
    int getCount(Node* head) {
        // Temporary pointer to traverse the list
        Node* temp = head;
        int cnt = 0;
        
        // Traverse until we reach the end of list (NULL)
        while(temp != nullptr) {
            // Move to next node
            temp = temp->next;
            // Increment node counter
            cnt++;
        }
        
        return cnt;
    }
};
