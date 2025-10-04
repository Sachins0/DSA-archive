# Minimum Window Substring (LeetCode)
Link: https://leetcode.com/problems/minimum-window-substring/description/

Solution - 
## Approach 1: Sliding Window - Brute Force
- Time Complexity: O((s.length)^2 * t.length)
- Space Complexity: O(t.length)
```C++
class Solution {
public:
    string minWindow(string s, string t) {
        if (s.empty() || t.empty()) return "";
        int minLength = INT_MAX;
        string result = "";

        for (int start = 0; start < s.length(); ++start) {
            unordered_map<char, int> map;
            for (char c : t) map[c]++;
            int end = start;
            while (end < s.length()) {
                if (map.find(s[end]) != map.end()) {
                    map[s[end]]--;
                    if (map[s[end]] == 0) map.erase(s[end]);
                }
                if (map.empty()) {
                    if (end - start + 1 < minLength) {
                        minLength = end - start + 1;
                        result = s.substr(start, minLength);
                    }
                    break; // try to move start to find shorter valid window
                }
                ++end;
            }
        }
        return result;
    }
};
```

## Approach 2: Sliding Window - Optimized with HashMaps
- Time Complexity: O(s.length + t.length)
 - Space Complexity: O(t.length) 
```C++
string minWindow(string s, string t) {
    int n = s.size(), m = t.size();
    int cnt = 0;
    int sIdx = -1, minLen = INT_MAX;
    int l = 0, r = 0;
    int freq[256] = {0};
    for(int i = 0; i < m; i++) freq[t[i]]++;
    while(r < n) {
        if(freq[s[r]] > 0) cnt++;
        freq[s[r]] --;
        while(cnt == m) {
            if(r - l + 1 < minLen) {
                minLen = r-l+1;
                sIdx = l;
            }
            freq[s[l]]++;
            if(freq[s[l]] > 0) cnt--;
            l++;
        }
        r++;
    }
    return sIdx == -1 ? "" : s.substr(sIdx, minLen);
}
```