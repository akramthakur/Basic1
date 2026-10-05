# Count Primes - Solution

## Problem Statement
Given an integer `n`, return the number of prime numbers that are strictly less than `n`.

## Step-by-Step Logic

### Algorithm:
1. **Sieve of Eratosthenes**: Efficient algorithm to find all primes up to n
2. **Mark Non-Primes**: Start from 2 and mark all multiples as non-prime
3. **Optimization**: Only check up to √n, as larger factors would have been marked by smaller primes

### Key Insights:
- All non-prime numbers have at least one prime factor ≤ √n
- Start marking from i² (smaller multiples would have been marked by smaller primes)
- Skip even numbers after 2 for further optimization

## Complexity Analysis

### Time Complexity: **O(n log log n)**
- The Sieve of Eratosthenes has nearly linear time complexity
- Much faster than O(n √n) naive approach

### Space Complexity: **O(n)**
- Boolean array of size n to track prime status

## Final Code with Comments

```cpp
class Solution {
public:
    int countPrimes(int n) {
        if (n <= 2) return 0;  // No primes less than 2
        
        vector<bool> primes(n, true);
        primes[0] = false;  // 0 is not prime
        primes[1] = false;  // 1 is not prime
        
        // Sieve of Eratosthenes
        for (int i = 2; i * i < n; i++) {
            if (primes[i]) {
                // Mark all multiples of i as non-prime
                // Start from i*i (smaller multiples already marked by smaller primes)
                for (int j = i * i; j < n; j += i) {
                    primes[j] = false;
                }
            }
        }
        
        // Count primes
        int count = 0;
        for (int i = 2; i < n; i++) {
            if (primes[i]) {
                count++;
            }
        }
        return count;
    }
};
