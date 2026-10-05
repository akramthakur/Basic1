# Word Break II - Solution

## Problem Statement
Given a dictionary of words and a string, break the string into all possible space-separated sequences of dictionary words. Return all such possible sentences.

## Step-by-Step Logic

### Dynamic Programming Approach:
1. **State Definition**: `dp[i]` stores all valid sentences that can be formed from index `i` to end of string
2. **Base Case**: `dp[n] = {""}` (empty string at the end)
3. **Recurrence**: For each position `i`, check all substrings `s[i:j]`
   - If substring is in dictionary, combine with sentences from `dp[j]`
4. **Result**: `dp[0]` contains all valid sentences starting from beginning

## Algorithm Details

### DP Table Construction:
- **Bottom-up**: Process from end of string to beginning
- **Substring Check**: For each `i`, check all `j` from `i+1` to `n`
- **Sentence Building**: Combine valid words with previously built sentences

### Key Operations:
- **Dictionary Lookup**: O(1) using unordered_set
- **Substring Extraction**: O(n) in worst case
- **Sentence Construction**: Append words with spaces

## Complexity Analysis

### Time Complexity: **O(n³ × 2^n)**
- **n³**: Three nested loops (i, j, and substring operations)
- **2^n**: In worst case, exponential number of valid sentences
- **Practical**: Much better due to dictionary constraints

### Space Complexity: **O(n × 2^n)**
- **DP Table**: Stores all possible sentences
- **Dictionary**: O(m) where m = dictionary size
- **Output**: Exponential in worst case

## Final Code with Comments

```cpp
class Solution {
public:
    vector<string> wordBreak(vector<string> &dict, string &s) {
        // Convert dictionary to a set for fast lookups
        unordered_set<string> st(dict.begin(), dict.end());
        
        int n = s.length();
        
        // dp[i] stores all valid sentences starting from index i
        vector<vector<string>> dp(n + 1);
        
        // Base case: an empty string at the end
        dp[n] = {""};
        
        // Process from end to beginning
        for (int i = n - 1; i >= 0; --i) {
            // Check all substrings starting from current index
            for (int j = i + 1; j <= n; ++j) {
                string word = s.substr(i, j - i);
                
                // If word is in dictionary and we can form sentences from j
                if (st.count(word) && !dp[j].empty()) {
                    // Append valid sub-sentences to the current word
                    for (string &sub : dp[j]) {
                        if (sub.empty()) {
                            // No more words after this one
                            dp[i].push_back(word);
                        } else {
                            // Combine current word with following sentence
                            dp[i].push_back(word + " " + sub);
                        }
                    }
                }
            }
        }
        
        return dp[0];
    }
};
