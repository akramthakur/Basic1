# Number of Connected Components - Solution

## Problem Statement
Given an undirected graph with `n` nodes and a list of edges, return the number of connected components in the graph.

## Step-by-Step Logic

### Connected Components Algorithm:
1. **Build Adjacency List**: Convert edge list to adjacency list representation
2. **DFS Traversal**: 
   - Start DFS from unvisited nodes
   - Each complete DFS traversal covers one connected component
3. **Count Components**: 
   - Increment counter for each new DFS start
   - All nodes reachable from start belong to same component
4. **Return Count**: Total number of connected components

## Complexity Analysis

### Time Complexity: **O(V + E)**
- **O(E)** for building adjacency list
- **O(V + E)** for DFS traversal of all components
- **V** = number of vertices, **E** = number of edges

### Space Complexity: **O(V + E)**
- **O(V + E)** for adjacency list storage
- **O(V)** for visited array
- **O(V)** for recursion stack in worst case

## Final Code with Comments

```cpp
class Solution {
public:
    // Helper function to build adjacency list from edge list
    vector<vector<int>> printGraph(int V, vector<vector<int>>& edges) {
        // Initialize adjacency list with V empty vectors
        vector<vector<int>> adj(V);
        
        // Process each edge in the input
        for(int i = 0; i < edges.size(); i++) {
            int u = edges[i][0];
            int v = edges[i][1];
            
            // Add v to u's adjacency list (undirected edge)
            adj[u].push_back(v);
            
            // Add u to v's adjacency list (undirected edge)
            adj[v].push_back(u);
        }
        
        return adj;
    }

    // DFS helper function to traverse connected component
    void dfss(int start, vector<vector<int>> &adj, vector<int>& vis) {
        vis[start] = 1;  // Mark current node as visited
        
        // Visit all adjacent vertices
        for(auto it : adj[start]) {
            if(!vis[it]) {
                dfss(it, adj, vis);  // Recursively visit unvisited neighbors
            }
        }
    }
    
    int countComponents(int n, vector<vector<int>>& edges) {
        // Build adjacency list from edges
        vector<vector<int>> adj = printGraph(n, edges);
        
        // Visited array to track visited vertices
        vector<int> vis(n, 0);
        
        int ans = 0;  // Counter for connected components
        
        // Iterate through all vertices
        for(int i = 0; i < n; i++) {
            // If vertex not visited, it's a new component
            if(!vis[i]) {
                // Perform DFS to mark entire component
                dfss(i, adj, vis);
                ans++;  // Increment component count
            }
        }
        
        return ans;
    }
};
