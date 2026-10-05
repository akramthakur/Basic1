# Activity Selection - Solution

## Problem Statement
Given two arrays `start[]` and `finish[]` representing starting and finishing times of activities, find the maximum number of activities that can be performed by a single person, assuming a person can only work on a single activity at a time.

## Step-by-Step Logic

### Algorithm:
1. **Sort by Finish Time**: Sort activities based on their finishing times
2. **Greedy Selection**: Always pick the next activity that finishes earliest and doesn't conflict with previously selected activities
3. **Conflict Check**: An activity can be selected if its start time is after the finish time of the last selected activity

### Key Insight:
- Selecting the activity that finishes earliest leaves maximum time for remaining activities
- This greedy choice leads to the optimal solution

## Complexity Analysis

### Time Complexity: **O(n log n)**
- Sorting activities: O(n log n)
- Single pass through sorted activities: O(n)

### Space Complexity: **O(n)**
- Storing activities as pairs: O(n)
- Could be O(1) if we sort indices instead

## Final Code with Comments

```cpp
class Solution {
  public:
    int activitySelection(vector<int> &start, vector<int> &finish) {
        int n = start.size();
        vector<pair<int, int>> activities;
        
        // Create pairs of (finish_time, start_time)
        for (int i = 0; i < n; i++) {
            activities.push_back({finish[i], start[i]});
        }
        
        // Sort activities by finish time
        sort(activities.begin(), activities.end());
        
        int count = 0;      // Count of selected activities
        int last_finish = -1; // Finish time of last selected activity
        
        for (int i = 0; i < n; i++) {
            // If current activity starts after last activity finishes
            if (activities[i].second > last_finish) {
                count++;
                last_finish = activities[i].first; // Update last finish time
            }
        }
        
        return count;
    }
};
