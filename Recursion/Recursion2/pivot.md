# Find Pivot Index - Solution

## Problem Statement
Given an array of integers, find the pivot index where the sum of all elements to the left equals the sum of all elements to the right. Return -1 if no such index exists.

## Step-by-Step Logic

1. **Calculate Total Sum**:
   - Precompute sum of all elements in the array
   - This gives the initial total for right sum calculation

2. **Recursive Search**:
   - Track left sum as we iterate through array
   - Calculate right sum = total - left sum - current element
   - Check if left sum equals right sum at each position

3. **Early Termination**:
   - Return pivot index immediately when found
   - Return -1 if no pivot exists after full traversal

## Complexity Analysis

### Time Complexity: **O(n)**
- One pass to calculate total sum: O(n)
- One recursive pass to find pivot: O(n)
- Total: O(2n) = O(n)

### Space Complexity: **O(n)**
- Recursion stack depth equals array size
- Each recursive call uses stack space

## Final Code with Comments

```cpp
class Solution {
public:
    int helper(vector<int>& nums, int i, int totalsum, int leftsum) {
        // Base case: reached end of array, no pivot found
        if(i == nums.size()) return -1;

        // Calculate right sum for current index
        int rightsum = totalsum - leftsum - nums[i];
        
        // Check if current index is pivot
        if(rightsum == leftsum) {
            return i;  // Found pivot index
        }
        
        // Recursive call: move to next index, update left sum
        return helper(nums, i + 1, totalsum, leftsum + nums[i]);
    }
    
    int pivotIndex(vector<int>& nums) {
        int n = nums.size();
        int total = 0;
        
        // Calculate total sum of array
        for(int i = 0; i < n; i++) {
            total += nums[i];
        }
        
        // Start recursive search from index 0
        int ans = helper(nums, 0, total, 0);
        return ans;
    }
};
