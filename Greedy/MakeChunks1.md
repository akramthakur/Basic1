# Max Chunks To Make Sorted - Solution

## Problem Statement
Given an array `arr` of distinct integers from `0` to `n-1` (a permutation of `[0, 1, ..., n-1]`), we split the array into some number of chunks (partitions) and individually sort each chunk. After concatenating them, the result should equal the sorted array.

Return the largest number of chunks we can make to sort the array.

## Step-by-Step Logic

### Algorithm:
1. **Track Maximum**: Keep track of the maximum element encountered so far
2. **Chunk Boundary**: When the maximum element equals the current index, we've found a valid chunk
3. **Greedy Partition**: Each valid chunk can be sorted independently

### Key Insight:
- In the sorted array, element `i` should be at position `i`
- If the maximum element up to index `i` equals `i`, then all elements `0..i` are present in this segment
- This means we can sort this chunk independently and it will be in the correct final position

## Complexity Analysis

### Time Complexity: **O(n)**
- Single pass through the array
- Constant time operations per element

### Space Complexity: **O(1)**
- Only two integer variables used

## Final Code with Comments

```cpp
class Solution {
public:
    int maxChunksToSorted(vector<int>& arr) {
        int res = 0;        // Count of chunks
        int curmax = -1;    // Maximum element encountered so far
        
        for (int i = 0; i < arr.size(); i++) {
            // Update the maximum element in current segment
            curmax = max(curmax, arr[i]);
            
            // If maximum equals current index, we can form a chunk
            if (curmax == i) {
                res++;
            }
        }
        
        return res;
    }
};
