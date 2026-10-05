# Find Repeating Elements - Solution

## Problem Statement
Given an array of integers, find all the repeating elements (duplicates) in the array and print them. Each duplicate element should be printed only once.

## Step-by-Step Logic

### Brute Force Approach:
1. **Nested Loop**: Compare each element with every other element
2. **Duplicate Detection**: When two different indices have same value, it's a duplicate
3. **Store Duplicates**: Store found duplicates in a temporary array
4. **Remove Consecutive Duplicates**: Print only unique duplicate values

## Complexity Analysis

### Time Complexity: **O(n²)**
- **O(n²)** for nested loops comparing all pairs
- **n** = number of elements in array
- Inefficient for large arrays

### Space Complexity: **O(n)**
- **O(n)** for duplicate array storage
- **O(1)** additional space for counters

## Final Code with Comments

```cpp
#include<bits/stdc++.h>
using namespace std;

void findRepeatingElements(int arr[], int n) {
    int cnt = 0;
    int dup[n];  // Array to store duplicate elements
    
    // Nested loop to find duplicates
    for(int i = 0; i < n - 1; i++) {
        for(int j = i + 1; j < n; j++) {
            // If duplicate found and elements are at different positions
            if(arr[i] == arr[j]) {
                dup[cnt++] = arr[i];  // Store the duplicate element
            }
        }
    }
    
    cout << "The repeating elements are: ";
    // Print unique duplicates (skip consecutive duplicates)
    for(int i = 0; i < cnt; i++) {
        if(dup[i] != dup[i + 1]) {  // Check if next element is different
            cout << dup[i] << " ";
        }
    }
}

int main() {
    int arr[] = {1, 1, 2, 3, 4, 4, 5, 2};
    findRepeatingElements(arr, 8);
    return 0;
}
