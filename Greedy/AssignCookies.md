# Assign Cookies - Solution

## Problem Statement
Assume you are an awesome parent and want to give your children some cookies. But, you should give each child at most one cookie.

Each child `i` has a greed factor `g[i]`, which is the minimum size of a cookie that the child will be content with; and each cookie `j` has a size `s[j]`. If `s[j] >= g[i]`, we can assign the cookie `j` to the child `i`, and the child `i` will be content.

Your goal is to maximize the number of content children and output the maximum number.

## Step-by-Step Logic

### Algorithm:
1. **Sorting**: Sort both greed factors and cookie sizes in ascending order
2. **Two Pointers**: Use two pointers to match smallest sufficient cookie to each child
3. **Greedy Approach**: Always try to satisfy the least greedy child first with the smallest available cookie

### Key Insight:
- By sorting and using the smallest sufficient cookie for each child, we maximize the number of satisfied children
- If a cookie can satisfy a child, we should use it (no benefit in saving it for later)

## Complexity Analysis

### Time Complexity: **O(n log n + m log m)**
- Sorting greed array: O(n log n)
- Sorting cookies array: O(m log m)
- Two-pointer traversal: O(min(n, m))

### Space Complexity: **O(1)**
- Sorting may use O(log n) stack space, but no additional data structures

## Final Code with Comments

```cpp
class Solution {
public:
    int findContentChildren(vector<int>& g, vector<int>& s) {
        // Sort both arrays to use greedy approach
        sort(g.begin(), g.end());  // Sort children's greed factors
        sort(s.begin(), s.end());  // Sort cookie sizes
        
        int i = 0, j = 0;         // Two pointers
        int ans = 0;               // Count of content children
        
        // Try to assign cookies to children
        while (i < g.size() && j < s.size()) {
            // If current cookie can satisfy current child
            if (s[j] >= g[i]) {
                ans++;    // Child is content
                i++;      // Move to next child
            }
            j++;          // Move to next cookie (whether used or not)
        }
        
        return ans;
    }
};
