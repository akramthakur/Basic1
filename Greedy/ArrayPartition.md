# Array Partition - Solution

## Problem Statement
Given an integer array `nums` of 2n integers, group these integers into n pairs such that the sum of `min(a_i, b_i)` for all pairs is maximized. Return the maximized sum.

## Step-by-Step Logic

### Algorithm:
1. **Sorting**: Sort the array in ascending order
2. **Pair Adjacent Elements**: Group consecutive elements into pairs (0-1, 2-3, 4-5, ...)
3. **Sum Minimums**: Add up the first element of each pair (which will be the minimum)

### Key Insight:
- To maximize the sum of minimums, we want to minimize the "loss" from larger numbers
- By pairing smallest with second smallest, third smallest with fourth smallest, etc., we ensure we don't "waste" large numbers
- The minimum of each pair will always be the smaller (left) element after sorting

## Complexity Analysis

### Time Complexity: **O(n log n)**
- Dominated by sorting the array
- Linear pass through half the elements

### Space Complexity: **O(1)**
- Sorting may use O(log n) stack space
- No additional data structures used

## Final Code with Comments

```cpp
class Solution {
public:
    int arrayPairSum(vector<int>& nums) {
        // Sort the array to pair smallest with second smallest, etc.
        sort(nums.begin(), nums.end());
        
        int sum = 0;
        // Take every first element of each pair (indices 0, 2, 4, ...)
        for (int i = 0; i < nums.size(); i += 2) {
            sum += nums[i];
        }
        
        return sum;
    }
};
