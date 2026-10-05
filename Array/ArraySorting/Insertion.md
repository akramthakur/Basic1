# Insertion Sort - Solution

## Problem Statement
Implement the Insertion Sort algorithm that sorts an array in ascending order by building a sorted portion one element at a time, inserting each new element into its correct position in the sorted part.

## Step-by-Step Logic

### Insertion Sort Algorithm:
1. **Start from Second Element**: Consider first element as sorted
2. **Pick Element**: Select next element to be inserted
3. **Find Correct Position**: Compare with sorted elements from right to left
4. **Shift Elements**: Move larger elements one position right
5. **Insert Element**: Place current element in correct position
6. **Repeat**: Continue until all elements are processed

## Complexity Analysis

### Time Complexity:
- **Best Case**: **O(n)** - when array is already sorted
- **Average Case**: **O(n²)** - typical case with random data
- **Worst Case**: **O(n²)** - when array is reverse sorted
- **n** = number of elements in array

### Space Complexity: **O(1)**
- **O(1)** - only using constant extra space for variables
- In-place sorting algorithm

## Final Code with Comments

```cpp
#include <iostream>
using namespace std;

/* Function to sort array using insertion sort */
void insertionSort(int arr[], int n)
{
    // Start from the second element (index 1)
    // First element is considered already sorted
    for (int i = 1; i < n; ++i) {
        int key = arr[i];  // Element to be inserted
        int j = i - 1;     // Start comparing with previous element

        /* Move elements of arr[0..i-1], that are
           greater than key, to one position ahead
           of their current position */
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];  // Shift element to the right
            j = j - 1;            // Move to previous position
        }
        
        // Insert the key at its correct position
        arr[j + 1] = key;
    }
}

/* A utility function to print array of size n */
void printArray(int arr[], int n)
{
    for (int i = 0; i < n; ++i)
        cout << arr[i] << " ";
    cout << endl;
}

// Driver method
int main()
{
    int arr[] = { 12, 11, 13, 5, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << "Original array: ";
    printArray(arr, n);

    insertionSort(arr, n);

    cout << "Sorted array: ";
    printArray(arr, n);

    return 0;
}
