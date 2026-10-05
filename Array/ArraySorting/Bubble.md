# Optimized Bubble Sort - Solution

## Problem Statement
Implement an optimized version of the Bubble Sort algorithm that sorts an array in ascending order. The optimization detects when the array is already sorted and terminates early.

## Step-by-Step Logic

### Optimized Bubble Sort Algorithm:
1. **Outer Loop**: Iterate through each element (n-1 times)
2. **Inner Loop**: Compare adjacent elements up to unsorted portion
3. **Swap if Needed**: If current element > next element, swap them
4. **Early Termination**: Track if any swaps occurred in a pass
5. **Stop if Sorted**: If no swaps in a pass, array is sorted

## Complexity Analysis

### Time Complexity: 
- **Best Case**: **O(n)** - when array is already sorted (early termination)
- **Average Case**: **O(n²)** - typical case with random data
- **Worst Case**: **O(n²)** - when array is reverse sorted
- **n** = number of elements in array

### Space Complexity: **O(1)**
- **O(1)** - only using constant extra space for variables
- In-place sorting algorithm

## Final Code with Comments

```cpp
#include <bits/stdc++.h>
using namespace std;

// An optimized version of Bubble Sort 
void bubbleSort(vector<int>& arr) {
    int n = arr.size();
    bool swapped;  // Flag to track if any swaps occurred
  
    // Outer loop for each pass
    for (int i = 0; i < n - 1; i++) {
        swapped = false;  // Reset flag for each pass
        
        // Inner loop for comparing adjacent elements
        // Last i elements are already in place
        for (int j = 0; j < n - i - 1; j++) {
            // Compare adjacent elements
            if (arr[j] > arr[j + 1]) {
                // Swap if they are in wrong order
                swap(arr[j], arr[j + 1]);
                swapped = true;  // Set flag if swap occurred
            }
        }
      
        // If no two elements were swapped in inner loop,
        // then array is already sorted
        if (!swapped)
            break;  // Early termination
    }
}

// Function to print a vector
void printVector(const vector<int>& arr) {
    for (int num : arr)
        cout << " " << num;
    cout << endl;
}

int main() {
    vector<int> arr = { 64, 34, 25, 12, 22, 11, 90 };
    
    cout << "Original array:";
    printVector(arr);
    
    bubbleSort(arr);
    
    cout << "Sorted array:";
    printVector(arr);
    return 0;
}
