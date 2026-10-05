# Maximum Subarray Sum - Solution

## Problem Statement
Given an integer array, find the contiguous subarray with the largest sum and return its sum.

## Step-by-Step Logic

1. **Kadane's Algorithm**:
   - Maintain running sum of current subarray
   - Track maximum sum encountered so far
   - Reset running sum to 0 when it becomes negative

2. **Key Insight**:
   - If current sum becomes negative, it cannot contribute to maximum sum
   - Better to start fresh from next element
   - Always track the maximum sum encountered

## Complexity Analysis

### Time Complexity: **O(n)**
- Single pass through the array: O(n)
- Constant time operations for each element

### Space Complexity: **O(1)**
- Only using constant extra space for variables
- No additional data structures needed

## Final Code with Comments

```cpp
class Solution {
public:
    int maxSubArray(vector<int>& arr) {
        long long sum = 0;           // Current running sum
        long long maxSum = INT_MIN;  // Maximum sum found so far
        
        for(int i = 0; i < arr.size(); i++){
            sum += arr[i];           // Add current element to running sum
            maxSum = max(maxSum, sum); // Update maximum sum
            
            // Reset if current sum becomes negative
            if(sum < 0){
                sum = 0;  // Start fresh from next element
            }
        }
        return maxSum;  // Return maximum subarray sum
    }
};
