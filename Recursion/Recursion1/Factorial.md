# Factorial Calculation - Solution

## Problem Statement
Calculate the factorial of a non-negative integer `n`. The factorial of `n` (denoted as `n!`) is the product of all positive integers less than or equal to `n`.

## Step-by-Step Logic

### Recursive Algorithm:
1. **Base Case**: If `n` is 0 or 1, return 1
2. **Recursive Case**: Return `n * factorial(n - 1)`
3. **Unwinding**: Multiply results as recursion unwinds

## Complexity Analysis

### Time Complexity: **O(n)**
- **O(n)** recursive calls
- **O(1)** operations per recursive call
- **n** = input number

### Space Complexity: **O(n)**
- **O(n)** for recursion call stack
- Each recursive call adds a stack frame

## Final Code with Comments

```cpp
#include <iostream>
using namespace std;

int factorial(int n)
{
    // Base case: factorial of 0 or 1 is 1
    if (n == 0 || n == 1)
        return 1;
    
    // Recursive case: n! = n * (n-1)!
    return n * factorial(n - 1);
}

int main()
{
    int num = 5;
    cout << "Factorial of " << num << " is: " << factorial(num) << endl;
    return 0;
}
