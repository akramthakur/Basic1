# Bellman-Ford Algorithm - Shortest Path Solution

## Problem Statement
Given a weighted directed graph with `V` vertices and `E` edges, find the shortest distance from a source vertex to all other vertices. The graph may contain negative weight edges, and the algorithm should detect negative weight cycles.

## Step-by-Step Logic

### Bellman-Ford Algorithm Approach:
1. **Initialization**: Set source distance to 0, all others to infinity
2. **Relaxation**: Perform V-1 iterations relaxing all edges
3. **Negative Cycle Check**: One additional iteration to detect negative cycles
4. **Return**: Shortest distances or -1 if negative cycle detected

## Algorithm Details

### Relaxation Process:
- **V-1 Iterations**: Maximum possible edges in shortest path without cycles
- **Edge Relaxation**: `if(dist[u] + w < dist[v]) then dist[v] = dist[u] + w`
- **Negative Infinity**: Use large value (1e8) to represent infinity

### Negative Cycle Detection:
- **Additional Iteration**: If any distance can be improved in V-th iteration, negative cycle exists
- **Return Value**: `{-1}` if negative cycle detected

## Complexity Analysis

### Time Complexity: **O(V × E)**
- **V-1 Relaxation Passes**: O(V × E)
- **Negative Cycle Check**: O(E)
- **Total**: O(V × E)

### Space Complexity: **O(V)**
- **Distance Array**: O(V)
- **Auxiliary Space**: O(1)
- **Input Storage**: O(E) not counted in auxiliary

## Final Code with Comments

```cpp
class Solution {
public:
    vector<int> bellmanFord(int V, vector<vector<int>>& edges, int src) {
        // Initialize distances: 1e8 represents infinity
        vector<int> dist(V, 1e8);
        dist[src] = 0;
        
        // Relax all edges V-1 times
        for(int i = 0; i < V - 1; i++) {
            for(auto &edge : edges) {
                int u = edge[0];
                int v = edge[1];
                int w = edge[2];
                
                // Relax edge if we found a shorter path
                if(dist[u] != 1e8 && dist[u] + w < dist[v]) {
                    dist[v] = dist[u] + w;
                }
            }
        }
        
        // Check for negative weight cycles
        for(auto &edge : edges) {
            int u = edge[0];
            int v = edge[1];
            int w = edge[2];
            
            // If we can still relax an edge, negative cycle exists
            if(dist[u] != 1e8 && dist[u] + w < dist[v]) {
                return {-1};
            }
        }
        
        return dist;
    }
};
