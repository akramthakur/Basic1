# Coin Change - Solution

## Problem Statement
Given an array of coin denominations and a target amount, find the **minimum number of coins** needed to make that amount. If it's impossible to make the amount using the given coins, return -1.

## Step-by-Step Logic

### Algorithm:
1. **Dynamic Programming**: Use bottom-up approach to compute minimum coins
2. **State Definition**: `dp[i]` = minimum coins needed to make amount `i`
3. **Recurrence Relation**: 
   - For each amount `i`, try all coins `c` where `c <= i`
   - `dp[i] = min(dp[i], dp[i-c] + 1)` for all valid coins
4. **Base Case**: `dp[0] = 0` (0 coins needed to make amount 0)

### Key Insight:
- This is an **unbounded knapsack** problem (can use each coin multiple times)
- We want to minimize the count, not just check feasibility
- Initialize with a large value to represent "impossible"

## Complexity Analysis

### Time Complexity: **O(amount × n)**
- Outer loop: O(amount) for amounts 1 to amount
- Inner loop: O(n) for iterating through coins

### Space Complexity: **O(amount)**
- DP array of size amount+1

## Final Code with Comments

```cpp
class Solution {
public:
    int coinChange(vector<int>& coins, int amount) {
        // Sort coins (optional optimization for early termination)
        sort(coins.begin(), coins.end());
        
        // DP array: dp[i] = min coins to make amount i
        vector<int> dp(amount + 1, 1e9);  // Initialize with large value
        
        // Base case: 0 coins needed for amount 0
        dp[0] = 0;
        
        // Fill DP table for all amounts from 1 to amount
        for (int i = 1; i <= amount; i++) {
            // Try each coin that doesn't exceed current amount
            for (int c : coins) {
                if (i - c >= 0) {
                    dp[i] = min(dp[i], dp[i - c] + 1);
                }
            }
        }
        
        // Return result or -1 if amount is impossible
        return (dp[amount] == 1e9) ? -1 : dp[amount];
    }
};
