# Asteroid Collision - Solution

## Problem Statement
We are given an array `asteroids` representing asteroids in a row. For each asteroid:
- Absolute value represents its size
- Sign represents its direction (positive = right, negative = left)
- Asteroids moving in the same direction never meet
- When two asteroids meet, the smaller one explodes
- If both are same size, both explode

Return the state of the asteroids after all collisions.

## Step-by-Step Logic

1. **Stack-based Simulation**:
   - Use stack to simulate asteroid collisions
   - Process asteroids from left to right

2. **Collision Rules**:
   - **Right-moving (positive)**: Always push to stack (no collision with previous rights)
   - **Left-moving (negative)**: Can collide with right-moving asteroids on stack

3. **Collision Handling**:
   - While top of stack is right-moving and smaller than current left asteroid: pop (smaller explodes)
   - If top equals current asteroid: both explode (pop and skip current)
   - If top is larger: current asteroid explodes (don't push)
   - If stack empty or top is left-moving: push current asteroid

## Complexity Analysis

### Time Complexity: **O(n)**
- Each asteroid pushed and popped at most once
- Each operation O(1) amortized

### Space Complexity: **O(n)**
- Stack storage in worst case (no collisions)
- Output vector

## Final Code with Comments

```cpp
class Solution {
public:
    vector<int> asteroidCollision(vector<int>& asteroids) {
        stack<int> st;
        int n = asteroids.size();
        
        for(int i = 0; i < n; i++) {
            int a = asteroids[i];
            
            if(a > 0) {
                // Right-moving asteroid - no collision with previous rights
                st.push(a);
            } else { 
                // Left-moving asteroid - may collide with rights on stack
                
                // Destroy all smaller right-moving asteroids
                while(!st.empty() && st.top() > 0 && st.top() < -a) {
                    st.pop();
                }
                
                // Handle equal size collision
                if(!st.empty() && st.top() == -a) {
                    st.pop(); // Both explode
                } 
                // Push left-moving asteroid if no collision or destroyed all smaller
                else if(st.empty() || st.top() < 0) {
                    st.push(a);
                }
                // Else: current asteroid destroyed (do nothing)
            }
        }

        // Convert stack to result vector
        vector<int> ans;
        while(!st.empty()) {
            ans.push_back(st.top());
            st.pop();
        }
        reverse(ans.begin(), ans.end());
        return ans;
    }
};
