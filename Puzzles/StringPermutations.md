# String Permutations - Solution

## Problem Statement
Given a string `s`, find all permutations of the string in lexicographical order.

## Step-by-Step Logic

### Using STL Approach:
1. **Sort First**: Sort the string to get the lexicographically smallest permutation
2. **Generate Permutations**: Use `next_permutation` to systematically generate all permutations
3. **Collect Results**: Store each permutation in the result vector

## Algorithm Details

### `next_permutation` Function:
- **Purpose**: Generates the next lexicographically greater permutation
- **Returns**: `true` if next permutation exists, `false` otherwise
- **Modifies**: The input range in-place
- **Complexity**: Linear in the size of the range

### Process Flow:
1. Sort input string to start from smallest permutation
2. Add current permutation to result
3. Generate next permutation using `next_permutation`
4. Repeat until all permutations are generated

## Complexity Analysis

### Time Complexity: **O(n × n!)**
- Sorting: O(n log n)
- Number of permutations: O(n!)
- Each permutation operation: O(n)
- Total: O(n × n!) + O(n log n) = **O(n × n!)**

### Space Complexity: **O(n × n!)**
- Storage for all permutations: O(n × n!)
- Recursion stack: O(n) for `next_permutation`
- Total: **O(n × n!)**

## Final Code with Comments

```cpp
class Solution {
public:
    vector<string> findPermutation(string &s) {
        // Sort the string to get lexicographically smallest permutation
        sort(s.begin(), s.end());
        
        vector<string> ans;
        
        // Generate all permutations using next_permutation
        do {
            // Add current permutation to result
            ans.push_back(s);
        } while(next_permutation(s.begin(), s.end()));
        
        return ans;
    }
};
