# Climbing Stairs - Solution

## Problem Statement
You are climbing a staircase. It takes `n` steps to reach the top. Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

## Step-by-Step Logic

### Dynamic Programming Approach:
1. **Base Cases**:
   - `0 steps`: 0 ways
   - `1 step`: 1 way (climb 1 step)
   - `2 steps`: 2 ways (1+1 or 2)
2. **Recurrence Relation**: `ways(n) = ways(n-1) + ways(n-2)`
   - Reach step `n` from step `n-1` (1 step) OR from step `n-2` (2 steps)
3. **Bottom-up Computation**: Fill DP array from smallest to largest subproblems

## Complexity Analysis

### Time Complexity: **O(n)**
- **O(n)** for single pass through 3 to n
- **O(1)** operations per iteration

### Space Complexity: **O(n)**
- **O(n)** for DP array storage
- Can be optimized to **O(1)** by storing only last two values

## Final Code with Comments

```cpp
class Solution {
public:
    int climbStairs(int n) {
        // Handle small cases directly
        if(n < 3)  
            return n;
        
        // DP array to store number of ways for each step
        vector<int> dp(n + 1);
        
        // Initialize base cases
        dp[0] = 0;  // 0 steps - 0 ways
        dp[1] = 1;  // 1 step - 1 way (climb 1)
        dp[2] = 2;  // 2 steps - 2 ways (1+1 or 2)
        
        // Fill DP array using recurrence relation
        for(int i = 3; i <= n; i++) {
            dp[i] = dp[i - 1] + dp[i - 2];
        }
        
        return dp[n];
    }
};
