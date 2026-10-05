# Aggressive Cows - Solution

## Problem Statement
Given an array of stall positions and `k` cows, place the cows in stalls such that the minimum distance between any two cows is maximized.

## Step-by-Step Logic

### Binary Search on Answer Approach:
1. **Sort Stalls**: Arrange stall positions in ascending order
2. **Binary Search Range**: 
   - `start` = 1 (minimum possible distance)
   - `end` = max(stalls) - min(stalls) (maximum possible distance)
3. **Feasibility Check**: For each mid distance, check if we can place all cows
4. **Greedy Placement**: Place cows while maintaining minimum distance
5. **Maximize Distance**: Binary search to find maximum feasible distance

## Complexity Analysis

### Time Complexity: **O(n log n + n log d)**
- **O(n log n)** for sorting stalls
- **O(n log d)** for binary search with feasibility checks
- **n** = number of stalls, **d** = max distance between stalls

### Space Complexity: **O(1)**
- **O(1)** - only using constant extra space for variables
- In-place sorting and operations

## Final Code with Comments

```cpp
class Solution {
public:
    // Helper function to check if we can place k cows with minimum distance 'dis'
    bool canplace(vector<int>& stalls, int dis, int numCows) {
        int cnt = 1; // Place first cow at first stall
        int last = stalls[0]; // Position of last placed cow
        
        for(int i = 1; i < stalls.size(); i++) {
            // If current stall is at least 'dis' away from last placed cow
            if(stalls[i] - last >= dis) {
                cnt += 1; // Place cow here
                last = stalls[i]; // Update last position
            }
        }
        // Return true if we placed at least numCows cows
        return cnt >= numCows;
    }
    
    int aggressiveCows(vector<int> &stalls, int k) {
        // Sort stalls to enable greedy placement
        sort(stalls.begin(), stalls.end());
        
        // Binary search range for minimum distance
        int start = 1; // Minimum possible distance
        int end = stalls[stalls.size()-1] - stalls[0]; // Maximum possible distance
        int res = 1; // Store result
        
        while(start <= end) {
            int mid = start + (end - start) / 2; // Current distance to try
            
            if(canplace(stalls, mid, k)) {
                // If we can place cows with this distance, try larger distance
                res = mid;
                start = mid + 1;
            } else {
                // If we cannot place cows, try smaller distance
                end = mid - 1;
            }
        }
        return res;
    }
};
