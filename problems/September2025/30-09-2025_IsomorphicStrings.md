# Isomorphic Strings (LeetCode)
Link: https://leetcode.com/problems/isomorphic-strings/description/

Solution - 
## Approach 1: Character Mapping Using Hashmaps
- Time Complexity
O(n)
- Space Complexity
O(m + n)
```C++
bool isIsomorphic(string s, string t) {
    int n = s.size();
    unordered_map<char,char> mp1;
    unordered_map<char,char> mp2;
    for(int i = 0; i < n; i++) {
        if(mp1.count(s[i]) && mp1[s[i]] != t[i]) return false;
        if(mp2.count(t[i]) && mp2[t[i]] != s[i]) return false;
        mp1[s[i]] = t[i];
        mp2[t[i]] = s[i];
    }
    return true;
}
```

## Approach 2: Single Pass with Two Maps
- Time Complexity
O(n)
- Space Complexity
O(1)
```C++
bool isIsomorphic(string s, string t) {
    int n = s.size();
    char mp1[256] = {0};
    char mp2[256] = {0};
    for(int i = 0; i < n; i++) {
        if(mp1[s[i]] == 0 && mp2[t[i]] == 0) {
            mp1[s[i]] = t[i];
            mp2[t[i]] = s[i];
        }
        else if(mp1[s[i]] != t[i] || mp2[t[i]] != s[i])
            return false;
    }
    return true;
}
```
