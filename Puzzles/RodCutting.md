# Rod Cutting Problem - Solution

## Problem Statement
Given a rod of length `n` and an array `price[]` where `price[i]` represents the price of a piece of length `i+1`, find the maximum revenue obtainable by cutting the rod and selling the pieces.

## Step-by-Step Logic

### Dynamic Programming Approach:
1. **State Definition**: `dp[i]` = maximum revenue obtainable for rod of length `i`
2. **Base Case**: `dp[0] = 0` (no revenue for zero length)
3. **Recurrence Relation**: 
   - For each length `i`, try all possible first cuts of length `j` (1 to i)
   - `dp[i] = max(dp[i], price[j-1] + dp[i-j])`

## Key Insight
- Each piece of length `j` has price `price[j-1]` (since array is 0-indexed)
- After cutting piece of length `j`, remaining rod length is `i-j`
- Optimal solution uses optimal solutions to subproblems

## Complexity Analysis

### Time Complexity: **O(n²)**
- Outer loop: `n` iterations
- Inner loop: up to `n` iterations
- Total: `n × n = O(n²)`

### Space Complexity: **O(n)**
- DP array of size `n+1`
- No additional data structures

## Final Code with Comments

```cpp
class Solution {
public:
    int cutRod(vector<int> &price) {
        int n = price.size();
        // dp[i] = maximum revenue for rod of length i
        vector<int> dp(n + 1, 0);
        
        // Build DP table from bottom-up
        for(int i = 1; i <= n; i++) {
            // Try all possible first cut positions
            for(int j = 1; j <= i; j++) {
                // Either don't cut (current value) or 
                // cut at length j and add optimal solution for remaining
                dp[i] = max(dp[i], price[j - 1] + dp[i - j]);
            }
        }
        
        return dp[n];
    }
};
