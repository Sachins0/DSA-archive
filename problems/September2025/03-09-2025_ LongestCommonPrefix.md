# Longest Common Prefix (LeetCode)
Link: https://leetcode.com/problems/longest-common-prefix/description/

Solution - 
## Approach 1: Horizontal Scanning
- **Time Complexity**: O(S), where S is the sum of all characters in all strings. In the worst case, all strings are the same.
- **Space Complexity**: O(1)
```C++
string longestCommonPrefix(vector<string>& strs) {
    string prefix = strs[0];
    for(int i = 1; i < strs.size(); i++) {
        int j = 0;
        while(j < strs[i].size() && prefix[j] == strs[i][j]) {
            j++;
        }
        prefix = prefix.substr(0, j);
    }
    return prefix;
}
```

## Approach 2 : Trie
- **Time Complexity**: Time Complexity:O(N * L), where N = number of strings, L = max length of a string.
- **Space Complexity**: O(N * L)
```C++
struct Node {
    Node* links[26];
    bool flag = false;
    int childCnt;

    Node() {
        flag = false;
        childCnt = 0;
        for(int i = 0; i < 26; i++) {
            links[i] = NULL;
            
        }
    }
    bool containsKey(char ch) {
        return links[ch - 'a'] != NULL;
    }
    void put(char ch, Node* node) {
        links[ch - 'a'] = node;
    }
    Node* get(char ch) {
        return links[ch - 'a'];
    }
    void setEnd() {
        flag = true;
    }
    bool isEnd() {
        return flag;
    }
};

class Trie{
private:
    Node* root;
public: 
    Trie() {
        root = new Node();
    }
    void insert(string &word) {
        Node* node = root;
        for(int i = 0; i < word.length(); i++) {
            if(!node -> containsKey(word[i])){
                node -> put(word[i], new Node());
                node -> childCnt++;
            }
            node = node -> get(word[i]);
        }
        node -> setEnd();
    }
    void lcp(string &str, string &ans) {
        Node* node = root;
        for(int i = 0; i < str.size(); i++) {
            char ch = str[i];
            if (node->childCnt != 1 || node->isEnd()) {
                break;
            }
            ans.push_back(ch);
            node = node->get(ch);
        }
        
    }
};

class Solution {
public:
    string longestCommonPrefix(vector<string>& strs) {
        if(strs.empty()) return "";
        int n = strs.size();
        Trie *t = new Trie();
        for(int i = 0; i < n; i++) {
            if (strs[i].empty()) {
                return "";
            }
            t -> insert(strs[i]);
        }
        string first = strs[0];
        string ans = "";
        t -> lcp(first, ans);
        return ans;
    }
};
```
