# Container With Most Water - Solution

## Problem Statement
Given an array of non-negative integers `height` where each integer represents the height of a vertical line, find two lines that together with the x-axis form a container that holds the maximum amount of water.

## Step-by-Step Logic

1. **Two Pointer Approach**:
   - Start with widest container (left=0, right=n-1)
   - Calculate area using formula: `min(height[left], height[right]) * (right - left)`
   - Move the pointer pointing to the shorter line inward

2. **Key Insight**:
   - The area is limited by the shorter line
   - Moving the shorter pointer might find a taller line
   - Moving the taller pointer would never increase the area

3. **Greedy Strategy**:
   - Always move the pointer with smaller height
   - Track maximum area encountered

## Complexity Analysis

### Time Complexity: **O(n)**
- Single pass through the array with two pointers
- Each element visited at most once

### Space Complexity: **O(1)**
- Only constant extra space for pointers and variables
- No additional data structures

## Final Code with Comments

```cpp
class Solution {
public:
    // Helper function to calculate area between two lines
    int area(int l, int r, vector<int>& height) {
        return min(height[l], height[r]) * abs(l - r);
    }
    
    int maxArea(vector<int>& height) {
        int l = 0;                      // Left pointer
        int r = height.size() - 1;      // Right pointer
        int ar = INT_MIN;               // Track maximum area
        
        while(l < r) {
            // Calculate current area and update maximum
            ar = max(ar, area(l, r, height));
            
            // Move the pointer with smaller height
            if(height[l] > height[r])
                r--;
            else
                l++;
        }
        return ar;
    }
};
