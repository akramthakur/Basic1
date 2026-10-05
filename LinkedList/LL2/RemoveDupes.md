# Remove Duplicates from Sorted List - Solution

## Problem Statement
Given the head of a sorted linked list, delete all duplicates such that each element appears only once. Return the linked list sorted as well.

## Step-by-Step Logic

1. **Edge Case Check**:
   - If list is empty, return nullptr immediately

2. **Single Pointer Traversal**:
   - Use temp pointer to traverse the list
   - Compare current node with next node
   - Skip duplicate nodes by bypassing them
   - Only move pointer when no duplicate found

3. **Duplicate Removal**:
   - When duplicate found: temp->next = temp->next->next
   - When no duplicate: move temp to next node
   - This removes duplicates in-place

## Complexity Analysis

### Time Complexity: **O(n)**
- Single pass through the linked list
- Each node visited exactly once
- n = number of nodes in the list

### Space Complexity: **O(1)**
- Only using constant extra space for pointers
- In-place modification of existing list

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
    ListNode* deleteDuplicates(ListNode* head) {
        // Handle empty list
        if (!head) return nullptr;
        
        ListNode* temp = head;
        
        // Traverse until second last node
        while(temp->next != nullptr) {
            if(temp->val == temp->next->val) {
                // Duplicate found - skip the next node
                temp->next = temp->next->next;
            } else {
                // No duplicate - move to next node
                temp = temp->next;
            }
        }
        return head;
    }
};
