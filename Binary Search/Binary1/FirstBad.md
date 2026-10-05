# First Bad Version - Solution

## Problem Statement
You have `n` versions [1, 2, ..., n] and you want to find the first bad one, which causes all the following ones to be bad. You are given an API `bool isBadVersion(version)` which returns whether `version` is bad. Implement a function to find the first bad version efficiently.

## Step-by-Step Logic

1. **Binary Search Approach**:
   - Use two pointers: `lo` (start) and `hi` (end)
   - Calculate middle version: `mid = lo + (hi - lo) / 2`
   - Check if middle version is bad using the API

2. **Decision Making**:
   - If `mid` is **not bad**: First bad version must be after `mid`
   - If `mid` is **bad**: First bad version is `mid` or before `mid`

3. **Convergence**:
   - Continue until `lo` and `hi` meet
   - Both will point to the first bad version

## Complexity Analysis

### Time Complexity: **O(log n)**
- Binary search halves the search space each iteration
- Maximum of log₂(n) API calls

### Space Complexity: **O(1)**
- Only constant extra space for pointers
- No recursion or additional data structures

## Final Code with Comments

```cpp
// The API isBadVersion is defined for you.
// bool isBadVersion(int version);

class Solution {
public:
    int firstBadVersion(int n) {
        int lo = 1;
        int hi = n;
        int mid;
        
        while(lo < hi) {
            // Calculate mid without overflow
            mid = lo + (hi - lo) / 2;
            
            if(isBadVersion(mid) == false) {
                // Mid is good, so first bad version is after mid
                lo = mid + 1;
            } else {
                // Mid is bad, so first bad version is mid or before mid
                hi = mid;
            }
        }
        
        // When loop ends, lo == hi and both point to first bad version
        return lo;
    }
};
