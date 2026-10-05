# Merge Two Sorted Lists - Solution

## Problem Statement
Merge two sorted linked lists and return it as a new sorted list. The new list should be made by splicing together the nodes of the first two lists.

## Step-by-Step Logic

1. **Dummy Node Technique**:
   - Create a dummy node to simplify edge cases
   - Use a current pointer to build the new list
   - Return dummy.next as the head of merged list

2. **Two Pointer Comparison**:
   - Compare current nodes from both lists
   - Attach the smaller node to the result list
   - Move the pointer of the chosen list forward

3. **Remaining Elements**:
   - After one list is exhausted, attach the remaining nodes
   - No need to traverse remaining list - just link directly

## Complexity Analysis

### Time Complexity: **O(n + m)**
- n = length of list1, m = length of list2
- Each node visited exactly once
- Total operations: n + m comparisons

### Space Complexity: **O(1)**
- Only using dummy node and pointers
- No additional data structures created
- In-place merging using existing nodes

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
    ListNode* mergeTwoLists(ListNode* list1, ListNode* list2) {
        // Create dummy node to simplify edge cases
        ListNode dummy(0);      
        ListNode* ans = &dummy;  // Pointer to build new list
        
        ListNode* fast = list1;  // Pointer for first list
        ListNode* slow = list2;  // Pointer for second list
        
        // Compare and merge while both lists have nodes
        while(fast != NULL && slow != NULL) {
            if(fast->val < slow->val) {
                // Attach node from first list
                ans->next = fast;
                fast = fast->next;
            } else {
                // Attach node from second list
                ans->next = slow;
                slow = slow->next;
            }
            ans = ans->next;  // Move result pointer forward
        }
        
        // Attach remaining nodes from whichever list is not empty
        ans->next = (fast != NULL) ? fast : slow;
        
        // Return head of merged list (skip dummy node)
        return dummy.next;
    }
};
