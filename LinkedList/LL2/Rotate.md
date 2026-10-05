# Rotate Linked List - Solution

## Problem Statement
Given the head of a linked list, rotate the list to the right by k places.

## Step-by-Step Logic

### Efficient Rotation Algorithm:
1. **Edge Cases**: Handle empty list, single node, or k = 0
2. **Calculate Length**: Traverse to find list length and connect tail to head (make circular)
3. **Optimize k**: k = k % n (handle k > n cases)
4. **Find New Tail**: Traverse to (n - k - 1)th node
5. **Break and Reconnect**: Set new head and break the circle

## Complexity Analysis

### Time Complexity: **O(n)**
- **O(n)** to find length of list
- **O(n)** to find new tail position
- **n** = number of nodes in linked list

### Space Complexity: **O(1)**
- **O(1)** - only using constant extra space for pointers
- In-place rotation

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
    ListNode* rotateRight(ListNode* head, int k) {
        // Edge cases: empty list, single node, or no rotation needed
        if (!head || !head->next || k == 0) return head;
        
        // Step 1: Calculate length of linked list
        ListNode* temp = head;
        int n = 1; // Start from 1 since we're at head already
        while(temp->next != nullptr) {
            temp = temp->next;
            n++;
        }
        
        // Step 2: Optimize k (handle cases where k >= n)
        k = k % n;
        if(k == 0) return head; // No rotation needed after optimization
        
        // Step 3: Make the list circular
        temp->next = head;
        
        // Step 4: Find the new tail (n - k - 1)th node
        temp = head;
        for(int i = 0; i < n - k - 1; i++) {
            temp = temp->next;
        }
        
        // Step 5: Break the circle and set new head
        ListNode* newHead = temp->next;
        temp->next = nullptr;
        
        return newHead;
    }
};
