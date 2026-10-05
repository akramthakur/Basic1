# Add Two Numbers - Solution

## Problem Statement
You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

## Step-by-Step Logic

1. **Initialize Result**:
   - Create dummy node to simplify list construction
   - Initialize carry to 0
   - Use tail pointer to build result list

2. **Process Digits**:
   - While either list has nodes OR carry exists
   - Extract digits from current nodes (use 0 if list exhausted)
   - Calculate sum = digit1 + digit2 + carry
   - Update carry = sum / 10
   - Create new node with digit = sum % 10

3. **Move Pointers**:
   - Advance list pointers if nodes exist
   - Move tail to newly created node

4. **Return Result**:
   - Skip dummy node and return actual head

## Complexity Analysis

### Time Complexity: **O(max(m, n))**
- m = length of l1, n = length of l2
- Process each node exactly once
- Continue until both lists exhausted and carry is 0

### Space Complexity: **O(max(m, n))**
- New linked list to store result
- Maximum length = max(m, n) + 1 (for potential carry)

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
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        // Create dummy node to simplify list construction
        ListNode* ans = new ListNode(0);
        int carry = 0;
        ListNode* tail = ans;  // Pointer to build result list
        
        // Continue while either list has nodes or carry exists
        while(l1 != nullptr || l2 != nullptr || carry != 0) {
            // Get digits from current nodes (0 if list exhausted)
            int digit1 = (l1 != nullptr) ? l1->val : 0;
            int digit2 = (l2 != nullptr) ? l2->val : 0;
            
            // Calculate sum and carry
            int sum = digit1 + digit2 + carry;
            carry = sum / 10;    // Update carry for next iteration
            int digit = sum % 10; // Current digit for result
            
            // Create new node and add to result list
            ListNode* node = new ListNode(digit);
            tail->next = node;
            tail = tail->next;
            
            // Move to next nodes in input lists
            l1 = (l1 != nullptr) ? l1->next : nullptr;
            l2 = (l2 != nullptr) ? l2->next : nullptr;
        }
        
        // Return actual head (skip dummy node)
        ListNode* res = ans->next;
        delete ans;  // Clean up dummy node
        return res;
    }
};
