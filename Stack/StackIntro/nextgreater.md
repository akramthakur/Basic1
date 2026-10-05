# Next Greater Element I - Solution

## Problem Statement
Given two arrays `nums1` and `nums2` where `nums1` is a subset of `nums2`, for each element in `nums1`, find the next greater element in `nums2` to the right. If it doesn't exist, output -1.

## Step-by-Step Logic

### Monotonic Stack Approach:
1. **Process nums2**: Use stack to find next greater element for all elements
2. **Right to Left**: Traverse nums2 from end to beginning
3. **Maintain Decreasing Stack**: Pop elements smaller than current
4. **Store Results**: Map each element to its next greater element
5. **Answer Queries**: Use map to answer nums1 queries efficiently

## Complexity Analysis

### Time Complexity: **O(n + m)**
- **O(m)** for processing nums2 (m = size of nums2)
- **O(n)** for answering nums1 queries (n = size of nums1)
- Each element pushed and popped from stack at most once

### Space Complexity: **O(m)**
- **O(m)** for the stack and hash map storage
- **O(n)** for output array

## Final Code with Comments

```cpp
class Solution {
public:
    vector<int> nextGreaterElement(vector<int>& nums1, vector<int>& nums2) {
        unordered_map<int, int> map;  // Store element -> next greater element
        stack<int> st;               // Monotonic decreasing stack
        
        // Process nums2 from right to left
        for(int i = nums2.size() - 1; i >= 0; i--) {
            // Pop elements from stack that are smaller than current element
            // This maintains a decreasing order in the stack
            while(!st.empty() && st.top() <= nums2[i]) {
                st.pop();
            }
            
            // The next greater element is stack top if stack not empty, else -1
            map[nums2[i]] = st.empty() ? -1 : st.top();
            
            // Push current element to stack
            st.push(nums2[i]);
        }
        
        // Build result for nums1 using the precomputed map
        vector<int> res;
        for(int num : nums1) {
            res.push_back(map[num]);
        }
        return res;
    }
};
