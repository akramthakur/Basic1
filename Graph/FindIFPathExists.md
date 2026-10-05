# Find if Path Exists in Graph - Solution

## Problem Statement
Given an undirected graph with `n` vertices and a list of edges, determine if there is a valid path from vertex `source` to vertex `destination`.

## Step-by-Step Logic

### Algorithm:
1. **Graph Construction**: Build adjacency list representation from edge list
2. **BFS Traversal**: Use breadth-first search to explore reachable vertices from source
3. **Path Checking**: If destination is reached during BFS, path exists

### Key Insight:
- In an undirected graph, if there's a path from source to destination, BFS will find it
- BFS is optimal for finding shortest paths in unweighted graphs

## Complexity Analysis

### Time Complexity: **O(V + E)**
- Building adjacency list: O(E)
- BFS traversal: O(V + E)

### Space Complexity: **O(V + E)**
- Adjacency list: O(E)
- Visited array: O(V)
- Queue: O(V)

## Final Code with Comments

```cpp
class Solution {
public:
    // Helper function to build adjacency list from edges
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
    
    bool validPath(int n, vector<vector<int>>& edges, int source, int destination) {
        // Early return if source and destination are same
        if(source == destination) return true;
        
        // Build graph adjacency list
        vector<vector<int>> adj = printGraph(n, edges);
        
        // BFS initialization
        vector<int> vis(n, 0);  // Visited array
        queue<int> q;           // BFS queue
        
        // Start BFS from source
        q.push(source);
        vis[source] = 1;

        while (!q.empty()) {
            int node = q.front();
            q.pop();

            // Check if we reached destination
            if (node == destination) return true;

            // Explore all neighbors
            for (auto neighbor : adj[node]) {
                if (!vis[neighbor]) {
                    vis[neighbor] = 1;
                    q.push(neighbor);
                }
            }
        }

        return false;  // Destination not reachable
    }
};
