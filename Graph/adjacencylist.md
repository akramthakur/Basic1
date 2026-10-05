# Graph Adjacency List Representation - Solution

## Problem Statement
Given the number of vertices `V` and a list of edges, return the adjacency list representation of the undirected graph. The adjacency list should contain all adjacent vertices for each vertex in sorted order.

## Step-by-Step Logic

### Adjacency List Construction:
1. **Initialize**: Create empty adjacency list of size V
2. **Process Each Edge**: For each edge (u, v):
   - Add v to u's adjacency list
   - Add u to v's adjacency list (since graph is undirected)
3. **Return Result**: The completed adjacency list

## Complexity Analysis

### Time Complexity: **O(E)**
- **O(E)** for processing each edge exactly once
- **E** = number of edges in the graph
- **O(V + E log E)** if sorting is required per vertex

### Space Complexity: **O(V + E)**
- **O(V)** for the outer vector structure
- **O(E)** for storing all edges in adjacency lists
- Total space: **O(V + E)**

## Final Code with Comments

```cpp
class Solution {
public:
    // Function to return the adjacency list for each vertex.
    vector<vector<int>> printGraph(int V, vector<pair<int, int>>& edges) {
        // Initialize adjacency list with V empty vectors
        vector<vector<int>> adj(V);
        
        // Process each edge in the input
        for(int i = 0; i < edges.size(); i++) {
            int u = edges[i].first;
            int v = edges[i].second;
            
            // Add v to u's adjacency list (undirected edge)
            adj[u].push_back(v);
            
            // Add u to v's adjacency list (undirected edge)
            adj[v].push_back(u);
        }
        
        return adj;
    }
};
