# Substring with Concatenation of All Words (LeetCode)
Link: https://leetcode.com/problems/substring-with-concatenation-of-all-words/description/

Solution - 
## Brute Force Approach
- **Time Complexity**: O((n - m * k) * m * k), where n is the length of s, m is the number of words, and k is the length of each word.
- **Space Complexity**: O((m + n)/k) for the hashmap storage for words.
```C++
 vector<int> findSubstring(string s, vector<string>& words) {
    vector<int> res;
    int wordCnt = words.size();
    int wordLen = words[0].size();
    int totalLen = wordCnt*wordLen;
    unordered_map<string, int> mp;
    for(const string& word: words) mp[word]++;
    for(int i = 0; i <= static_cast<int>(s.size()) - totalLen; i++) {
        unordered_map<string, int> seenWord;
        int j = 0;
        while(j < wordCnt) {
            int wordIdx = i + j * wordLen;
            string word = s.substr(wordIdx, wordLen);
            if(mp.find(word) == mp.end()) break;
            seenWord[word]++;
            if(seenWord[word] > mp[word]) break;
            j++;
        }
        if(j == wordCnt) res.push_back(i); 
    }
    return res;
}
```

## Optimized Sliding Window with Hashmap
- **Time Complexity**: O(n * k), where n is the length of s, and k is the word length. The sliding window ensures each character is processed at most twice.
- **Space Complexity**: O(m + n/k) due to the maps used for counts of required and current words.
```C++
vector<int> findSubstring(string s, vector<string>& words) {
    vector<int> res;
    int wordCnt = words.size();
    int wordLen = words[0].size();
    int totalLen = wordCnt*wordLen;
    unordered_map<string, int> mp, currMp;
    for(const string& word: words) mp[word]++;
    for(int i = 0; i < wordLen; i++) {
        int left = i, cnt = 0;
        currMp.clear();
        for(int right = i; right <= 
        static_cast<int>(s.size()) - wordLen; right += wordLen) {
            string word = s.substr(right, wordLen);
            if(mp.count(word)) {
                currMp[word]++;
                cnt++;
                while(currMp[word] > mp[word]) {
                    string leftWord = s.substr(left, wordLen);
                    cnt--;
                    currMp[leftWord]--;
                    left += wordLen;
                }
                if (cnt == wordCnt) res.push_back(left);
            }
            else {
                currMp.clear();
                cnt = 0;
                left = right + wordLen;
            }
        }
    }
    return res;
}
```
