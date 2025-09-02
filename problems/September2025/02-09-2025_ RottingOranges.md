# Rotting Oranges (LeetCode)
Link: https://leetcode.com/problems/rotting-oranges/description/

Solution - 
```C++
int orangesRotting(vector<vector<int>>& grid) {
    int m = grid.size();
    int n = grid[0].size();
    queue<pair<int, int>> qu;
    int freshCnt = 0;
    int cnt = 0;
    for(int i = 0; i < m; i++) {
        for(int j = 0; j < n; j++) {
            if(grid[i][j] == 2) {
                qu.push({i, j});
            }else if(grid[i][j] == 1) freshCnt++;
        }
    }
    if(freshCnt == 0) return 0;
    int minutes = 0;
    vector<pair<int, int>> dirs = 
    {{0,1}, {0, -1}, {1, 0}, {-1, 0}};
    while(!qu.empty()) {
        bool rotted = false;
        int size = qu.size();
        for(int i = 0; i < size; i++) {
            auto node = qu.front();
            qu.pop();
            for(auto dir : dirs) {
                int nrow = node.first + dir.first;
                int ncol = node.second + dir.second;
                if(nrow >= 0 && nrow < m && ncol >= 0 &&
                ncol < n && grid[nrow][ncol] == 1) {
                    rotted = true;
                    grid[nrow][ncol] = 2;
                    qu.push({nrow, ncol});
                    freshCnt--;
                }
            }
        }
        if(rotted) minutes++;
    }
    return freshCnt == 0 ? minutes : -1;
}
```
