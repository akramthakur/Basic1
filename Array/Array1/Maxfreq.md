# Maximum Frequency Elements - Solution

## Problem Statement
Given an array of integers, find the total number of elements that have the maximum frequency in the array.

## Step-by-Step Logic

1. **Single Pass Frequency Tracking**:
   - Use hash map to count frequency of each element
   - Track maximum frequency encountered in real-time
   - Count how many elements share this maximum frequency

2. **Real-time Updates**:
   - When current frequency exceeds max frequency, update max and reset count
   - When current frequency equals max frequency, increment count
   - Calculate result as count × max frequency

## Complexity Analysis

### Time Complexity: **O(n)**
- Single pass through the array: O(n)
- Each operation inside loop is O(1) average case

### Space Complexity: **O(n)**
- Hash map to store frequency counts: O(n)
- In worst case, all elements are unique

## Final Code with Comments

```cpp
class Solution {
public:
    int maxFrequencyElements(vector<int>& nums) {
        // Hash map to store frequency of each element
        unordered_map<int, int> map;
        int maxfreq = 0;  // Track maximum frequency
        int count = 0;    // Count elements with max frequency
        
        // Single pass through array
        for(int num : nums){
            // Increment frequency of current element
            map[num]++;
            int cur = map[num];  // Current frequency
            
            // Update max frequency and count
            if(cur > maxfreq){
                maxfreq = cur;  // New maximum found
                count = 1;      // Reset count for new max
            }
            else if(cur == maxfreq){
                count++;        // Another element with same max frequency
            }
        }
        
        // Return total elements with maximum frequency
        return count * maxfreq;
    }
};
