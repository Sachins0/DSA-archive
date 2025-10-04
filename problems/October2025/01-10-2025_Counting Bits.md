# Counting Bits (LeetCode)
Link: https://leetcode.com/problems/counting-bits/description/

Solution - 
## Approach 1
```C++
vector<int> countBits(int n) {
    if(n == 0) return {0};
    vector<int> ans(n+1);
    ans[0] = 0;
    for(int i = 1; i <= n; i++) {
        if(i%2 == 0) ans[i] = ans[i/2];
        else ans[i] = ans[i/2]+1;
    }
    return ans;
}
```