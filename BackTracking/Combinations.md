# Combinations - Solution

## Problem Statement
Given two integers `n` and `k`, return all possible combinations of `k` numbers chosen from the range `[1, n]`. You may return the answer in any order.

## Step-by-Step Logic

### Backtracking Approach:
1. **Start Position**: Begin from current number `i` and try numbers from `i` to `n`
2. **Include Number**: Add current number to combination
3. **Recurse**: Generate combinations from remaining numbers (j+1 to n)
4. **Backtrack**: Remove last number to explore other possibilities
5. **Base Case**: When combination size equals `k`, save current combination

## Complexity Analysis

### Time Complexity: **O(C(n,k) × k)**
- **O(C(n,k))** total combinations generated (binomial coefficient)
- **O(k)** time per combination for pushing/popping
- **n choose k** = n! / (k! × (n-k)!)

### Space Complexity: **O(k)**
- **O(k)** for recursion call stack depth
- **O(k)** for current combination storage
- **O(C(n,k) × k)** for output storage (not counted in auxiliary space)

## Final Code with Comments

```cpp
class Solution {
public:
    void rec(vector<vector<int>>& res, vector<int>& nums, int i, int n, int k) {
        // Base case: combination size equals k, save current combination
        if(nums.size() == k) {
            res.push_back(nums);
            return;
        }
        
        // Try all numbers from current position to n
        for(int j = i; j <= n; j++) {
            // Include current number
            nums.push_back(j);
            
            // Recursively generate combinations from remaining numbers
            rec(res, nums, j + 1, n, k);
            
            // Backtrack: remove last number to try other possibilities
            nums.pop_back();
        }
    }
    
    vector<vector<int>> combine(int n, int k) {
        vector<vector<int>> res;  // Store all combinations
        vector<int> num;         // Current combination being built
        rec(res, num, 1, n, k);  // Start from number 1
        return res;
    }
};
