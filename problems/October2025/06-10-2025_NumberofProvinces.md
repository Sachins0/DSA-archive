# Number of Provinces (LeetCode)
Link: https://leetcode.com/problems/number-of-provinces/description/

Solution - 
## Approach 1: DFS
**Time Complexity**: O(n^2)
**Space Complexity**: O(n)
```C++
class Solution {
private:
    void DFS(vector<vector<int>>& isConnected, int i, 
    vector<bool> &visited, int n) {
        visited[i] = true;
        for(int j = 0; j < n; j++) {
            if(!visited[j] && isConnected[i][j] == 1)
                DFS(isConnected, j, visited, n);
        }
    }
public:
    int findCircleNum(vector<vector<int>>& isConnected) {
        int n = isConnected.size();
        int cnt = 0;
        vector<bool> visited(n, false);
        for(int i = 0; i < n; i++) {
            if(!visited[i]) {
                DFS(isConnected, i, visited, n);
                cnt++;
            }
        }
        return cnt;
    }
};

```

## Approach 2: Breadth First Search (BFS)
**Time Complexity**: O(n^2)
**Space Complexity**: O(n)
```C++
int findCircleNum(vector<vector<int>>& isConnected) {
    int n = isConnected.size();
    vector<bool> visited(n, false);
    queue<int> qu;
    int cnt = 0;

    for(int i = 0; i < n; i++) {
        if(!visited[i]) {
            qu.push(i);
            cnt++;
            while(!qu.empty()) {
                int curr = qu.front();
                qu.pop();
                visited[curr] = true;
                for(int j = 0; j < n; j++) {
                    if(!visited[j] && isConnected[curr][j] 
                                                        ==1) {
                        qu.push(j);
                    } 
                }
            }
        }
    }
    return cnt;
}

```

## Approach 3: Union-Find (Disjoint Set Union)
**Time Complexity**: O(n^2 * α(n))
**Space Complexity**: O(n)
```C++
class DisjointSet {
    vector<int> parent, rank;
public:
    DisjointSet(int n) {
        rank.resize(n);
        parent.resize(n, 0);
        for(int i = 0; i < n; i++) parent[i] = i;
    }
    int findUPar(int node) {
        if(node == parent[node]) return node;
        return parent[node] = findUPar(parent[node]);
    }
    void unionByRank(int u, int v) {
        int ulp = findUPar(u);
        int vlp = findUPar(v);
        if(ulp == vlp) return;
        if(rank[ulp] < rank[vlp]) parent[ulp] = vlp;
        else if(rank[ulp] > rank[vlp]) parent[vlp] = ulp;
        else {
            parent[vlp] = ulp;
            rank[ulp] ++;
        }
    }
    int countDistinctRoots() {
        int cnt = 0;
        for(int i = 0; i < parent.size(); i++) {
            if(parent[i] == i) cnt++;
        }
        return cnt;
    }
};

class Solution {
public:
    int findCircleNum(vector<vector<int>>& isConnected) {
        int n = isConnected.size();
        DisjointSet ds(n);
        for(int i = 0; i < n; i++) {
            for(int j = i+1; j < n; j++) {
                if(isConnected[i][j] == 1){
                    ds.unionByRank(i, j);
                }
            }
        }
        return ds.countDistinctRoots();
    }
};
```