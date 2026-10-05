# Linear Search - Solution

## Problem Statement
Implement a linear search algorithm to find the position of a given key in an unsorted array. Return the index if found, otherwise return -1.

## Step-by-Step Logic

### Linear Search Algorithm:
1. **Iterate through array**: Traverse each element from start to end
2. **Compare with key**: Check if current element matches search key
3. **Return index**: If match found, return current index immediately
4. **Not found**: If loop completes without match, return -1

## Complexity Analysis

### Time Complexity: **O(n)**
- **Best Case**: O(1) - element found at first position
- **Average Case**: O(n) - element found in middle
- **Worst Case**: O(n) - element not found or at last position
- **n** = number of elements in array

### Space Complexity: **O(1)**
- **O(1)** - only using constant extra space for variables
- No additional data structures used

## Final Code with Comments

```cpp
// C++ program to implement linear search in unsorted array
#include <bits/stdc++.h>
using namespace std;

// Function to implement search operation
int findElement(int arr[], int n, int key)
{
    // Iterate through each element in the array
    for (int i = 0; i < n; i++) {
        // Check if current element matches the key
        if (arr[i] == key) {
            return i;  // Return index if found
        }
    }

    // If the key is not found after checking all elements
    return -1;
}

// Driver's Code
int main()
{
    int arr[] = { 12, 34, 10, 6, 40 };
    int n = sizeof(arr) / sizeof(arr[0]);  // Calculate array size

    // Using last element as search element
    int key = 40;

    // Function call to perform linear search
    int position = findElement(arr, n, key);

    // Display results
    if (position == -1) {
        cout << "Element not found";
    } else {
        cout << "Element Found at Position: " << position + 1;
    }

    return 0;
}
