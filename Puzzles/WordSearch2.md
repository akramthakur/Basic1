# Word Search II - Trie + Backtracking Solution

## Problem Statement
Given an `m x n` board of characters and a list of words, return all words from the list that can be formed by sequentially adjacent cells (horizontal or vertical) on the board.

## Step-by-Step Logic

### Trie + Backtracking Approach:
1. **Trie Construction**: Build a trie from all words for efficient prefix search
2. **Board Exploration**: DFS from each cell to find matching words
3. **Backtracking**: Mark visited cells and restore after exploration
4. **Word Deduplication**: Remove found words from trie to avoid duplicates

## Algorithm Details

### Trie Structure:
- **child[26]**: Pointers to child nodes for each letter
- **word**: Stores complete word at terminal node (empty for non-terminal)

### Key Operations:
- **insert()**: Build trie by inserting each word
- **dfs()**: Explore board from current position using trie for guidance
- **Backtracking**: Use '#' to mark visited, restore original character

### Optimization Features:
- **Early Termination**: Stop when character not in trie
- **Prefix Pruning**: Trie prevents exploring dead-end paths
- **Word Removal**: Avoid duplicate findings by clearing word after discovery

## Complexity Analysis

### Time Complexity: **O(m × n × 4^L + W × L)**
- **Trie Construction**: O(W × L) where W = words count, L = average word length
- **Board DFS**: O(m × n × 4^L) where L = maximum word length
- **Practical**: Much faster due to trie pruning

### Space Complexity: **O(W × L + m × n)**
- **Trie Storage**: O(W × L) for all words
- **Recursion Stack**: O(L) for DFS depth
- **Board Modification**: O(1) auxiliary space

## Code with Detailed Comments

```cpp
struct Trie {
    Trie* child[26] = {};  // 26 pointers for each lowercase letter
    string word = "";      // Store complete word at leaf node
};

class Solution {
public:
    // Insert a word into the trie
    void insert(Trie* root, string& w) {
        for(char c : w) {
            if(!root->child[c - 'a']) {
                root->child[c - 'a'] = new Trie();
            }
            root = root->child[c - 'a'];
        }
        root->word = w;  // Mark end of word
    }
    
    // DFS to explore board and find words
    void dfs(vector<vector<char>>& board, long long i, long long j, 
             Trie* root, vector<string>& ans) {
        char c = board[i][j];
        
        // Check if current path is valid in trie
        if(c == '#' || !root->child[c - 'a']) return;
        
        // Move to next node in trie
        root = root->child[c - 'a'];
        
        // If we found a complete word, add to results and remove from trie
        if(!root->word.empty()) {
            ans.push_back(root->word);
            root->word = "";  // Prevent duplicates
        }
        
        // Mark current cell as visited
        board[i][j] = '#';
        
        int m = board.size();
        int n = board[0].size();
        
        // Explore all four directions
        if(i > 0) dfs(board, i - 1, j, root, ans);          // Up
        if(j > 0) dfs(board, i, j - 1, root, ans);          // Left
        if(i < m - 1) dfs(board, i + 1, j, root, ans);      // Down
        if(j < n - 1) dfs(board, i, j + 1, root, ans);      // Right
        
        // Backtrack: restore original character
        board[i][j] = c;
    }
    
    vector<string> findWords(vector<vector<char>>& board, vector<string>& words) {
        Trie* root = new Trie();
        vector<string> ans;
        
        // Build trie from all words
        for(auto& word : words) {
            insert(root, word);
        }
        
        // Start DFS from every cell in the board
        for(int i = 0; i < board.size(); i++) {
            for(int j = 0; j < board[0].size(); j++) {
                dfs(board, i, j, root, ans);
            }
        }
        
        return ans;
    }
};
