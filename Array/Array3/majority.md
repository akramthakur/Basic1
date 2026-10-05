# Majority Element - Solution

## Problem Statement
Given an array of size n, find the majority element. The majority element is the element that appears more than ⌊n/2⌋ times.

## Step-by-Step Logic

1. **Frequency Counting**:
   - Use hash map to count occurrences of each element
   - Store element as key and frequency as value

2. **Majority Check**:
   - Iterate through hash map entries
   - Check if any element's frequency exceeds n/2
   - Return the majority element if found

3. **Assumption**:
   - Problem guarantees majority element exists
   - Return -1 as fallback (though majority always exists)

## Complexity Analysis

### Time Complexity: **O(n)**
- One pass to count frequencies: O(n)
- One pass to check majority condition: O(n)
- Total: O(2n) = O(n)

### Space Complexity: **O(n)**
- Hash map to store frequency counts: O(n)
- In worst case, all elements are unique except majority

## Final Code with Comments

```cpp
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        unordered_map<int, int> ans;  // Hash map for frequency counting
        int n = nums.size();          // Array size
        
        // Count frequency of each element
        for(int i = 0; i < nums.size(); i++)
            ans[nums[i]]++;           // Increment count for current element

        // Check for majority element
        for(auto [x, y] : ans){
            if(y > (n / 2)){          // If frequency > n/2
                return x;             // Return majority element
            }
        }
        return -1;  // Fallback (majority element guaranteed to exist)
    }
};
