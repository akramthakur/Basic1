# Max Chunks To Make Sorted - Alternative Solution

## Problem Statement
Given an array `arr` of distinct integers from `0` to `n-1` (a permutation of `[0, 1, ..., n-1]`), we split the array into some number of chunks (partitions) and individually sort each chunk. After concatenating them, the result should equal the sorted array.

Return the largest number of chunks we can make to sort the array.

## Step-by-Step Logic

### Algorithm:
1. **Prefix Maximum**: Compute the maximum element from left to right
2. **Suffix Minimum**: Compute the minimum element from right to left
3. **Chunk Boundaries**: A chunk can end at index `i` if `left[i] <= right[i+1]`

### Key Insight:
- `left[i]` represents the maximum element in `arr[0..i]`
- `right[i+1]` represents the minimum element in `arr[i+1..n-1]`
- If `left[i] <= right[i+1]`, then all elements in the left chunk are ≤ all elements in the right chunk

## Complexity Analysis

### Time Complexity: **O(n)**
- Three passes through the array
- Constant time operations per element

### Space Complexity: **O(n)**
- Two auxiliary arrays of size n

## Final Code with Comments

```cpp
class Solution {
public:
    int maxChunksToSorted(vector<int>& arr) {
        int n = arr.size();
        vector<int> left(n);   // left[i] = max(arr[0..i])
        vector<int> right(n);  // right[i] = min(arr[i..n-1])
        
        // Compute prefix maximum from left to right
        left[0] = arr[0];
        for (int i = 1; i < n; i++) {
            left[i] = max(left[i - 1], arr[i]);
        }
        
        // Compute suffix minimum from right to left
        right[n - 1] = arr[n - 1];
        for (int i = n - 2; i >= 0; i--) {
            right[i] = min(arr[i], right[i + 1]);
        }
        
        // Count chunks: we can split after index i if left[i] <= right[i+1]
        int res = 1;  // At least one chunk (the entire array)
        for (int i = 0; i < n - 1; i++) {
            if (left[i] <= right[i + 1]) {
                res++;
            }
        }
        
        return res;
    }
};
