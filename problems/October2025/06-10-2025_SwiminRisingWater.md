# Swim in Rising Water (LeetCode)
Link: https://leetcode.com/problems/swim-in-rising-water/description/   

Solution - 
## Approach 1: Brute Force BFS
**Time Complexity**: O(n^3)
**Space Complexity**: O(n^2)
```C++
class Solution {
private:
    bool canReach(vector<vector<int>>& grid, int threshold) {
        if (grid[0][0] > threshold) return false;
        int n = grid.size();
        vector<vector<bool>> visited(n, vector<bool>(n, false));
        queue<pair<int, int>> q;
        q.push({0, 0});
        visited[0][0] = true;
        int directions[4][2] = {{1, 0}, {-1, 0}, {0, 1}, {0, -1}};
        while (!q.empty()) {
            auto [x, y] = q.front();
            q.pop();
            if (x == n - 1 && y == n - 1) return true;

            for (auto& dir : directions) {
                int nx = x + dir[0], ny = y + dir[1];
                if (nx >= 0 && ny >= 0 && nx < n && ny < n &&   
                !visited[nx][ny] && grid[nx][ny] <= threshold) {
                    visited[nx][ny] = true;
                    q.push({nx, ny});
                }
            }
        }
        return false;
    }
public:
    int swimInWater(vector<vector<int>>& grid) {
        int n = grid.size();
        for(int t = 0; t < n*n; t++) {
            if(canReach(grid, t)) return t;
        }
        return -1;
    }
};
```

## Approach 2: Min-Heap / Dijkstra-like Approach
**Time Complexity**: O(n^2 logn)
**Space Complexity**: O(n^2)
```C++
int swimInWater(vector<vector<int>>& grid) {
    int n = grid.size();
    priority_queue<tuple<int, int, int>, vector<tuple<int,int,
    int>>, greater<tuple<int,int,int>>> pq;
    pq.emplace(grid[0][0], 0, 0);
    vector<vector<bool>> visited(n, vector<bool>(n, false));
    visited[0][0] = true;
    int directions[4][2] = {{1, 0}, {-1, 0}, {0, 1}, {0, -1}};
    while (!pq.empty()) {
        auto [max_elevation, x, y] = pq.top();
        pq.pop();

        if (x == n - 1 && y == n - 1) {
            return max_elevation;
        }

        for (auto& dir : directions) {
            int nx = x + dir[0], ny = y + dir[1];
            if (nx >= 0 && ny >= 0 && nx < n && ny < n && !visited[nx][ny]) {
                visited[nx][ny] = true;
                pq.emplace(max(max_elevation, grid[nx][ny]), nx, ny);
            }
        }
    }
    return -1;
}
```