# Jump Game II - Solution

## Problem Statement
Given an array `nums` of non-negative integers, you are initially positioned at the first index. Each element in the array represents your maximum jump length at that position.

Your goal is to reach the last index in the **minimum number of jumps**.

## Step-by-Step Logic

### Algorithm:
1. **DFS with Memoization**: Recursively explore all possible jumps from each position
2. **State Definition**: `dp[i]` = minimum jumps needed to reach last index from position `i`
3. **Recurrence Relation**: 
   - From position `i`, try all jumps from 1 to `nums[i]`
   - Take minimum jumps among all possible paths: `min(1 + dp[i+j])`
4. **Base Cases**:
   - If `i >= nums.size()-1`, reached/overshot the end → return 0 jumps
   - If `nums[i] == 0`, cannot jump anywhere → return large value (invalid)

### Key Insight:
- This is a shortest path problem in an implicit graph
- At each position, we want the minimum jumps to reach the end
- Memoization prevents exponential time complexity

## Complexity Analysis

### Time Complexity: **O(n²)**
- In worst case, each position can jump to all subsequent positions
- With memoization, each state is computed once

### Space Complexity: **O(n)**
- DP array of size n
- Recursion stack depth: O(n) in worst case

## Final Code with Comments

```cpp
class Solution {
public:
    int solve(vector<int>& nums, int i, vector<int>& dp) {
        // Base case: reached or overshot the last index (0 jumps needed)
        if (i >= nums.size() - 1) return 0;
        
        // Return cached result if available
        if (dp[i] != -1) return dp[i];
        
        // If current position has 0 jump capacity, cannot proceed
        if (nums[i] == 0) return 1e9;  // Large value representing infinity
        
        int minJumps = 1e9;  // Initialize with large value
        
        // Try all possible jumps from current position
        for (int j = 1; j <= nums[i]; j++) {
            int jumpsFromNext = solve(nums, i + j, dp);
            minJumps = min(minJumps, 1 + jumpsFromNext);
        }
        
        return dp[i] = minJumps;
    }
    
    int jump(vector<int>& nums) {
        // Single element array: already at the end (0 jumps needed)
        if (nums.size() == 1) return 0;
        
        // DP array for memoization
        vector<int> dp(nums.size(), -1);
        
        return solve(nums, 0, dp);
    }
};
