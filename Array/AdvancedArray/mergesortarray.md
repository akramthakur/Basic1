# Merge Sorted Array - Solution

## Problem Statement
You are given two integer arrays `nums1` and `nums2`, sorted in non-decreasing order. Merge `nums2` into `nums1` as one sorted array. `nums1` has length `m + n` where the first `m` elements are valid and `n` zeros are at the end.

## Step-by-Step Logic

1. **Three Pointer Technique**:
   - `i`: Points to last valid element in nums1 (m-1)
   - `j`: Points to last element in nums2 (n-1)  
   - `k`: Points to last position in nums1 (m+n-1)

2. **Backward Merging**:
   - Compare elements from the end of both arrays
   - Place larger element at position `k`
   - Move pointers accordingly
   - Continue until one array is exhausted

3. **Handle Remaining Elements**:
   - If nums2 has remaining elements, copy them to nums1
   - If nums1 has remaining elements, they're already in place

## Complexity Analysis

### Time Complexity: **O(m + n)**
- Process each element exactly once from both arrays
- Single pass through combined elements

### Space Complexity: **O(1)**
- In-place merging using existing array
- Only constant extra space for pointers

## Final Code with Comments

```cpp
class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
        // Initialize pointers
        int i = m - 1;      // Last element of valid nums1
        int j = n - 1;      // Last element of nums2
        int k = m + n - 1;  // Last position of nums1

        // Merge from the end while both arrays have elements
        while(j >= 0 && i >= 0) {
            if(nums1[i] > nums2[j]) {
                nums1[k] = nums1[i];  // nums1 element is larger
                k--;
                i--;
            } else {
                nums1[k] = nums2[j];  // nums2 element is larger or equal
                k--;
                j--;
            }
        }

        // Copy remaining elements from nums2 (if any)
        while(j >= 0) {
            nums1[k] = nums2[j];
            j--;
            k--;
        }
        
        // No need to handle remaining nums1 elements as they're already in place
    }
};
