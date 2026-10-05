# Koko Eating Bananas - Solution

## Problem Statement
Koko loves to eat bananas. There are `n` piles of bananas, the `i-th` pile has `piles[i]` bananas. Koko can eat bananas at a speed of `k` bananas per hour. Each hour, she chooses some pile and eats `k` bananas from that pile. If the pile has less than `k` bananas, she eats all of them and won't eat any more bananas during that hour. Koko wants to finish eating all bananas within `h` hours. Return the minimum integer `k` such that she can eat all the bananas within `h` hours.

## Step-by-Step Logic

### Binary Search Approach:
1. **Search Space**: 
   - Minimum speed: `l = 1` (eat 1 banana/hour)
   - Maximum speed: `r = 1,000,000,000` (max possible in constraints)

2. **Binary Search**:
   - Calculate mid speed `m = (l + r) / 2`
   - Check if Koko can finish all bananas in `h` hours at speed `m`
   - Adjust search range based on result

3. **Hours Calculation**:
   - For each pile: `hours += ceil(pile / m)`
   - Using integer math: `(pile + m - 1) / m` gives ceiling division

4. **Decision**:
   - If `total hours > h`: current speed too slow, need faster speed (`l = m + 1`)
   - If `total hours <= h`: current speed works, try slower speed (`r = m`)

## Complexity Analysis

### Time Complexity: **O(n log(maxPile))**
- Binary search iterations: O(log(1,000,000,000)) ≈ O(30)
- Each iteration processes n piles: O(n)
- Total: O(30n) = O(n)

### Space Complexity: **O(1)**
- Only using constant extra space for variables
- No additional data structures

## Detailed Code Explanation

```cpp
class Solution {
public:
    int minEatingSpeed(vector<int>& piles, int h) {
        int l = 1, r = 1000000000;  // Search space: 1 to 1 billion
        
        while(l < r) {
            int m = (l + r) / 2;    // Midpoint of search space
            int total = 0;           // Total hours needed at speed m
            
            // Calculate total hours needed to eat all piles at speed m
            for(int p : piles)
                total += (p + m - 1) / m;  // Ceiling division: ceil(p/m)
            
            // Binary search decision
            if(total > h)
                l = m + 1;  // Too slow, need faster speed
            else 
                r = m;      // Fast enough, try slower speed
        }
        return l;  // Minimum speed that works
    }
};
