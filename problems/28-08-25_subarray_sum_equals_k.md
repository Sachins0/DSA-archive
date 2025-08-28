# Subarray Sum Equals K (LeetCode)
Link: https://leetcode.com/problems/subarray-sum-equals-k/description/

Solution - 
```C++
int subarraySum(vector<int>& nums, int k) {
    int cnt = 0, currSum = 0;
    unordered_map<int, int> mp;
    mp[0] = 1;
    for(int i = 0; i < nums.size(); i++) {
        currSum += nums[i];
        if(mp.find(currSum - k) != mp.end()) cnt += mp[currSum - k];
        mp[currSum]++;
    }
    return cnt;
}
```



