# House Robber - Solution

## Problem Statement
You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed. The only constraint stopping you from robbing every house is that adjacent houses have security systems connected, and they will automatically contact the police if two adjacent houses are broken into on the same night.

Given an integer array `nums` representing the amount of money at each house, return the maximum amount of money you can rob tonight without alerting the police.

## Step-by-Step Logic

### Algorithm:
1. **Dynamic Programming**: Use bottom-up approach to compute maximum loot
2. **State Definition**: `dp[i]` = maximum amount that can be robbed from first `i+1` houses
3. **Recurrence Relation**: At each house, choose between:
   - Rob current house + loot from `i-2` houses
   - Skip current house, take loot from `i-1` houses
4. **Decision**: `dp[i] = max(dp[i-1], dp[i-2] + nums[i])`

### Key Insight:
- At each house, we have two choices: rob it or skip it
- If we rob house `i`, we cannot rob house `i-1`
- If we skip house `i`, we can take the maximum from first `i-1` houses

## Complexity Analysis

### Time Complexity: **O(n)**
- Single pass through the array
- Constant time operations per house

### Space Complexity: **O(n)**
- DP array of size n
- Can be optimized to O(1)

## Final Code with Comments

```cpp
class Solution {
public:
    int rob(vector<int>& nums) {
        int n = nums.size();
        
        // Handle edge cases
        if (n == 0) return 0;
        if (n == 1) return nums[0];
        
        vector<int> dp(n, -1);
        
        // Base cases
        dp[0] = nums[0];  // Only one house - rob it
        dp[1] = max(nums[0], nums[1]);  // Two houses - rob the richer one
        
        // Fill DP table
        for (int i = 2; i < n; i++) {
            // Choice 1: Skip current house (take dp[i-1])
            // Choice 2: Rob current house + take dp[i-2] (non-adjacent)
            dp[i] = max(dp[i - 1], dp[i - 2] + nums[i]);
        }
        
        return dp[n - 1];
    }
};
