# Counting Bits - Solution

## Problem Statement
Given an integer `n`, return an array `ans` of length `n + 1` such that for each `i` (0 ≤ i ≤ n), `ans[i]` is the number of 1's in the binary representation of `i`.

## Step-by-Step Logic

### Algorithm:
1. **Dynamic Programming**: Use previously computed results
2. **Bit Pattern Observation**: 
   - Number of 1's in `i` = number of 1's in `i/2` + least significant bit
   - `i >> 1` = `i/2` (right shift removes LSB)
   - `i & 1` = LSB (0 if even, 1 if odd)

### Key Insight:
- **Even numbers**: `i` and `i/2` have same number of 1's
- **Odd numbers**: `i` has one more '1' than `i/2`

## Complexity Analysis

### Time Complexity: **O(n)**
- Single pass through 0 to n
- Constant time operation per number

### Space Complexity: **O(n)**
- DP array of size n+1
- Output array of size n+1

## Final Code with Comments

```cpp
class Solution {
public:
    vector<int> countBits(int n) {
        vector<int> dp(n + 1, 0);  // DP array to store count of 1's
        vector<int> ans;           // Result array
        
        for (int i = 0; i <= n; i++) {
            // Recurrence relation:
            // dp[i] = count of 1's in i/2 + least significant bit
            dp[i] = dp[i >> 1] + (i & 1);  
            ans.push_back(dp[i]);
        }
        return ans;
    }
};
