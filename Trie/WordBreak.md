# Word Break - Solution

## Problem Statement
Given a string `s` and a dictionary of words `wordDict`, determine if `s` can be segmented into a space-separated sequence of one or more dictionary words.

## Step-by-Step Logic

### Algorithm:
1. **Trie Construction**: Build a trie from the dictionary words for efficient prefix search
2. **DFS with Memoization**: Recursively check all possible segmentations
3. **Dynamic Programming**: Cache results to avoid recomputation

### Key Insight:
- Use trie for O(L) word lookups instead of O(N) dictionary scans
- Memoization prevents exponential time complexity
- Check all possible split points using DFS

## Complexity Analysis

### Time Complexity: **O(n² × L)**
- Trie operations: O(L) per word lookup
- DFS with memoization: O(n²) states
- Where n = string length, L = average word length

### Space Complexity: **O(n + M × L)**
- DP array: O(n)
- Trie: O(M × L) where M = dictionary size
- Recursion stack: O(n)

## Final Code with Comments

```cpp
struct Node {
    bool flag;          // Marks end of a word
    Node* child[26];    // Pointers to child nodes for a-z
    
    Node() {
        flag = false;
        for(auto &a : child) a = nullptr;  // Initialize all children to null
    }
};

class Trie {
private:
    Node* root;  // Root of the trie

public:
    Trie() {
        root = new Node();  // Initialize empty root node
    }
    
    void insert(string word) {
        Node* p = root;
        for(auto &a : word) {
            int i = a - 'a';  // Convert char to index (0-25)
            
            // Create new node if path doesn't exist
            if(!p->child[i]) {
                p->child[i] = new Node();
            }
            p = p->child[i];  // Move to next node
        }
        p->flag = true;  // Mark end of word
    }
    
    bool search(string word, bool prefix = false) {
        Node* p = root;
        for (auto &a : word) {
            if (a < 'a' || a > 'z') return false;  // safety guard
            int i = a - 'a';
            if (!p->child[i]) return false;
            p = p->child[i];
        }
        return prefix ? true : p->flag;
    }
    
    bool startsWith(string prefix) {
        return search(prefix, true);  // Reuse search with prefix flag
    }
};

// Helper function for DFS with memoization
bool solve(string& word, Trie &t, int start, vector<int> &dp) {
    // Base case: reached end of string
    if (word.size() == start) return true;
    
    // Return cached result if available
    if (dp[start] != -1) return dp[start];
    
    string curr = "";
    // Try all possible substrings starting from 'start'
    for (int i = start; i < word.size(); i++) {
        curr.push_back(word[i]);
        
        // If current substring is a valid word
        if (t.search(curr)) {
            // Recursively check the remaining string
            if (solve(word, t, i + 1, dp)) {
                return dp[start] = true;
            }
        }
    }
    
    // No valid segmentation found from this position
    return dp[start] = false;
}

class Solution {
public:
    bool wordBreak(string s, vector<string>& wordDict) {
        Trie t;
        int n = s.size();
        vector<int> dp(n + 1, -1);  // DP array: -1 = uncomputed, 0 = false, 1 = true
        
        // Build trie from dictionary
        for (int i = 0; i < wordDict.size(); i++) {
            t.insert(wordDict[i]);
        }
        
        return solve(s, t, 0, dp);
    }
};
