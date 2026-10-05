# Middle of the Linked List - Solution

## Problem Statement
Given the head of a singly linked list, return the middle node of the linked list. If there are two middle nodes, return the second middle node.

## Step-by-Step Logic

1. **Two Pointer Technique (Tortoise and Hare)**:
   - **Slow pointer**: Moves one step at a time
   - **Fast pointer**: Moves two steps at a time
   - When fast pointer reaches end, slow pointer is at middle

2. **Even vs Odd Length Handling**:
   - **Odd length**: Fast reaches last node, slow at exact middle
   - **Even length**: Fast reaches null, slow at second middle

3. **Termination Condition**:
   - Stop when fast is null OR fast->next is null
   - This ensures we handle both even and odd lengths correctly

## Complexity Analysis

### Time Complexity: **O(n)**
- Single pass through the list
- Fast pointer traverses n nodes
- Slow pointer traverses n/2 nodes

### Space Complexity: **O(1)**
- Only two pointers used regardless of input size
- Constant extra space

## Final Code with Comments

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* middleNode(ListNode* head) {
        // Initialize both pointers at head
        ListNode* fast = head;
        ListNode* slow = head;
        
        // Traverse until fast reaches end
        while(fast != nullptr && fast->next != nullptr) {
            slow = slow->next;        // Move slow by 1 step
            fast = fast->next->next;  // Move fast by 2 steps
        }
        
        // Slow pointer is now at the middle
        return slow;
    }
};
