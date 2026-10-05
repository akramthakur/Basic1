# Trapping Rain Water - Solution

## Problem Statement
Given `n` non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it can trap after raining.

## Step-by-Step Logic

### Dynamic Programming Approach (Precomputation):
1. **Left Maximum Array**: For each position, store the maximum height to the left
2. **Right Maximum Array**: For each position, store the maximum height to the right  
3. **Water Calculation**: For each position, water trapped = min(leftMax, rightMax) - current height
4. **Summation**: Accumulate water from all positions

## Complexity Analysis

### Time Complexity: **O(n)**
- **O(n)** for left maximum array computation
- **O(n)** for right maximum array computation  
- **O(n)** for water calculation pass
- **n** = number of elements in array

### Space Complexity: **O(n)**
- **O(n)** for left maximum array storage
- **O(n)** for right maximum array storage
- Can be optimized to **O(1)** with two-pointer approach

## Final Code with Comments

```cpp
class Solution {
public:
    int trap(vector<int>& arr) {
        int n = arr.size();
        // Edge case: if array has less than 3 elements, no water can be trapped
        if(n < 3) return 0;
        
        int res = 0;
        
        // Arrays to store maximum height to left and right of each position
        int lmax[n], rmax[n];
        
        // Compute left maximum for each position
        lmax[0] = arr[0];
        for(int i = 1; i < n; i++) {
            lmax[i] = max(arr[i], lmax[i-1]);
        }
        
        // Compute right maximum for each position
        rmax[n-1] = arr[n-1];
        for(int i = n-2; i >= 0; i--) {
            rmax[i] = max(arr[i], rmax[i+1]);
        }
        
        // Calculate trapped water for each position
        // Skip first and last positions as they can't trap water
        for(int i = 1; i < n-1; i++) {
            // Water level is determined by minimum of left and right max
            // Subtract current height to get trapped water
            res = res + (min(lmax[i], rmax[i]) - arr[i]);
        }
        
        return res;
    }
};
