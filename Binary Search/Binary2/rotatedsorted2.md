# Search in Rotated Sorted Array II - Solution

## Problem Statement
Given a sorted array that has been rotated at an unknown pivot and may contain **duplicates**, search for a target value in O(log n) time on average. Return true if target exists, otherwise false.

## Step-by-Step Logic

1. **Modified Binary Search with Duplicate Handling**:
   - Similar to rotated array search, but handles duplicates
   - Additional check when `nums[lo] == nums[mid] == nums[hi]`

2. **Duplicate Handling**:
   - When all three points are equal, we cannot determine which side is sorted
   - Increment `lo` and decrement `hi` to skip duplicates
   - This maintains O(log n) average case, O(n) worst case

3. **Standard Rotated Search**:
   - If left half `[lo, mid]` is sorted: check if target in range
   - If right half `[mid, hi]` is sorted: check if target in range

## Complexity Analysis

### Time Complexity: **O(log n) average, O(n) worst case**
- **Average**: Binary search with occasional duplicate skips
- **Worst**: All elements equal except target (linear scan)
- Each duplicate skip reduces search space

### Space Complexity: **O(1)**
- Only constant extra space for pointers
- In-place operations

## Final Code with Comments

```cpp
class Solution {
public:
    bool search(vector<int>& nums, int target) {
        int hi = nums.size() - 1;
        int lo = 0;

        while(lo <= hi) {
            int mid = lo + (hi - lo) / 2;

            // Target found
            if(nums[mid] == target) {
                return true;
            }

            // Handle duplicates: cannot determine sorted half
            if (nums[lo] == nums[mid] && nums[mid] == nums[hi]) {
                lo++;
                hi--;
            }
            // Left half [lo, mid] is sorted
            else if(nums[lo] <= nums[mid]) {
                // Check if target is in sorted left half
                if(target >= nums[lo] && target < nums[mid]) {
                    hi = mid - 1;  // Search left
                } else {
                    lo = mid + 1;  // Search right
                }
            }
            // Right half [mid, hi] is sorted
            else {
                // Check if target is in sorted right half
                if(target > nums[mid] && target <= nums[hi]) {
                    lo = mid + 1;  // Search right
                } else {
                    hi = mid - 1;  // Search left
                }
            }
        }
        return false;  // Target not found
    }
};
