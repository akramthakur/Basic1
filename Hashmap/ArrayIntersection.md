# Array Intersection - Solution

## Problem Statement
Given two integer arrays `nums1` and `nums2`, return an array of their intersection (common elements present in both arrays).

## Step-by-Step Logic

### Three-Pass Hash Map Approach:
1. **First Pass**: Store all elements from nums1 in hash map, mark as `false`
2. **Second Pass**: For elements in nums2 that exist in map, mark as `true`
3. **Third Pass**: Collect all keys marked as `true` (common elements)

## Complexity Analysis

### Time Complexity: **O(n + m)**
- First pass through nums1: O(n)
- Second pass through nums2: O(m)
- Third pass through map: O(min(n, m))
- Total: O(n + m)

### Space Complexity: **O(n)**
- Hash map storage for nums1 elements: O(n)
- Result vector: O(min(n, m))

## Final Code with Comments

```cpp
class Solution {
public:
    vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
        unordered_map<int, bool> map;
        
        // First pass: store all elements from nums1
        for(int i = 0; i < nums1.size(); i++) {
            map[nums1[i]] = false;  // Initially mark as not found in nums2
        }
        
        // Second pass: mark elements that exist in both arrays
        for(int i = 0; i < nums2.size(); i++) {
            if(map.find(nums2[i]) != map.end()) {
                map[nums2[i]] = true;  // Mark as found in both arrays
            }
        }
        
        // Third pass: collect intersection results
        vector<int> res;
        for(auto [key, val] : map) {
            if(val) {
                res.push_back(key);  // Add elements present in both arrays
            }
        }
        
        return res;
    }
};
