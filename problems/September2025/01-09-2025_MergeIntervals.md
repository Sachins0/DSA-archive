# Merge Intervals (LeetCode)
Link: https://leetcode.com/problems/merge-intervals/description/

Solution - 
## Approach 1
```C++
vector<vector<int>> merge(vector<vector<int>>& intervals) {
    sort(intervals.begin(), intervals.end());
    vector<vector<int>> res;
    int i = 0;
    while(i < intervals.size()) {
        int start = intervals[i][0];
        int end = intervals[i][1];
        int j = i+1;
        while(j < intervals.size() && intervals[j][0] <= end) {
            end = max(end, intervals[j][1]);
            j++;
        }
        res.push_back({start, end});
        i = j;
    }
    return res;
}
```

## Optimized Approach
### Time Complexity: O(n logn) Space Complexity: O(n)
```C++
vector<vector<int>> merge(vector<vector<int>>& intervals) {
    sort(intervals.begin(), intervals.end());
    vector<vector<int>> res;
    res.push_back(intervals[0]);
    for(int i = 1; i < intervals.size(); i++) {
        int end = res.back()[1];
        if(intervals[i][0] <= end) 
            res.back()[1] = max(intervals[i][1], end);
        else res.push_back(intervals[i]);
    }
    return res;
}
```
