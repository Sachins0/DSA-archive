# Coin Change (LeetCode)
Link: https://leetcode.com/problems/coin-change/description/

Solution - 
## Brute Force Recursive Approach
- **Time Complexity**: Exponential — O(S^n), where S is the amount, and n is the number of different coins. 
- **Space Complexity**: O(S)
```C++
int coinUtil(vector<int>& coins, int amount, int i) {
    if(amount == 0) return 0;
    if(amount < 0 || i >= coins.size()) return 1e9;
    int takenAndStand = 1 + coinUtil(coins, amount - coins[i], i);
    int notTaken = coinUtil(coins, amount, i+1);
    return min(takenAndStand,notTaken);
}
int coinChange(vector<int>& coins, int amount) {
    int ans = coinUtil(coins, amount, 0);
    return  ans >= 1e9 ? -1 : ans ;
}
```

## Optimized Recursive Memoization
- **Time Complexity**: O(S*n)
- **Space Complexity**: O(S)
```C++
 vector<vector<int>> dp;
int coinUtil(vector<int>& coins, int amount, int i) {
    if(amount == 0) return 0;
    if(amount < 0 || i >= coins.size()) return 1e9;
    if(dp[i][amount] != -1) return dp[i][amount];
    int takenAndStand = 1 + coinUtil(coins, amount - coins[i], i);
    int notTaken = coinUtil(coins, amount, i+1);
    return dp[i][amount] = min(takenAndStand,notTaken);
}
int coinChange(vector<int>& coins, int amount) {
    int n = coins.size();
    dp.resize(n+1, vector<int>(amount+1, -1));
    int ans = coinUtil(coins, amount, 0);
    return  ans >= 1e9 ? -1 : ans ;
}
```

## Bottom-Up Dynamic Programming
- **Time Complexity**: O(S*n)
- **Space Complexity**: O(S)
```C++
int coinChange(vector<int>& coins, int amount) {
    int n = coins.size();
    vector<vector<int>> dp.resize(n+1, vector<int>(amount+1, 0));
    for(int j = 0; j <= amount; j++) dp[n][j] = 1e9;
    for(int i = n-1; i>= 0; i--) {
        for(int j = 1; j <= amount; j++) {
            int taken = 1e9;
            if(j >= coins[i]) taken = 1 + (dp[i][j - coins[i]]);
            int notTaken = dp[i+1][j];
            dp[i][j] = min(taken,notTaken);
        }
    }
    return  dp[0][amount] >= 1e9 ? -1 : dp[0][amount] ;
}
```
## Optimized Space for bottom up DP
- **Time Complexity**: O(S*n)
- **Space Complexity**: O(S)
```C++
int coinChange(vector<int>& coins, int amount) {
    int n = coins.size();
    dp.resize(amount+1, amount+1);
    dp[0] = 0;
    for(int i = 0; i <= amount; i++) {
        for(int coin : coins) {
            if(i - coin >= 0) dp[i] = min(dp[i], 1 + dp[i-coin]);
        }
    }
    return dp[amount] > amount ? -1 : dp[amount];
}

```