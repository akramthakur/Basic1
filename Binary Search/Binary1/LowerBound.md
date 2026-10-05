# Lower Bound - Solution

## Problem Statement
Given a sorted array and a target value, find the first index where the target can be inserted to maintain sorted order (first position where arr[i] >= target).

## Step-by-Step Logic

### Lower Bound Definition:
- **Returns**: The first index where arr[i] >= target
- **If target exists**: Returns first occurrence index
- **If target doesn't exist**: Returns insertion position
- **If target > all elements**: Returns array size

## Complexity Analysis

### Time Complexity: **O(log n)**
- **O(log n)** for binary search implementation
- **n** = number of elements in array

### Space Complexity: **O(1)**
- **O(1)** - only using constant extra space for variables
- In-place algorithm

## Final Code with Comments

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int lowerBound(vector<int> &arr, int target) {
    // Using built-in lower_bound function
    // Returns iterator to first element >= target
    int index = lower_bound(arr.begin(), arr.end(), target) - arr.begin();
    
    return index;
}

int main() {
    vector<int> arr = {2, 3, 7, 10, 11, 11, 25};
    int target = 9;
    
    cout << "Array: ";
    for(int num : arr) cout << num << " ";
    cout << "\nTarget: " << target << endl;
    cout << "Lower Bound Index: " << lowerBound(arr, target) << endl;
    
    return 0;
}
