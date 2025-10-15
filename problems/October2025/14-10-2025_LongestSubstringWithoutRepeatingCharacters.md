# Longest Substring Without Repeating Characters (LeetCode)
Link: https://leetcode.com/problems/longest-substring-without-repeating-characters/description/
Solution - 
## Approach 1: Brute Force
**Time Complexity**: O(n^3)
**Space Complexity**: O(n)
```C++
int lengthOfLongestSubstring(string s) {
    int maxLength = 0;
    
    // Step through all possible starting points of substrings
    for (int i = 0; i < s.size(); ++i) {
        unordered_set<char> seenChars;
        
        // Explore each possible substring starting at position i
        for (int j = i; j < s.size(); ++j) {
            // Check if the character is already seen
            if (seenChars.find(s[j]) != seenChars.end()) {
                break;
            }
            seenChars.insert(s[j]);
            maxLength = max(maxLength, j - i + 1);
        }
    }
    return maxLength;
}
```

## Approach 2: Sliding Window
**Time Complexity**: O(n)
**Space Complexity**: O(min(n,m))
```C++
int lengthOfLongestSubstring(string s) {
    int start = 0;
    unordered_set<char> st;
    int maxLen = 0;
    for(int end = 0; end < s.size(); end++) {
        while(st.find(s[end]) != st.end()) st.erase(s[start++]);
        st.insert(s[end]);
        maxLen = max(maxLen, end-start+1);
    }
    return maxLen;
}
```

## Approach 3: Optimized Sliding Window with Hash Map
**Time Complexity**: O(n)
**Space Complexity**: O(min(n,m))
```C++
int lengthOfLongestSubstring(string s) {
    int start = 0;
    unordered_map<char, int> mp;
    int maxLen = 0;
    for(int end = 0; end < s.size(); end++) {
        while(mp.find(s[end]) != mp.end() && mp[s[end]] >= start) {
            start = mp[s[end]]+1;
        }
        mp[s[end]] = end;
        maxLen = max(maxLen, end-start+1);
    }
    return maxLen;
}
```