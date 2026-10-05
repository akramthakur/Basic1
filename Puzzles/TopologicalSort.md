# Topological Sort - DFS Solution

## Problem Statement
Given a Directed Acyclic Graph (DAG) with `V` vertices and `E` directed edges, return a topological ordering of its vertices.

## Step-by-Step Logic

### DFS-Based Approach:
1. **Graph Representation**: Convert edge list to adjacency list
2. **DFS Traversal**: Perform depth-first search on all unvisited nodes
3. **Stack Storage**: Push nodes to stack after visiting all neighbors (post-order)
4. **Result Construction**: Pop from stack to get topological order

## Algorithm Details

### Key Concepts:
- **Topological Order**: Linear ordering where for every directed edge u→v, u comes before v
- **Post-order DFS**: Process node after processing all its descendants
- **Stack Usage**: LIFO structure to reverse DFS finishing order

### Process Flow:
1. Mark current node as visited
2. Recursively visit all unvisited neighbors
3. Push current node to stack after processing all neighbors
4. Repeat for all unvisited nodes

## Complexity Analysis

### Time Complexity: **O(V + E)**
- **DFS Traversal**: O(V + E) for adjacency list
- **Stack Operations**: O(V) for push/pop operations
- **Total**: O(V + E)

### Space Complexity: **O(V)**
- **Visited Array**: O(V)
- **Adjacency List**: O(V + E)
- **Stack**: O(V)
- **Recursion Stack**: O(V) in worst case

## Final Code with Comments

```cpp
class Solution {
public:
    void dfs(int i, vector<int>& vis, vector<vector<int>>& adj, stack<int>& st) {
        vis[i] = 1;  // Mark current node as visited
        
        // Visit all unvisited neighbors
        for(auto it : adj[i]) {
            if(!vis[it]) {
                dfs(it, vis, adj, st);
            }
        }
        
        // Push current node to stack after processing all neighbors
        st.push(i);
    }
    
    vector<int> topoSort(int V, vector<vector<int>>& edges) {
        vector<int> vis(V, 0);  // Visited array
        vector<vector<int>> adj(V);  // Adjacency list
        
        // Build adjacency list from edges
        for(auto &e : edges) {
            adj[e[0]].push_back(e[1]);
        }
        
        stack<int> st;  // Stack to store topological order
        
        // Perform DFS on all unvisited nodes
        for(int i = 0; i < V; i++) {
            if(!vis[i]) {
                dfs(i, vis, adj, st);
            }
        }
        
        // Extract topological order from stack
        vector<int> ans;
        while(!st.empty()) {
            ans.push_back(st.top());
            st.pop();
        }
        
        return ans;
    }
};
