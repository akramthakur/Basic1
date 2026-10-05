# Upper Bound - Counting Smaller and Larger Elements

## Problem Statement
Given a sorted array and a target value, use `upper_bound` to count:
1. Number of elements smaller than or equal to target
2. Number of elements strictly greater than target

## Step-by-Step Logic

### Upper Bound Definition:
- **Returns**: First iterator where element > target
- **Smaller Elements**: `upper_bound - begin()` gives count of elements <= target
- **Larger Elements**: `end() - upper_bound` gives count of elements > target

## Complexity Analysis

### Time Complexity: **O(log n)**
- **O(log n)** for `upper_bound` binary search
- **n** = number of elements in array

### Space Complexity: **O(1)**
- **O(1)** - only using constant extra space
- No additional data structures

## Final Code with Comments

```cpp
#include <algorithm>
#include <iostream>
#include <vector>
using namespace std;

int main()
{
    vector<int> v = {10, 20, 30, 40, 50};
    int val = 30;

    // Finding the upper bound of val in v
    // upper_bound returns iterator to first element > val
    auto ub = upper_bound(v.begin(), v.end(), val);

    // Number of elements <= val (smaller or equal)
    // Distance from beginning to upper_bound
    cout << "No. of Smaller or Equal Elements: " << ub - v.begin() << endl;

    // Number of elements > val (strictly larger)
    // Distance from upper_bound to end
    cout << "No. of Larger Elements: " << v.end() - ub;

    return 0;
}
