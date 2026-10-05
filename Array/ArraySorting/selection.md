# Selection Sort - Solution

## Problem Statement
Implement the Selection Sort algorithm that sorts an array in ascending order by repeatedly finding the minimum element from the unsorted part and putting it at the beginning.

## Step-by-Step Logic

### Selection Sort Algorithm:
1. **Divide Array**: Split into sorted (left) and unsorted (right) portions
2. **Find Minimum**: Scan unsorted portion to find smallest element
3. **Swap**: Move minimum element to end of sorted portion
4. **Expand Sorted Portion**: Increase sorted portion by one element each pass
5. **Repeat**: Continue until entire array is sorted

## Complexity Analysis

### Time Complexity: **O(n²)**
- **Best Case**: **O(n²)** - always scans entire unsorted portion
- **Average Case**: **O(n²)** - same number of comparisons regardless of input
- **Worst Case**: **O(n²)** - performs n(n-1)/2 comparisons
- **n** = number of elements in array

### Space Complexity: **O(1)**
- **O(1)** - only using constant extra space for variables
- In-place sorting algorithm

## Final Code with Comments

```cpp
#include <bits/stdc++.h>
using namespace std;

void selectionSort(vector<int> &arr) {
    int n = arr.size();

    // One by one move boundary of unsorted subarray
    for (int i = 0; i < n - 1; ++i) {
        
        // Assume the current position holds the minimum element
        int min_idx = i;

        // Iterate through the unsorted portion to find the actual minimum
        for (int j = i + 1; j < n; ++j) {
            // If current element is smaller than current minimum
            if (arr[j] < arr[min_idx]) {
                // Update min_idx to point to new minimum element
                min_idx = j; 
            }
        }

        // Move minimum element to its correct position
        // Swap the found minimum element with the first element of unsorted part
        swap(arr[i], arr[min_idx]);
    }
}

void printArray(vector<int> &arr) {
    for (int &val : arr) {
        cout << val << " ";
    }
    cout << endl;
}

int main() {
    vector<int> arr = {64, 25, 12, 22, 11};

    cout << "Original array: ";
    printArray(arr); 

    selectionSort(arr);

    cout << "Sorted array: ";
    printArray(arr);

    return 0;
}
