# Array Intersection - Solution

## Problem Statement
Given two arrays, find the intersection of the two arrays (common elements present in both arrays).

## Step-by-Step Logic

1. **Mark First Array Elements**:
   - Store all elements from first array in hash map
   - Initially mark them as `false` (not found in second array yet)

2. **Check Second Array**:
   - For each element in second array, check if it exists in hash map
   - If found, mark it as `true` (exists in both arrays)

3. **Collect Results**:
   - Iterate through hash map and collect all elements marked as `true`
   - These are the common elements present in both arrays

## Complexity Analysis

### Time Complexity: **O(n + m)**
- First pass through nums1: O(n)
- Second pass through nums2: O(m)
- Third pass through hash map: O(min(n, m))
- Total: O(n + m)

### Space Complexity: **O(n)**
- Hash map to store elements from first array: O(n)
- Result vector: O(min(n, m))

## Final Code with Comments

```cpp
class Solution {
public:
    vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
        unordered_map<int, bool> ans;
        
        // Store all elements from first array
        for(int i = 0; i < nums1.size(); i++){
            ans[nums1[i]] = false;  // Initially mark as not found in nums2
        }
        
        // Check elements from second array
        for(int j = 0; j < nums2.size(); j++){
            if(ans.find(nums2[j]) != ans.end()){
                ans[nums2[j]] = true;  // Mark as found in both arrays
            }
        }
        
        // Collect intersection results
        vector<int> res;
        for(auto [x, y] : ans){
            if(y == true){
                res.push_back(x);  // Add elements present in both arrays
            }
        }
        return res;
    }
};
