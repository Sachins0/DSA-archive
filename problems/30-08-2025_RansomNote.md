# Ransom Note (LeetCode)
Link: https://leetcode.com/problems/ransom-note/description/

Solution - 
## Approach 1
```C++
bool canConstruct(string ransomNote, string magazine) {
    unordered_map<char, int> mp;
    for(char chars : magazine) mp[chars]++;
    for(auto chars : ransomNote) {
        if(mp[chars] <= 0) return false; 
        else mp[chars]--;
    }
    return true;
}
```

## Approach 2
```C++
bool canConstruct(string ransomNote, string magazine) {
    vector<int> cnt(26, 0);
    for(char chars : magazine) cnt[chars - 'a']++;
    for(auto chars : ransomNote) {
        if(cnt[chars - 'a'] <= 0) return false; 
        else cnt[chars - 'a']--;
    }
    return true;
}

```
