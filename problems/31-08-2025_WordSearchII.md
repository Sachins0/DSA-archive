# Word Search II (LeetCode)
Link: https://leetcode.com/problems/word-search-ii/description/

Solution - 
## Approach 1: Backtracking with Set(DFS)
### Time Complexity: O(N * 3^L * W), where N is the number of cells on the board, L is the maximum length of a word, and W is the total number of words in the dictionary.
### Space Complexity: O(L), for recursion stack maximum depth.
```C++
class Solution {
public:
    vector<string> findWords(vector<vector<char>>& board, vector<string>& words) {
        unordered_set<string> result;
        for (string& word : words) {
            if (exist(board, word)) {
                result.insert(word);
            }
        }
        return vector<string>(result.begin(), result.end());
    }
    
private:
    bool exist(vector<vector<char>>& board, const string& word) {
        for (int i = 0; i < board.size(); ++i) {
            for (int j = 0; j < board[0].size(); ++j) {
                if (dfs(board, i, j, 0, word)) {
                    return true;
                }
            }
        }
        return false;
    }

    bool dfs(vector<vector<char>>& board, int i, int j, int k, const string& word) {
        if (k == word.length()) return true; // Whole word found

        if (i < 0 || i >= board.size() || j < 0 || j >= board[0].size() || board[i][j] != word[k]) {
            return false; // Out of bounds or mismatch
        }
        
        char tmp = board[i][j]; // Store current character
        board[i][j] = '#'; // Mark as visited
        bool found = dfs(board, i + 1, j, k + 1, word) ||
                     dfs(board, i - 1, j, k + 1, word) ||
                     dfs(board, i, j + 1, k + 1, word) ||
                     dfs(board, i, j - 1, k + 1, word);
        board[i][j] = tmp; // Restore character
        
        return found;
    }
};
```

## Approach 2: Trie with Backtracking
### Time Complexity: O(N * 3^L), where N is the number of cells on the board, and L is the maximum length of a word in the Trie. The Trie reduces redundant searches.
### Space Complexity: O(W * L), where W is the number of words, and L is the length of the longest word for the Trie storage.
```C++
struct Node {
    Node* links[26];
    string word;
    Node() {
        for(int i = 0; i < 26; i++) links[i] = NULL;
        word = "";
    }
    bool containsKey(char ch) {
        return (links[ch - 'a'] != NULL);
    }
    void put(Node* node, char ch) {
        links[ch-'a'] = node;
    }
    Node* get(char ch) {
        return links[ch-'a'];
    }
};

class Solution {
private:
    Node* root;
    int m, n;
    vector<string> res;
    void insert(string &word) {
        Node* node = root;
        for(int i = 0; i < word.length(); i++) {
            if(!node -> containsKey(word[i])) {
                node -> put(new Node(), word[i]);
            }
            node = node -> get(word[i]);
        }
        node -> word = word;
    }
    void dfs(vector<vector<char>>& board, int i, int j, Node* node) {
        char ch = board[i][j];
        if(ch == '$' || !node -> containsKey(ch))
         return;
        node = node -> get(ch);
        if(!node -> word.empty()) {
            res.push_back(node -> word);
            node -> word = "";
        }
        board[i][j] = '$';
        if(i > 0) dfs(board, i-1, j, node);
        if(i < m-1) dfs(board, i+1, j, node);
        if(j > 0) dfs(board, i, j-1, node);
        if(j < n-1) dfs(board, i, j+1, node);
        board[i][j] = ch;
    }
public:
    vector<string> findWords(vector<vector<char>>& board, vector<string>& words) {
        root = new Node();
        for(string &word : words) insert(word);
        m = board.size();
        n = board[0].size();
        for(int i = 0; i < m; i++) {
            for(int j = 0; j < n; j++) {
                dfs(board, i, j, root);
            }
        }
        return res;
    }
};
```
