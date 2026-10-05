# Sort Colors - Solution

## Problem Statement
Given an array `nums` with n objects colored red, white, or blue, sort them in-place so that objects of the same color are adjacent, with the colors in the order red (0), white (1), and blue (2).

## Step-by-Step Logic

1. **Counting Approach**:
   - First pass: Count occurrences of 0s and 1s
   - Second pass: Overwrite array with 0s, then 1s, then 2s
   - Use counters to track remaining elements to place

2. **Three-Phase Overwrite**:
   - Fill beginning with all 0s (red)
   - Fill middle with all 1s (white)
   - Fill remaining with all 2s (blue)

## Complexity Analysis

### Time Complexity: **O(n)**
- First pass to count 0s and 1s: O(n)
- Second pass to overwrite array: O(n)
- Total: O(2n) = O(n)

### Space Complexity: **O(1)**
- Only using constant extra space for counters
- In-place modification of input array

## Final Code with Comments

```cpp
class Solution {
public:
    void sortColors(vector<int>& nums) {
        int cnt1 = 0, cnt0 = 0;
        
        // First pass: count 0s and 1s
        for(int i = 0; i < nums.size(); i++) {
            if(nums[i] == 0) {
                cnt0++;
            } else if(nums[i] == 1) {
                cnt1++;
            }
        }
        
        int i = 0;
        // Fill with 0s
        while(cnt0 > 0) {
            nums[i] = 0;
            i++;
            cnt0--;
        }
        
        // Fill with 1s
        while(cnt1 > 0) {
            nums[i] = 1;
            i++;
            cnt1--;
        }
        
        // Fill remaining with 2s
        while(i < nums.size()) {
            nums[i] = 2;
            i++;
        }
    }
};
