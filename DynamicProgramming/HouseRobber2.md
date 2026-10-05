# House Robber II - Solution

## Problem Statement
You are a professional robber planning to rob houses along a street arranged in a circle. This means the first house is the neighbor of the last house. The constraint remains the same: adjacent houses have security systems and cannot be robbed on the same night.

Given an integer array `nums` representing the amount of money at each house, return the maximum amount of money you can rob tonight without alerting the police.

## Step-by-Step Logic

### Algorithm:
1. **Circular Constraint Handling**: Since first and last houses are adjacent, we cannot rob both
2. **Two Scenarios Approach**:
   - Scenario 1: Rob houses from 0 to n-2 (exclude last house)
   - Scenario 2: Rob houses from 1 to n-1 (exclude first house)
3. **Dynamic Programming**: Apply original House Robber logic to both scenarios
4. **Final Decision**: Take maximum of both scenarios

### Key Insight:
- In circular arrangement, the problem reduces to two linear problems
- We solve the original House Robber problem on two different ranges
- The maximum of both solutions gives the optimal answer

## Complexity Analysis

### Time Complexity: **O(n)**
- Two linear passes through the array
- Each pass takes O(n) time

### Space Complexity: **O(n)**
- DP arrays for both scenarios
- Can be optimized to O(1) with variables

## Final Code with Comments

```cpp
class Solution {
public:
    int rob(vector<int>& nums) {
        int n = nums.size();
        
        // Handle edge cases
        if (n == 0) return 0;
        if (n == 1) return nums[0];
        if (n == 2) return max(nums[0], nums[1]);
        
        // Scenario 1: Rob houses 0 to n-2 (exclude last house)
        int scenario1 = robLinear(nums, 0, n - 2);
        
        // Scenario 2: Rob houses 1 to n-1 (exclude first house)
        int scenario2 = robLinear(nums, 1, n - 1);
        
        // Return maximum of both scenarios
        return max(scenario1, scenario2);
    }

private:
    // Helper function to solve linear House Robber problem
    int robLinear(vector<int>& nums, int start, int end) {
        int n = end - start + 1;
        
        // Handle base cases for the range
        if (n == 1) return nums[start];
        if (n == 2) return max(nums[start], nums[start + 1]);
        
        // DP array for current range
        vector<int> dp(n, -1);
        
        // Base cases for DP
        dp[0] = nums[start];  // Only first house in range
        dp[1] = max(nums[start], nums[start + 1]);  // Two houses in range
        
        // Fill DP table for the range
        for (int i = 2; i < n; i++) {
            // Choice 1: Skip current house (take dp[i-1])
            // Choice 2: Rob current house + take dp[i-2] (non-adjacent)
            dp[i] = max(dp[i - 1], dp[i - 2] + nums[start + i]);
        }
        
        return dp[n - 1];
    }
};
