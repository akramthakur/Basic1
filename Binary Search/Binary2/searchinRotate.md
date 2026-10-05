# Search in Rotated Sorted Array - Solution

## Problem Statement
Given a sorted array that has been rotated at an unknown pivot, search for a target value in O(log n) time.Return the index of target if found, otherwise return -1.

## Step-by-Step Logic

1. **Modified Binary Search**:
   - Regular binary search won't work due to rotation
   - Need to determine which half is properly sorted
   - Then check if target lies within the sorted half

2. **Identify Sorted Half**:
   - If `nums[lo] <= nums[mid]`: left half is sorted
   - Else: right half is sorted

3. **Target Search**:
   - If left half sorted: check if target in `[nums[lo], nums[mid])`
   - If right half sorted: check if target in `(nums[mid], nums[hi]]`
   - Adjust search range accordingly

## Complexity Analysis

### Time Complexity: **O(log n)**
- Binary search approach
- Each iteration halves the search space

### Space Complexity: **O(1)**
- Only constant extra space for pointers
- In-place operations

## Final Code with Comments

```cpp
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int hi = nums.size() - 1;
        int lo = 0;
        
        while(lo <= hi) {
            int mid = lo + (hi - lo) / 2;  // Prevent overflow
            
            // Target found
            if(nums[mid] == target) {
                return mid;
            }
            
            // Check if left half [lo, mid] is sorted
            else if(nums[lo] <= nums[mid]) {
                // Check if target is in sorted left half
                if(target >= nums[lo] && target < nums[mid]) {
                    hi = mid - 1;  // Search left half
                } else {
                    lo = mid + 1;  // Search right half
                }
            }
            
            // Otherwise right half [mid, hi] is sorted
            else {
                // Check if target is in sorted right half
                if(target > nums[mid] && target <= nums[hi]) {
                    lo = mid + 1;  // Search right half
                } else {
                    hi = mid - 1;  // Search left half
                }
            }
        }
        return -1;  // Target not found
    }
};
