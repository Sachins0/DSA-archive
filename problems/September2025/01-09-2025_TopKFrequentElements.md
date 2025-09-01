# Top K Frequent Elements (LeetCode)
Link: https://leetcode.com/problems/top-k-frequent-elements/description/
Solution - 
## Naive Approach: Sorting with a Frequency Map
### Time Complexity: O(N log N) Space Complexity: O(N)
```C++

vector<int> topKFrequent(std::vector<int>& nums, int k) {
    unordered_map<int, int> frequencyMap;
    for (int num : nums) {
        frequencyMap[num]++;
    }
    vector<pair<int, int>> freqVec(frequencyMap.begin(), frequencyMap.end());
    sort(freqVec.begin(), freqVec.end(), [](const pair<int, int>& a, const pair<int, int>& b) {
        return a.second > b.second;
    });
    vector<int> result;
    for (int i = 0; i < k; ++i) {
        result.push_back(freqVec[i].first);
    }

    return result;
}
```

## Optimized Approach: Using a Min-Heap (Priority Queue)
### Time Complexity: O(N log k) Space Complexity: O(N + k)
```C++
vector<int> topKFrequent(vector<int>& nums, int k) {
    unordered_map<int, int> mp;
    for(int ele : nums) mp[ele]++;
    priority_queue<pair<int,int>, vector<pair<int, int>>,
        greater<pair<int, int>>> pq;
    for(auto ele : mp) {
        pq.push({ele.second, ele.first});
        if(pq.size() > k) pq.pop();
    }
    vector<int> ans;
    while(!pq.empty()) {
        ans.push_back(pq.top().second);
        pq.pop();
    }
    return ans;
}
```
## Optimal Approach: Bucket Sort
### Time Complexity: O(N) Space Complexity: O(N)
```C++
vector<int> topKFrequent(vector<int>& nums, int k) {
    unordered_map<int, int> mp;
    for(int ele : nums) mp[ele]++;
    vector<vector<int>> freq(nums.size()+1);
    for(auto ele : mp) {
        freq[ele.second].push_back(ele.first);
    }
    vector<int> ans;
    for(int i = freq.size() - 1; i >= 0 && ans.size() < k; i--) {
        for(int nums : freq[i]) {
            ans.push_back(nums);
            if(ans.size() == k) break;
        }
    }
    return ans;
}
```
