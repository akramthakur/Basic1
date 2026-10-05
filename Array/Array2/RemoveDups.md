# Remove Duplicates from Sorted Array - Solution

## Problem Statement
Given a sorted array nums, remove the duplicates in-place such that each element appears only once and return the new length.

## Step-by-Step Logic

1. **Two Pointer Approach**:
   - `ans` pointer tracks the position for next unique element
   - `i` pointer iterates through the array

2. **Unique Element Detection**:
   - Compare current element with previous element
   - If different, it's a new unique element
   - Place it at `ans` position and increment `ans`

3. **In-place Modification**:
   - Overwrite duplicates while maintaining order
   - Return count of unique elements

## Complexity Analysis

### Time Complexity: **O(n)**
- Single pass through the array: O(n)
- Each element checked exactly once

### Space Complexity: **O(1)**
- In-place modification, no extra data structures
- Only using constant space for pointers

## Final Code with Comments

```cpp
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        // Handle empty array case
        if(nums.size() == 0) return 0;
        
        int ans = 1;  // First element is always unique
        
        // Start from second element
        for(int i = 1; i < nums.size(); i++){
            // If current element is different from previous
            if(nums[i] != nums[i-1]){
                // Place unique element at ans position
                nums[ans] = nums[i];
                ans++;  // Move to next position
            }
        }
        return ans;  // Return count of unique elements
    }
};
