# Dijkstra's Algorithm - Shortest Path Solution

## Problem Statement
Given a weighted undirected graph with `V` vertices and `E` edges, find the shortest distance from a source vertex to all other vertices using Dijkstra's algorithm.

## Step-by-Step Logic

### Dijkstra's Algorithm Approach:
1. **Graph Representation**: Convert edge list to adjacency list
2. **Priority Queue**: Min-heap to always expand the closest vertex
3. **Distance Array**: Track shortest known distance to each vertex
4. **Relaxation**: Update distances when shorter paths are found

## Algorithm Details

### Graph Construction:
- **Adjacency List**: `vector<vector<pair<int, int>>>`
- **Each Entry**: `{neighbor_vertex, edge_weight}`
- **Undirected**: Add edges in both directions

### Dijkstra's Process:
1. **Initialize**: Source distance = 0, all others = ∞
2. **Priority Queue**: Push `{0, source}`
3. **Extract Min**: Get vertex with smallest known distance
4. **Relax Edges**: Update distances for all neighbors
5. **Skip Processed**: Ignore if extracted distance > current known distance

## Complexity Analysis

### Time Complexity: **O((V + E) log V)**
- **Priority Queue Operations**: O(log V) per insertion/extraction
- **Each Edge Processed Once**: O(E log V)
- **Each Vertex Processed Once**: O(V log V)
- **Total**: O((V + E) log V)

### Space Complexity: **O(V + E)**
- **Adjacency List**: O(V + E)
- **Distance Array**: O(V)
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
    
    vector<int> dijkstra(int V, vector<vector<int>> &edges, int src) {
        // Build adjacency list representation
        vector<vector<pair<int, int>>> adj = constructadj(V, edges);
        
        // Min-heap priority queue: {distance, vertex}
        priority_queue<pair<int, int>, vector<pair<int, int>>, 
                      greater<pair<int, int>>> pq;
        
        // Distance array initialized to infinity
        vector<int> dist(V, INT_MAX);
        
        // Initialize source vertex
        dist[src] = 0;
        pq.push({0, src});
        
        while(!pq.empty()) {
            // Extract vertex with minimum distance
            pair<int, int> k = pq.top();
            pq.pop();
            
            int cost = k.first;    // Current distance to this vertex
            int node = k.second;   // Current vertex
            
            // Skip if we found a better path after this was added to queue
            if(cost > dist[node]) continue;
            
            // Relax all outgoing edges
            for(auto &edge : adj[node]) {
                int neighbor = edge.first;
                int weight = edge.second;
                
                // If shorter path found, update and push to queue
                if(cost + weight < dist[neighbor]) {
                    dist[neighbor] = cost + weight;
                    pq.push({dist[neighbor], neighbor});
                }
            }
        }
        
        return dist;
    }
};
