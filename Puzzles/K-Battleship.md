# Battleship Placement Problem - Solution

## Problem Statement
Given an `m × n` grid and a list of battleships with different attack ranges, determine if all battleships can be placed such that no ship is within attack range of another ship.

Each battleship has:
- `rowAttack`: Attack range in horizontal directions
- `columnAttack`: Attack range in vertical directions  
- `diagonalAttack`: Attack range in diagonal directions

## Step-by-Step Logic

### Algorithm:
1. **Backtracking with Pruning**: Try placing ships one by one
2. **Conflict Detection**: Mark attacked cells when placing a ship
3. **Optimization**: Sort ships by attack range (largest first)
4. **Backtracking**: Undo placements if they lead to dead ends

### Key Insight:
- Place ships with largest attack range first (most constrained)
- Use backtracking to explore all possible placements
- Efficiently mark/unmark attacked cells during exploration

## Complexity Analysis

### Time Complexity: **O((m × n)^k)**
- k = number of ships
- In worst case, exponential but heavily pruned

### Space Complexity: **O(m × n)**
- Attacked grid of size m × n
- Recursion stack: O(k)

## Code Analysis with Comments

```cpp
#include <bits/stdc++.h>
using namespace std;

struct BattleShip {
    int rowAttack;      // Horizontal attack range
    int columnAttack;   // Vertical attack range  
    int diagonalAttack; // Diagonal attack range
};

// Mark/Unmark attacked cells for a ship placement
vector<pair<int, int>> markAttacks(int r, int c, BattleShip ship, 
                                  vector<vector<bool>>& attacked, bool set, int m, int n) {
    vector<pair<int, int>> change;
    
    // Mark the ship's position itself
    attacked[r][c] = set;
    change.push_back({r, c});
    
    // 8 directions: right, down, up, left, and 4 diagonals
    int dr[8] = {0, 1, -1, 0, 1, -1, 1, -1};
    int dc[8] = {1, 0, 0, -1, 1, -1, -1, 1};
    int range[8] = {ship.rowAttack, ship.columnAttack, ship.columnAttack, ship.rowAttack,
                   ship.diagonalAttack, ship.diagonalAttack, ship.diagonalAttack, ship.diagonalAttack};
    
    // Mark attack range in all directions
    for (int dir = 0; dir < 8; dir++) {
        for (int step = 1; step <= range[dir]; step++) {
            int nr = r + dr[dir] * step;
            int nc = c + dc[dir] * step;
            
            // Check bounds and if cell is already attacked
            if (nr >= 0 && nr < m && nc >= 0 && nc < n && !attacked[nr][nc]) {
                attacked[nr][nc] = set;
                change.push_back({nr, nc});
            }
        }
    }
    return change;
}

// Backtracking function to place ships
bool placeShip(int ind, vector<BattleShip>& ships, vector<vector<bool>>& attacked, int m, int n) {
    // Base case: all ships placed successfully
    if (ind == (int)ships.size())
        return true;
    
    BattleShip ship = ships[ind];
    
    // Try all possible positions
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            if (!attacked[i][j]) {  // Cell is safe
                // Mark attacked cells for this placement
                auto change = markAttacks(i, j, ship, attacked, true, m, n);
                
                // Recurse for next ship
                if (placeShip(ind + 1, ships, attacked, m, n))
                    return true;
                
                // Backtrack: unmark attacked cells
                for (auto& cell : change) {
                    attacked[cell.first][cell.second] = false;
                }
            }
        }
    }
    return false;
}

// Main function to check if placement is possible
bool isPossible(int m, int n, vector<BattleShip>& ships) {
    // Early check: more ships than cells
    if ((int)ships.size() > m * n) return false;
    
    // Optimization: sort ships by total attack range (largest first)
    sort(ships.begin(), ships.end(), [](const BattleShip& a, const BattleShip& b) {
        int totalA = a.rowAttack + a.columnAttack + a.diagonalAttack;
        int totalB = b.rowAttack + b.columnAttack + b.diagonalAttack;
        return totalA > totalB;  // Place most constraining ships first
    });
    
    // Initialize attacked grid
    vector<vector<bool>> attacked(m, vector<bool>(n, false));
    
    return placeShip(0, ships, attacked, m, n);
}
