# Number of 1 Bits (LeetCode)
Link: https://leetcode.com/problems/number-of-1-bits/description/

Solution - 
## Approach 1: Brute Force Approach
**Time Complexity**: O(1)

**Space Complexity**: O(1)
```C++
int hammingWeight(int n) {
    int cnt = 0;
    while(n > 1) {
        cnt += n&1; // if(n %2 == 1) cnt+=1;
        n = n >> 1; // n /= 2;
    }
    if(n == 1) cnt += 1;
    return cnt;
}
```

## Approach 2 : Optimized Approach: Brian Kernighan's Algorithm
- **Time Complexity**: O(k)  where k is the number of '1' bits.
- **Space Complexity**: O(1)
```C++
int hammingWeight(int n) {
    int cnt = 0;
    while(n) {
        n = n &(n-1);
        cnt++;
    }
    return cnt;
}
```
## Approach 2 : STL
```C++
int hammingWeight(int n) {
    return __builtin_popcount(n);
}

```
