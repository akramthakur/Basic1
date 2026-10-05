# Reverse Linked List - Solution

## Problem Statement
Given the head of a singly linked list, reverse the list and return the reversed list.

## Step-by-Step Logic

### Iterative Three-Pointer Approach:
1. **Initialize Pointers**: 
   - `prev` = NULL (will become new tail)
   - `cur` = head (current node being processed)
   - `next` = temporary storage for next node
2. **Traverse and Reverse**:
   - Store next node temporarily
   - Reverse current node's pointer to point to previous
   - Move prev and cur pointers one step forward
3. **Terminate**: When cur reaches NULL
4. **Return**: prev becomes new head

## Complexity Analysis

### Time Complexity: **O(n)**
- **O(n)** for single pass through the list
- **n** = number of nodes in linked list

### Space Complexity: **O(1)**
- **O(1)** - only using constant extra space for pointers
- In-place reversal

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
    ListNode* reverseList(ListNode* head) {
        ListNode* cur = head;    // Current node being processed
        ListNode* prev = NULL;   // Previous node (will become next pointer)
        ListNode* next;          // Temporary storage for next node
        
        // Traverse through the list and reverse pointers
        while(cur != NULL) {
            // Store next node before breaking the link
            next = cur->next;
            
            // Reverse the current node's pointer
            cur->next = prev;
            
            // Move pointers one step forward
            prev = cur;
            cur = next;
        }
        
        // prev is now the new head of reversed list
        return prev;
    }
};
