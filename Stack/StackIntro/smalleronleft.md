# Smallest on Left - Solution Analysis

## Problem Statement
For each element in the array, find the largest element to its left that is smaller than the current element. If no such element exists, return -1.

## Current Approach Issues

### Problems Identified:
1. **Inefficient Time Complexity**: O(n²) due to nested loops
2. **Unnecessary Stack Copying**: Creating temp stack for each element
3. **Inefficient Search**: Linear scan through all previous elements

## Complexity Analysis

### Current Code:
- **Time Complexity**: O(n²)
  - Outer loop: n iterations
  - Inner while loop: up to n operations each
  - Total: O(n²) operations

- **Space Complexity**: O(n)
  - Stack storage: O(n)
  - Result vector: O(n)

## Optimized Solution

### Using Balanced BST (set) - O(n log n)

```cpp
#include <vector>
#include <set>
using namespace std;

vector<int> Smallestonleft(int arr[], int n) {
    vector<int> ans;
    set<int> s;
    
    for(int i = 0; i < n; i++) {
        auto it = s.lower_bound(arr[i]);
        
        if(it == s.begin()) {
            // No smaller element exists
            ans.push_back(-1);
        } else {
            // Move to largest element smaller than arr[i]
            it--;
            ans.push_back(*it);
        }
        
        s.insert(arr[i]);
    }
    return ans;
}
