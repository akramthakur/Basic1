# Array Sum - Solution

## Problem Statement
Calculate the sum of all elements in an array using recursion.

## Step-by-Step Logic

1. **Recursive Approach**:
   - Start from index 0 with initial sum 0
   - At each step, add current element to running sum
   - Move to next index recursively
   - Stop when all elements are processed

2. **Base Case**:
   - When index reaches array size, return accumulated sum

3. **Tail Recursion**:
   - Uses tail recursion where the recursive call is the last operation
   - Some compilers can optimize this to iterative code

## Complexity Analysis

### Time Complexity: **O(n)**
- Each array element is visited exactly once
- n recursive calls for n elements

### Space Complexity: **O(n)**
- Recursion stack depth equals array size
- Each recursive call uses stack space
- For large arrays, this could cause stack overflow

## Final Code with Comments

```cpp
class Solution {
public:
    // Recursive function to calculate sum
    int sum(vector<int>& arr, int i, int ans) {
        // Base case: reached end of array
        if(i == arr.size()) {
            return ans;  // Return accumulated sum
        }
        // Recursive case: add current element and move to next
        return sum(arr, i + 1, ans + arr[i]);
    }
    
    int arraySum(vector<int>& arr) {
        // Start recursion from index 0 with initial sum 0
        int ans = sum(arr, 0, 0);
        return ans;
    }
};
