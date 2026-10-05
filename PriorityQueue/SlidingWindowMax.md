# Sliding Window Maximum - Solution

## Problem Statement
Given an array of integers and a window size k, find the maximum element in each sliding window as it moves from left to right.

## Step-by-Step Logic

### Algorithm:
1. **Use Deque**: Maintain indices in decreasing order of their values
2. **Remove Out-of-Window Elements**: Remove elements that are outside current window
3. **Maintain Decreasing Order**: Remove smaller elements from back before adding new element
4. **Get Maximum**: Front of deque always contains maximum of current window

### Key Operations:
- **Deque Operations**: 
  - `pop_front()`: Remove out-of-window elements
  - `pop_back()`: Maintain decreasing order
  - `push_back()`: Add new element
- **Window Tracking**: Use indices to track window boundaries

## Complexity Analysis

### Time Complexity: **O(n)**
- Each element pushed and popped at most once

### Space Complexity: **O(k)**
- Deque stores at most k elements

## Final Code with Comments

```cpp
class Solution {
public:
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        deque<int> dq;  // Stores indices, maintains decreasing order of values
        vector<int> ans;
        
        for(int i = 0; i < nums.size(); i++) {
            // Remove elements that are out of current window
            if(!dq.empty() && dq.front() == i - k)
                dq.pop_front();
            
            // Maintain decreasing order in deque
            // Remove elements smaller than current from back
            while(!dq.empty() && nums[dq.back()] <= nums[i])
                dq.pop_back();
            
            // Add current element at the back
            dq.push_back(i);
            
            // Add to result once we have our first complete window
            if(i >= k - 1) 
                ans.push_back(nums[dq.front()]);
        }
        return ans;
    }
};S
