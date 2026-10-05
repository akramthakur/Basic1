# Prim's Algorithm - Minimum Spanning Tree Solution

## Problem Statement
Given a connected, undirected, and weighted graph with `V` vertices and `E` edges, find the minimum spanning tree (MST) weight using Prim's algorithm.

## Step-by-Step Logic

### Prim's Algorithm Approach:
1. **Graph Representation**: Convert edge list to adjacency list
2. **Priority Queue**: Min-heap to always add the smallest edge to MST
3. **Visited Array**: Track vertices already included in MST
4. **Greedy Selection**: At each step, add the minimum weight edge connecting MST to non-MST vertices

## Algorithm Details

### MST Construction:
- **Start**: From vertex 0 (any vertex works)
- **Process**: Add smallest edge connecting visited and unvisited vertices
- **Termination**: When all vertices are included in MST

### Key Operations:
- **Priority Queue**: Stores `{edge_weight, neighbor_vertex}`
- **Visited Tracking**: Prevents cycles and ensures tree property
- **Weight Accumulation**: Sum all selected edge weights

## Complexity Analysis

### Time Complexity: **O((V + E) log V)**
- **Priority Queue Operations**: O(log V) per insertion
- **Each Edge Considered Once**: O(E log V)
- **Each Vertex Processed Once**: O(V log V)
- **Total**: O((V + E) log V)

### Space Complexity: **O(V + E)**
- **Adjacency List**: O(V + E)
- **Visited Array**: O(V)
- **Priority Queue**: O(V)

## Final Code with Comments

```cpp
class Solution {
public:
    // Construct adjacency list from edge list
    vector<vector<pair<int, int>>> constructadj(int V, vector<vector<int>> &edges) {
        vector<vector<pair<int, int>>> adj(V);
        
        for(vector<int> &edge : edges) {
            int node1 = edge[0];
            int node2 = edge[1];
            int cost = edge[2];
            
            // Undirected graph: add edges in both directions
            adj[node1].push_back({node2, cost});
            adj[node2].push_back({node1, cost});
        }
        return adj;
    }
    
    int spanningTree(int V, vector<vector<int>>& edges) {
        // Build adjacency list representation
        vector<vector<pair<int, int>>> adjlist = constructadj(V, edges);
        
        // Min-heap priority queue: {edge_weight, vertex}
        priority_queue<pair<int, int>, vector<pair<int, int>>, 
                      greater<pair<int, int>>> pq;
        
        // Visited array to track vertices in MST
        vector<int> vis(V, 0);
        int sum = 0;  // Total weight of MST
        
        // Start from vertex 0 with weight 0
        pq.push({0, 0});
        
        while(!pq.empty()) {
            // Extract minimum weight edge
            auto it = pq.top();
            pq.pop();
            
            int node = it.second;
            int wt = it.first;
            
            // Skip if vertex already in MST
            if(vis[node] == 1) continue;
            
            // Add vertex to MST and accumulate weight
            vis[node] = 1;
            sum += wt;
            
            // Add all edges from current vertex to unvisited neighbors
            for(auto j : adjlist[node]) {
                int adjnode = j.first;
                int edW = j.second;
                
                if(!vis[adjnode]) {
                    pq.push({edW, adjnode});
                }
            }
        }
        
        return sum;
    }
};
