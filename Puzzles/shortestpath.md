# Shortest Path in Binary Grid - Solution

## Problem Statement
Given a binary grid where `1` represents traversable cells and `0` represents obstacles, find the shortest path from source to destination. Movement is allowed only in 4 directions (up, down, left, right).

## Step-by-Step Logic

### Dijkstra's Algorithm Approach:
1. **Priority Queue**: Min-heap to always expand the shortest path first
2. **Distance Array**: Track shortest distance to each cell from source
3. **Neighbor Exploration**: Check all 4-directional neighbors
4. **Obstacle Handling**: Only traverse through cells with value `1`

## Algorithm Details

### Initialization
- Set source distance to `0`, all others to `INT_MAX`
- Push source `(0, {src_x, src_y})` to priority queue

### Processing
- Extract cell with minimum distance from queue
- If destination reached, return distance
- For each valid neighbor:
  - Check bounds and traversability (`grid[nr][nc] == 1`)
  - If new distance is smaller, update and push to queue

## Complexity Analysis

### Time Complexity: **O(n × m × log(n × m))**
- Each cell processed once: `O(n × m)`
- Priority queue operations: `O(log(n × m))` per operation
- Total: `O(n × m × log(n × m))`

### Space Complexity: **O(n × m)**
- Distance matrix: `n × m`
- Priority queue: up to `n × m` elements

## Final Code with Comments

```cpp
class Solution {
public:
    int shortestPath(vector<vector<int>> &grid, pair<int, int> source,
                     pair<int, int> destination) {
        int n = grid.size();
        int m = grid[0].size();
        
        // Direction vectors for 4-directional movement
        int delRow[] = {-1, 0, 1, 0};  // up, left, down, right
        int delCol[] = {0, -1, 0, 1};
        
        // Distance matrix initialized to infinity
        vector<vector<int>> dist(n, vector<int>(m, INT_MAX));
        dist[source.first][source.second] = 0;
        
        // Min-heap priority queue: {distance, {row, col}}
        priority_queue<pair<int, pair<int, int>>, 
                      vector<pair<int, pair<int, int>>>,
                      greater<pair<int, pair<int, int>>>> pq;
        
        pq.push({0, {source.first, source.second}});
        
        while(!pq.empty()) {
            int distance = pq.top().first;
            int r = pq.top().second.first;
            int c = pq.top().second.second;
            pq.pop();
            
            // If destination reached, return shortest distance
            if(r == destination.first && c == destination.second) {
                return distance;
            }
            
            // Explore all 4 neighbors
            for(int i = 0; i < 4; i++) {
                int nr = r + delRow[i];
                int nc = c + delCol[i];
                
                // Check bounds, traversability and better path
                if(nr >= 0 && nc >= 0 && nr < n && nc < m && 
                   grid[nr][nc] == 1 && distance + 1 < dist[nr][nc]) {
                   
                    dist[nr][nc] = distance + 1;
                    pq.push({dist[nr][nc], {nr, nc}});
                }
            }
        }
        
        // Destination not reachable
        return -1;
    }
};
