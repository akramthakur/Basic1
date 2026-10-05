# Two Sum - Solution

## Problem Statement
Given an array of integers `nums` and an integer `target`, return indices of the two numbers such that they add up to `target`. You may assume that each input would have exactly one solution, and you may not use the same element twice.

## Step-by-Step Logic

### Two-Pass Hash Map Approach:
1. **First Pass**: Store each element and its index in hash map
2. **Second Pass**: For each element, check if complement exists in map
3. **Index Validation**: Ensure we don't use the same element twice

## Complexity Analysis

### Time Complexity: **O(n)**
- First pass: O(n) to build hash map
- Second pass: O(n) to find complement
- Hash map operations: O(1) average case

### Space Complexity: **O(n)**
- Hash map stores n elements
- Output vector of size 2

## Final Code with Comments

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> map;
        int n = nums.size();

        // First pass: store all elements with their indices
        for(int i = 0; i < n; i++) {
            map[nums[i]] = i;
        }

        // Second pass: find complement for each element
        for(int i = 0; i < n; i++) {
            int comp = target - nums[i];
            
            // Check if complement exists and it's not the same element
            if(map.count(comp) && map[comp] != i) {
                return {i, map[comp]};
            }
        }
        
        return {};  // No solution found (though problem guarantees one exists)
    }
};
