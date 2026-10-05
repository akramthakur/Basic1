# Coin Change II - Solution

## Problem Statement
Given an array of distinct coin denominations and a target amount, return the **number of combinations** that make up that amount. If it's impossible to make the amount, return 0.

**Note**: The order of coins does not matter (1+2 and 2+1 count as the same combination).

## Step-by-Step Logic

### Algorithm:
1. **Dynamic Programming**: Use bottom-up approach to count combinations
2. **State Definition**: `dp[i]` = number of combinations to make amount `i`
3. **Recurrence Relation**: 
   - Process coins one by one to avoid counting permutations
   - For each coin `c`, update amounts from `c` to `amount`: `dp[i] += dp[i-c]`
4. **Base Case**: `dp[0] = 1` (1 way to make amount 0 - use no coins)

### Key Insight:
- This is an **unbounded knapsack** counting problem
- Process coins **outer loop**, amounts **inner loop** to avoid counting permutations
- If we process amounts outer loop and coins inner loop, we'd count permutations (1+2 and 2+1 as different)

## Complexity Analysis

### Time Complexity: **O(amount × n)**
- Outer loop: O(n) for each coin
- Inner loop: O(amount) for amounts from coin value to target

### Space Complexity: **O(amount)**
- DP array of size amount+1

## Final Code with Comments

```cpp
class Solution {
public:
    int change(int amount, vector<int>& coins) {
        // DP array: dp[i] = number of combinations to make amount i
        vector<unsigned long long> dp(amount + 1, 0);
        
        // Base case: 1 way to make amount 0 (use no coins)
        dp[0] = 1;
        
        // Process each coin one by one
        for (int c : coins) {
            // For current coin, update all amounts from c to amount
            for (int i = c; i <= amount; i++) {
                // Add combinations using current coin
                dp[i] = (dp[i] + dp[i - c]);
            }
        }
        
        return (int)(dp[amount]);
    }
};
