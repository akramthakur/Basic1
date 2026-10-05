# Minimum Platforms Required - Solution

## Problem Statement
Given arrival and departure times of all trains that reach a railway station, find the minimum number of platforms required for the railway station so that no train is kept waiting.

## Step-by-Step Logic

### Algorithm:
1. **Sort Both Arrays**: Sort arrival and departure times separately
2. **Two Pointer Approach**: Use two pointers to simulate the timeline
3. **Count Concurrent Trains**: When a train arrives, increment platform count; when a train departs, decrement platform count
4. **Track Maximum**: Keep track of the maximum platforms needed at any time

### Key Insight:
- The maximum number of trains that overlap at any time gives the minimum platforms needed
- By processing events in chronological order, we can simulate the station's occupancy

## Complexity Analysis

### Time Complexity: **O(n log n)**
- Sorting both arrays: O(n log n)
- Single pass with two pointers: O(n)

### Space Complexity: **O(1)**
- Only a few integer variables used
- Sorting may use O(log n) stack space

## Final Code with Comments

```cpp
class Solution {
  public:
    int minPlatform(vector<int>& arr, vector<int>& dep) {
        int n = arr.size();
        
        // Sort arrival and departure times
        sort(arr.begin(), arr.end());
        sort(dep.begin(), dep.end());
        
        int i = 0, j = 0;      // Pointers for arrival and departure
        int platform = 0;       // Current platforms in use
        int maxi = 0;           // Maximum platforms needed
        
        // Process all arrival and departure events
        while (i < n && j < n) {
            if (arr[i] <= dep[j]) {
                // Train arrives - need a platform
                platform++;
                maxi = max(maxi, platform);
                i++;
            } else {
                // Train departs - free a platform
                platform--;
                j++;
            }
        }
        
        return maxi;
    }
};
