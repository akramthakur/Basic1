# Trie Implementation - Solution

## Problem Statement
Implement a Trie (prefix tree) with the following operations:
- `insert(word)`: Inserts a word into the trie
- `search(word)`: Returns true if the word is in the trie
- `startsWith(prefix)`: Returns true if there is any word in the trie that starts with the given prefix

## Step-by-Step Logic

### Data Structure Design:
1. **Node Structure**: Each node contains:
   - `flag`: Marks end of a word
   - `child[26]`: Array of pointers to child nodes (a-z)
2. **Trie Structure**: Root node with empty children

### Algorithm:
1. **Insert**: Traverse trie, creating nodes as needed, mark end node
2. **Search**: Traverse trie, check if word exists and ends at flagged node
3. **StartsWith**: Traverse trie, check if prefix exists (don't check end flag)

## Complexity Analysis

### Time Complexity:
- **Insert**: O(L) where L is word length
- **Search**: O(L) where L is word length  
- **StartsWith**: O(L) where L is prefix length

### Space Complexity: **O(N × L)**
- Where N is number of words and L is average word length
- Each character stores 26 pointers (constant factor)

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
        for(auto &a : word) {
            int i = a - 'a';
            if(!p->child[i]) return false;  // Path doesn't exist
            p = p->child[i];
        }
        
        // For prefix search, don't check end flag
        if(!prefix) {
            return p->flag;  // Check if this node marks a complete word
        }
        return true;  // Prefix exists
    }
    
    bool startsWith(string prefix) {
        return search(prefix, true);  // Reuse search with prefix flag
    }
};
