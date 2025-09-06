# Word Ladder (LeetCode)
Link: https://leetcode.com/problems/word-ladder/description/

Solution - 
## Approach 1: BFS with Word List
- **Time Complexity**:  O(N*M^2), where N is the length of wordList and M is the average length of words.
- **Space Complexity**:  O(N * M)
```C++
int ladderLength(string beginWord, string endWord, vector<string>& wordList) {
    unordered_set<string> st(wordList.begin(), wordList.end());
    st.erase(beginWord);
    queue<pair<string, int>> qu;
    qu.push({beginWord, 1});
    while(!qu.empty()) {
        string word = qu.front().first;
        int steps = qu.front().second;
        qu.pop();
        if(word == endWord) return steps;
        for(int i = 0; i < word.size(); i++) {
            char org = word[i];
            for(char ch = 'a'; ch <= 'z'; ch++) {
                word[i] = ch;
                if(st.find(word) != st.end()) {
                    st.erase(word);
                    qu.push({word, steps+1});
                }
            }
            word[i] = org;
        }
    }
    return 0;
}
```
