# Row with Maximum Ones - Solution

## Problem Statement
Given a binary matrix, find the row index that has the maximum number of 1's, and the count of ones in that row. If multiple rows have the same maximum number of 1's, return the smallest row index.

## Step-by-Step Logic

1. **Count Ones in Each Row**:
   - Iterate through each row and count number of 1's
   - Store row index and count as pairs

2. **Custom Sorting**:
   - Sort rows by count in descending order
   - For same count, sort by row index in ascending order

3. **Return Result**:
   - Return the first element after sorting (row index and count)

## Complexity Analysis

### Time Complexity: **O(m × n + m log m)**
- Counting ones: O(m × n) where m = rows, n = columns
- Sorting: O(m log m) for m rows
- Total: O(m × n + m log m)

### Space Complexity: **O(m)**
- Additional vector to store (index, count) pairs: O(m)
- Sorting uses O(log m) stack space

## Final Code with Comments

```cpp
class Solution {
public:
    // Custom comparator for sorting
    static bool comp(pair<int, int>& a, pair<int, int>& b) {
        if (a.second != b.second)
            return a.second > b.second;  // Higher count first
        return a.first < b.first;        // Smaller index for same count
    }
    
    vector<int> rowAndMaximumOnes(vector<vector<int>>& mat) {
        vector<pair<int, int>> ans;
        
        // Count ones in each row
        for(int i = 0; i < mat.size(); i++) {
            int cnt = 0;
            for(int j = 0; j < mat[i].size(); j++) {
                if(mat[i][j] == 1)
                    cnt++;
            }
            ans.push_back({i, cnt});  // Store (row_index, count)
        }
        
        // Sort based on custom comparator
        sort(ans.begin(), ans.end(), comp);
       
        // Return row index and count of maximum ones
        return {ans[0].first, ans[0].second};
    }
};
