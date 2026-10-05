# Two Sum - Solution

## Problem Statement
Given an array of integers `nums` and an integer `target`, return indices of the two numbers such that they add up to `target`. You may assume that each input would have exactly one solution, and you may not use the same element twice.

## Step-by-Step Logic

1. **Brute Force Approach**:
   - Check every possible pair of elements in the array
   - For each element at index `j`, check with all elements at indices `k > j`
   - If sum equals target, return the indices

2. **Nested Loop**:
   - Outer loop: iterate through each element as first number
   - Inner loop: iterate through remaining elements as second number
   - Check if their sum equals target

## Complexity Analysis

### Time Complexity: **O(n²)**
- Outer loop runs n times
- Inner loop runs (n-1), (n-2), ..., 1 times
- Total comparisons: n(n-1)/2 = O(n²)

### Space Complexity: **O(1)**
- Only using constant extra space for variables
- Output vector of size 2 is not counted in space complexity

## Final Code with Comments

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        int i = nums.size();
        vector<int> res;
        
        // Check all possible pairs
        for(int j = 0; j < i; j++) {
            for(int k = j + 1; k < i; k++) {
                // If pair sum equals target, store indices
                if(target == nums[j] + nums[k]) {
                    res.push_back(j);
                    res.push_back(k);
                    return res;  // Early return since exactly one solution
                }
            }
        }
        return res;
    }
};
