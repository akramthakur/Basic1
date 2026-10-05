# Count Subarrays with Zero Sum - Solution

## Problem Statement
Given an array of integers, count the number of subarrays that have a sum equal to zero.

## Step-by-Step Logic

### Prefix Sum with Hash Map Approach:
1. **Prefix Sum Calculation**: Maintain running sum of elements
2. **Hash Map Storage**: Store frequency of each prefix sum encountered
3. **Zero Sum Detection**:
   - If prefix sum becomes zero, increment count
   - If same prefix sum appears again, subarray between occurrences has zero sum
4. **Combination Formula**: For n occurrences of a prefix sum, number of zero-sum subarrays = nC2

## Complexity Analysis

### Time Complexity: **O(n)**
- **O(n)** for single pass through the array
- **O(1)** hash map operations on average
- **n** = number of elements in array

### Space Complexity: **O(n)**
- **O(n)** for hash map storage in worst case
- Stores at most n prefix sums

## Final Code with Comments

```cpp
class Solution {
public:
    int findSubarray(vector<int> &arr) {
        long long cnt = 0;          // Count of zero-sum subarrays
        long long preSum = 0;       // Running prefix sum
        unordered_map<long long, long long> map; // Store frequency of prefix sums
        
        for(int i = 0; i < arr.size(); i++) {
            preSum += arr[i];       // Update prefix sum
            
            map[preSum]++;          // Increment frequency of current prefix sum
            
            // If prefix sum itself is zero, we found a subarray from start to current index
            if(preSum == 0) {
                cnt++;
            }
        }
        
        // For each prefix sum that occurred multiple times, 
        // the subarrays between occurrences have zero sum
        for(auto &i : map) {
            // nC2 = n*(n-1)/2 combinations of indices with same prefix sum
            cnt += ((i.second) * (i.second - 1)) / 2;
        }
        
        return cnt;
    }
};
