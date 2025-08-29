# Number of Islands (LeetCode)
Link: https://leetcode.com/problems/number-of-islands/description/

Solution - 
## Approach 1: DFS (Depth-First Search)
### Time Complexity: O(M * N) Space Complexity: O(M * N)
```C++
vector<vector<string>> groupAnagrams(vector<string>& strs) {
    unordered_map<string, vector<string>> mp;
    for(int i = 0; i < strs.size(); i++) {
        string sortStr = strs[i];
        sort(sortStr.begin(), sortStr.end());
        mp[sortStr].push_back(strs[i]);
    }
    vector<vector<string>> v;
    for(auto str : mp) {
        v.push_back(str.second);
    }
    return v;
}
```

## Approach 2: BFS (Breadth-First Search) Approach
### Time Complexity: O(M * N) Space Complexity: O(min(M * N))
```C++
vector<vector<string>> groupAnagrams(vector<string>& strs) {
    unordered_map<string, vector<string>> mp;
    for(int i = 0; i < strs.size(); i++) {
        vector<int> cnts(26, 0);
        for(char ch : strs[i]) cnts[ch - 'a']++;
        string key = "";
        for(int cnt : cnts) key += '#' + to_string(cnt);
        mp[key].push_back(strs[i]);
    }
    vector<vector<string>> v;
    for(auto str : mp) {
        v.push_back(str.second);
    }
    return v;
}
```
