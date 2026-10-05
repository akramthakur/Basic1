# Array Reverse After Position M - Solution

## Problem Statement
Reverse the elements of the given array starting from index `m+1` to the end of the array, while keeping the first `m+1` elements (indices 0 to m) unchanged.

## Step-by-Step Logic

1. **Initialize Pointers**: 
   - Start pointer `i` at position `m+1` (first element to reverse)
   - End pointer `j` at last position `arr.size()-1`

2. **Two-Pointer Swap**:
   - Swap elements at positions `i` and `j`
   - Move `i` forward and `j` backward
   - Continue until `i` crosses `j`

3. **Termination**:
   - Stop when `i >= j` (all elements in target range are reversed)

## Complexity Analysis

### Time Complexity: **O(n)**
- Where `n` is the number of elements from `m+1` to end
- We process each element in the target range exactly once
- Best case: O(1) when array size is 1 or m is at end
- Worst case: O(n) when reversing almost entire array

### Space Complexity: **O(1)**
- Only using constant extra space for pointers and temp variable
- In-place algorithm, no additional data structures

## Final Code with Comments

```cpp
void reverseArray(vector<int> &arr, int m) {
    // Start from the element after position m
    int i = m + 1;
    // End at the last element
    int j = arr.size() - 1;
    
    // Two-pointer approach to reverse
    while (i < j) {
        // Swap elements at i and j
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
        
        // Move pointers towards center
        i++;
        j--;
    }
    
    // Array is now reversed from m+1 to end
}
