# Climbing Stairs (LeetCode)
Link: https://leetcode.com/problems/climbing-stairs/description/

Solution - 
## Approach 1: Recursion
### Time Complexity: O(2^n) Space Complexity: O(n)
```C++
int climbStairs(int n) {
    if (n <= 1) return 1;
    return climbStairs(n - 1) + climbStairs(n - 2);
}
```

## Approach 2: Recursion with Memorization
### Time Complexity: O(n) Space Complexity: O(n)
```C++
int climbStairsMemo(int n, unordered_map<int, int>& memo) {
    if (memo.find(n) != memo.end()) return memo[n];
    if (n <= 1) return 1;
    memo[n] = climbStairsMemo(n - 1, memo) + climbStairsMemo(n - 2, memo);
    return memo[n];
}

int climbStairs(int n) {
    unordered_map<int, int> memo;
    return climbStairsMemo(n, memo);
}
```
## Approach 3: Dynamic Programming
### Time Complexity: O(n) Space Complexity: O(n)
```C++
int climbStairs(int n) {
    if (n <= 1) return 1;
    vector<int> dp(n + 1);
    dp[0] = 1; 
    dp[1] = 1;
    
    for (int i = 2; i <= n; ++i) {
        dp[i] = dp[i - 1] + dp[i - 2];
    }
    
    return dp[n];
}
```

## Approach 4: Space opti
### Time Complexity: O(n) Space Complexity: O(1)
```C++
int climbStairs(int n) {
    int prev1 = 1;
    int prev2 = 1;
    int next = 0;
    for(int i = 2; i <= n; i++) {
        next = prev1 + prev2;
        prev2 = prev1;
        prev1 = next;
    }
    return prev1;
}
```

## Approach 5: Fibonacci Formula Approach
### Time Complexity: O(1) Space Complexity: O(1)
```C++
int climbStairs(int n) {
    // Golden ratio
    double sqrt5 = sqrt(5);
    double phi = (1 + sqrt5) / 2;
    double psi = (1 - sqrt5) / 2;
    
    // Using Binet's formula for Fibonacci numbers
    return round((pow(phi, n+1) - spow(psi, n+1)) / sqrt5);
}
```