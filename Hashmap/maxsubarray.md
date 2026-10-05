# Maximum Length Subarray with Equal 0s and 1s - Solution

## Problem Statement
Given a binary array, find the maximum length of a contiguous subarray with an equal number of 0 and 1.

## Step-by-Step Logic

### Prefix Sum with Hash Map:
1. **Convert 0s to -1**: This transformation helps identify equal counts
2. **Track Prefix Sums**: Store first occurrence of each prefix sum
3. **Subarray Detection**: Same prefix sum indicates equal 0s and 1s between indices
4. **Max Length Tracking**: Update maximum length when same prefix sum found

## Complexity Analysis

### Time Complexity: **O(n)**
- Single pass through the array: O(n)
- Hash map operations: O(1) average case
- Total: O(n)

### Space Complexity: **O(n)**
- Hash map stores up to n prefix sums
- Worst case: all prefix sums are unique

## Final Code with Comments

```cpp
class Solution {
public:
    int maxLength(vector<int>& arr) {
        unordered_map<int, int> map;
        map[0] = -1;  // Initialize with sum 0 at index -1
        int pre = 0;   // Prefix sum
        int ans = 0;   // Maximum length
        
        for(int i = 0; i < arr.size(); i++) {
            // Convert 0 to -1 and 1 to +1
            pre += (arr[i] == 0) ? -1 : 1;
            
            // Check if same prefix sum encountered before
            if(map.count(pre)) {
                // Subarray from map[pre]+1 to i has equal 0s and 1s
                ans = max(ans, i - map[pre]);
            } else {
                // Store first occurrence of this prefix sum
                map[pre] = i;
            }
        }
        return ans;
    }
};
