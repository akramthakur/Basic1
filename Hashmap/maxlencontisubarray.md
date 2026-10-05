# Maximum Length of Contiguous Subarray with Equal 0s and 1s - Solution

## Problem Statement
Given a binary array `nums`, return the maximum length of a contiguous subarray with an equal number of 0 and 1.

## Step-by-Step Logic

### Count Difference Approach:
1. **Track Counts**: Maintain running counts of zeros and ones
2. **Calculate Difference**: `diff = zero_count - one_count`
3. **Hash Map Storage**: Store first occurrence of each difference
4. **Subarray Detection**: Same difference indicates equal zeros and ones between indices

## Complexity Analysis

### Time Complexity: **O(n)**
- Single pass through the array: O(n)
- Hash map operations: O(1) average case
- Total: O(n)

### Space Complexity: **O(n)**
- Hash map stores up to n difference values
- Worst case: all differences are unique

## Final Code with Comments

```cpp
class Solution {
public:
    int findMaxLength(vector<int>& nums) {
        unordered_map<int, int> map;
        int zero = 0, one = 0, maxlen = 0;
        map[0] = -1;  // Initialize with difference 0 at index -1
        
        for(int i = 0; i < nums.size(); i++) {
            // Update counts
            (nums[i] == 0) ? zero++ : one++;
            
            // Calculate difference between zero and one counts
            int diff = zero - one;
            
            // Check if same difference encountered before
            if(map.count(diff)) {
                // Subarray from map[diff]+1 to i has equal 0s and 1s
                maxlen = max(maxlen, i - map[diff]);
            } else {
                // Store first occurrence of this difference
                map[diff] = i;
            }
        }
        return maxlen;
    }
};
