# Missing Number - Solution

## Problem Statement
Given an array `nums` containing `n` distinct numbers in the range `[0, n]`, return the only number in the range that is missing from the array.

## Step-by-Step Logic

### Frequency Map Approach:
1. **Create Frequency Array**: Size n+1 initialized to 0
2. **Mark Present Numbers**: Increment count for each number found
3. **Find Missing Number**: Return index with count 0

## Complexity Analysis

### Time Complexity: **O(n)**
- First pass: O(n) to build frequency map
- Second pass: O(n) to find missing number
- Total: O(2n) = O(n)

### Space Complexity: **O(n)**
- Frequency array of size n+1
- Additional O(n) space

## Final Code with Comments

```cpp
class Solution {
public:
    int missingNumber(vector<int>& nums) {
        int n = nums.size();
        vector<int> map(n + 1, 0);  // Frequency array
        
        // Mark all present numbers
        for(int i = 0; i < nums.size(); i++) {
            map[nums[i]]++;
        }
        
        // Find the missing number (count = 0)
        for(int i = 0; i < n + 1; i++) {
            if(map[i] == 0) {
                return i;
            }
        }
        return -1;  // Should never reach here per problem constraints
    }
};
