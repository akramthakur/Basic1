# Can Place Flowers - Solution

## Problem Statement
You have a long flowerbed in which some plots are planted and some are not. However, flowers cannot be planted in adjacent plots.

Given an integer array `flowerbed` containing 0's and 1's, where 0 means empty and 1 means not empty, and an integer `n`, return `true` if `n` new flowers can be planted in the flowerbed without violating the no-adjacent-flowers rule.

## Step-by-Step Logic

### Algorithm:
1. **Track Empty Segments**: Find consecutive empty plots between planted flowers
2. **Calculate Capacity**: For each segment of consecutive zeros, calculate how many flowers can be planted
3. **Edge Cases**: Handle segments at the beginning and end specially

### Key Insight:
- Between two planted flowers (1's), we can plant `(zeros - 1) / 2` flowers
- At the beginning (before first 1), we can plant `zeros / 2` flowers  
- At the end (after last 1), we can plant `zeros / 2` flowers

## Complexity Analysis

### Time Complexity: **O(n)**
- Single pass through the flowerbed array
- Constant time operations per element

### Space Complexity: **O(1)**
- Only a few integer variables used

## Final Code with Comments

```cpp
class Solution {
public:
    bool canPlaceFlowers(vector<int>& flowerbed, int n) {
        int ans = 0;      // Count of flowers we can plant
        int l = -1;       // Index of last planted flower (-1 if none yet)
        
        for (int i = 0; i < flowerbed.size(); i++) {
            if (flowerbed[i] == 1) {
                // Found a planted flower
                int zeros = i - l - 1;  // Consecutive zeros between current and last planted
                
                if (l == -1) {
                    // Segment from start to first planted flower
                    ans += zeros / 2;
                } else {
                    // Segment between two planted flowers
                    ans += (zeros - 1) / 2;
                }
                
                l = i;  // Update last planted position
            }
        }
        
        // Handle the segment after the last planted flower
        if (l == -1) {
            // No flowers planted at all
            ans += (flowerbed.size() + 1) / 2;
        } else {
            // Segment from last planted to end
            ans += (flowerbed.size() - l - 1) / 2;
        }
        
        return ans >= n;
    }
};
