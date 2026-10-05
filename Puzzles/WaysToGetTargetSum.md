# Target Sum - Solution

## Problem Statement
You are given an integer array `nums` and an integer `target`. You want to build an expression out of nums by adding either '+' or '-' before each integer in nums and then concatenate all the integers.

Return the number of different expressions that can be built, which evaluates to `target`.

## Step-by-Step Logic

### Algorithm:
1. **DFS with Memoization**: Explore all possible +/- assignments
2. **State Definition**: `dp[i][sum]` = number of ways to reach `sum` using first `i` elements
3. **Recurrence Relation**: 
   - At each number, we have two choices: add (+) or subtract (-)
   - `ways = rec(sum + nums[i]) + rec(sum - nums[i])`
4. **Offset Handling**: Since sum can be negative, shift all sums by `total` to make indices positive

### Key Insight:
- This is essentially a partition problem: find subsets with `(sum_positive - sum_negative) = target`
- The sum range is from `-total` to `+total`, so we need array size `2 * total + 1`
- Memoization is crucial to avoid exponential time complexity

## Complexity Analysis

### Time Complexity: **O(n × total)**
- n = number of elements, total = sum of all elements
- Each state (i, sum) is computed once

### Space Complexity: **O(n × total)**
- DP table of size n × (2 × total + 1)
- Recursion stack depth: O(n)

## Final Code with Comments

```cpp
class Solution {
public:
    vector<vector<int>> dp;
    int total;
    
    int rec(vector<int>& nums, int target, int sum, int i) {
        // Base case: processed all numbers
        if (i == nums.size()) {
            return target == sum ? 1 : 0;
        }
        
        // Return cached result if available (using offset sum+total)
        if (dp[i][sum + total] != -1) {
            return dp[i][sum + total];
        }
        
        // Two choices: add current number or subtract it
        int add = rec(nums, target, sum + nums[i], i + 1);
        int sub = rec(nums, target, sum - nums[i], i + 1);
        
        return dp[i][sum + total] = add + sub;
    }
    
    int findTargetSumWays(vector<int>& nums, int target) {
        // Calculate total sum for array size
        total = accumulate(nums.begin(), nums.end(), 0);
        
        // Initialize DP table: [index][sum + total] 
        // sum ranges from -total to +total, so size = 2*total + 1
        dp.resize(nums.size(), vector<int>(2 * total + 1, -1));
        
        return rec(nums, target, 0, 0);
    }
};
