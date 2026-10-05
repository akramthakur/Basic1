# Coin Change (Greedy) - Solution

## Problem Statement
Given an array of coin denominations and a target amount, find the minimum number of coins needed to make that amount. Return -1 if it's not possible.

## Important Note
**This greedy approach only works for specific coin systems** (like US currency). For arbitrary coin denominations, this may not give the optimal solution.

## Step-by-Step Logic

### Algorithm:
1. **Sort Coins**: Sort coins in descending order
2. **Greedy Selection**: Always use the largest possible coin
3. **Update Amount**: Subtract the coin value and count how many times it's used
4. **Check Completion**: If amount becomes 0, return count; else return -1

### Key Insight:
- For canonical coin systems, using the largest possible coin first leads to optimal solution
- For non-canonical systems, this approach may fail

## Complexity Analysis

### Time Complexity: **O(n log n + amount)**
- Sorting: O(n log n)
- Single pass through coins: O(n)

### Space Complexity: **O(1)**
- Only a few integer variables used

## Final Code with Comments

```cpp
class Solution {
public:
    int coinChange(vector<int>& coins, int amount) {
        int ans = 0;
        // Sort coins in descending order to use largest coins first
        sort(coins.begin(), coins.end(), greater<int>());
        
        for (int i = 0; i < coins.size(); i++) {
            if (amount >= coins[i]) {
                // Use as many of this coin as possible
                ans += amount / coins[i];
                amount = amount % coins[i];
            }
        }
        
        // Return count if amount is exactly 0, else -1
        return (amount == 0) ? ans : -1;
    }
};
