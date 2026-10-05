# Min Cost Climbing Stairs - Solution

## Problem Statement
Given an integer array `cost` where `cost[i]` is the cost of stepping on the i-th stair, return the minimum cost to reach the top of the floor. You can start from either step 0 or step 1, and you can climb 1 or 2 steps at a time.

## Step-by-Step Logic

### Algorithm:
1. **Dynamic Programming**: Use bottom-up approach to compute minimum cost
2. **State Definition**: `dp[i]` = minimum cost to reach step `i`
3. **Recurrence Relation**: `dp[i] = min(dp[i-1], dp[i-2]) + cost[i]`
4. **Final Answer**: Minimum of last two steps (since we can reach top from either)

### Key Insight:
- At each step, we can come from either 1 step back or 2 steps back
- We want the minimum cost path to reach each step
- The top is beyond the last step, so we can reach it from either last or second-last step

## Complexity Analysis

### Time Complexity: **O(n)**
- Single pass through the cost array
- Constant time operations per step

### Space Complexity: **O(n)**
- DP array of size n
- Can be optimized to O(1) with variables

## Final Code with Comments

```cpp
class Solution {
public:
    int minCostClimbingStairs(vector<int>& cost) {
        int n = cost.size();
        vector<int> dp(n, -1);
        
        // Base cases: cost to reach step 0 and step 1
        dp[0] = cost[0];
        dp[1] = cost[1];
        
        // Fill DP table from step 2 to n-1
        for (int i = 2; i < n; i++) {
            dp[i] = min(dp[i - 1], dp[i - 2]) + cost[i];
        }
        
        // We can reach top from either last or second-last step
        return min(dp[n - 1], dp[n - 2]);
    }
};
