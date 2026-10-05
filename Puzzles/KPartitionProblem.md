# K-Partition Problem - Backtracking Solution

## Problem Statement
Given an array of integers and an integer `k`, determine if the array can be partitioned into `k` subsets with equal sum. If possible, print all partitions.

## Step-by-Step Logic

### Backtracking Approach:
1. **Pre-check**: Verify if total sum is divisible by `k`
2. **Target Sum**: Each subset should have sum = `total_sum / k`
3. **Subset Assignment**: Try assigning each element to each subset
4. **Constraint Checking**: Don't exceed target sum for any subset
5. **Backtracking**: If assignment fails, try different subset

## Algorithm Details

### Key Components:
- **sumLeft[]**: Tracks remaining capacity for each subset
- **A[]**: Tracks which subset each element belongs to
- **checkSum()**: Verifies if all subsets are completely filled
- **subsetSum()**: Recursive backtracking to assign elements

### Assignment Strategy:
- Process elements from last to first
- For each element, try placing in each valid subset
- Valid placement: `sumLeft[i] - S[n] >= 0`
- Backtrack if current path doesn't lead to solution

## Complexity Analysis

### Time Complexity: **O(k^n)**
- **Exponential**: Each element can go into any of k subsets
- **Pruning**: Invalid assignments are skipped early
- **Worst Case**: When no solution exists or many possibilities

### Space Complexity: **O(n + k)**
- **Assignment Array**: O(n) to track subset membership
- **Sum Left Array**: O(k) to track remaining capacity
- **Recursion Stack**: O(n) depth

## Code with Detailed Comments

```cpp
#include <iostream>
#include <numeric>
using namespace std;

// Function to check if all subsets are filled or not
bool checkSum(int sumLeft[], int k)
{
    for (int i = 0; i < k; i++)
    {
        if (sumLeft[i] != 0) {
            return false;
        }
    }
    return true;
}

// Helper function for solving `k` partition problem
bool subsetSum(int S[], int n, int sumLeft[], int A[], int k)
{
    // Base case: all subsets are perfectly filled
    if (checkSum(sumLeft, k)) {
        return true;
    }

    // Base case: no items left but subsets not filled
    if (n < 0) {
        return false;
    }

    bool result = false;

    // Try placing current element S[n] in each subset
    for (int i = 0; i < k; i++)
    {
        // If not solved yet and current element fits in subset i
        if (!result && (sumLeft[i] - S[n]) >= 0)
        {
            // Mark current element as belonging to subset i
            A[n] = i + 1;

            // Deduct element's value from subset's remaining sum
            sumLeft[i] = sumLeft[i] - S[n];

            // Recur for remaining elements
            result = subsetSum(S, n - 1, sumLeft, A, k);

            // Backtrack: restore the sum for subset i
            sumLeft[i] = sumLeft[i] + S[n];
        }
    }

    return result;
}

// Main function for solving k–partition problem
void partition(int S[], int n, int k)
{
    // Base case: more subsets than elements
    if (n < k)
    {
        cout << "k-partition of set S is not possible";
        return;
    }

    // Calculate total sum of all elements
    int sum = accumulate(S, S + n, 0);

    int A[n], sumLeft[k];

    // Initialize each subset's target sum
    for (int i = 0; i < k; i++) {
        sumLeft[i] = sum / k;
    }

    // Check if sum is divisible by k and solution exists
    bool result = !(sum % k) && subsetSum(S, n - 1, sumLeft, A, k);

    if (!result)
    {
        cout << "k-partition of set S is not possible";
        return;
    }

    // Print all k partitions
    for (int i = 0; i < k; i++)
    {
        cout << "Partition " << i + 1 << " is: ";
        for (int j = 0; j < n; j++)
        {
            if (A[j] == i + 1) {
                cout << S[j] << " ";
            }
        }
        cout << endl;
    }
}

int main()
{
    int S[] = { 7, 3, 5, 12, 2, 1, 5, 3, 8, 4, 6, 4 };
    int n = sizeof(S) / sizeof(S[0]);
    int k = 5;

    partition(S, n, k);

    return 0;
}
