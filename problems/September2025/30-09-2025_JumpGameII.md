# Jump Game II (LeetCode)
Link: https://leetcode.com/problems/jump-game-ii/description/

Solution - 
## Approach 1: Greedy Algorithm
- Time Complexity: O(n)
 - Space Complexity: O(1)
```C++
int jump(vector<int>& nums) {
    int cnt = 0;
    int currEnd = 0;
    int farthest = 0;
    for(int i = 0; i < nums.size()-1; i++) {
        farthest = max(farthest, i+nums[i]);
        if(i == currEnd) {
            cnt++;
            currEnd = farthest;
            if(currEnd >= nums.size()-1) break;
        }
    }
    return cnt;
}
```