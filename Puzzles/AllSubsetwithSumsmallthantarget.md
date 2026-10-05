# Find All Subsets with Sum ≤ Target - Solution

## Problem Statement
Given an array of integers and a target sum, find all subsets where the sum of elements is less than or equal to the target.

## Step-by-Step Logic

### Backtracking/Subset Generation Approach:
1. **Sort Array**: Sort input to generate subsets in sorted order
2. **Generate Subsets**: Use backtracking to generate all possible subsets
3. **Check Sum Constraint**: Only include subsets where sum ≤ target
4. **Include All Sizes**: Consider subsets of all sizes (empty to full)
5. **Avoid Early Termination**: Continue exploring even if current sum exceeds target (for smaller subsets)

## Complexity Analysis

### Time Complexity: **O(2ⁿ)**
- **O(n log n)** for sorting
- **O(2ⁿ)** for generating all subsets in worst case
- **n** = number of elements in input array

### Space Complexity: **O(n)**
- **O(n)** for recursion call stack depth
- **O(2ⁿ)** for output storage (not counted in auxiliary space)
- **O(n)** for current subset tracking

## Final Code with Comments

```cpp
#include <bits/stdc++.h>
using namespace std;

void generateSubsets(vector<int>& nums, int target, int start, vector<int>& current, vector<vector<int>>& result, int currentSum) {
    // Always add current subset if sum ≤ target (including empty set)
    if (currentSum <= target) {
        result.push_back(current);
    }
    
    // If current sum already exceeds target, no need to explore further
    if (currentSum >= target) {
        return;
    }
    
    // Generate all possible subsets by including elements one by one
    for (int i = start; i < nums.size(); i++) {
        // Include nums[i] in current subset
        current.push_back(nums[i]);
        currentSum += nums[i];
        
        // Recursively generate subsets with remaining elements
        generateSubsets(nums, target, i + 1, current, result, currentSum);
        
        // Backtrack: remove nums[i] from current subset
        currentSum -= nums[i];
        current.pop_back();
    }
}

void findAllSubsets(vector<int>& nums, int target) {
    sort(nums.begin(), nums.end());  // Sort to get subsets in sorted order
    vector<int> current;
    vector<vector<int>> result;
    int currentSum = 0;
    
    generateSubsets(nums, target, 0, current, result, currentSum);
    
    // Print all valid subsets
    for (auto& subset : result) {
        cout << "[";
        for (int i = 0; i < subset.size(); i++) {
            cout << subset[i];
            if (i < subset.size() - 1) cout << ", ";
        }
        cout << "] (Sum: ";
        int sum = 0;
        for (int num : subset) sum += num;
        cout << sum << ")" << endl;
    }
}

int main() {
    int target = 10;
    vector<int> input = {2, 7, 4, 9, 5, 1, 3};
    
    cout << "All subsets with sum ≤ " << target << ":" << endl;
    findAllSubsets(input, target);
    
    return 0;
}
