# Permutation in String (LeetCode)
Link: https://leetcode.com/problems/permutation-in-string/description/
Solution - 
## Approach 1: Brute Force using String Permutations
**Time Complexity**: O(n! * m)
**Space Complexity**: O(n)
```C++
bool checkInclusion(string s1, string s2) {
    sort(s1.begin(), s1.end());
    do {
        if(s2.find(s1) != string::npos) {
            return true;
        }
    } while(next_permutation(s1.begin(), s1.end()));
    return false;
}
```

## Approach 2: Sliding Window with Array Comparison
**Time Complexity**: O(n + m)
**Space Complexity**: O(1)
```C++
bool checkInclusion(string s1, string s2) {
    if (s1.length() > s2.length()) return false;
    int n1 = s1.size(), n2 = s2.size();
    vector<int> freq1(26, 0);
    vector<int> freq2(26, 0);
    for(int i = 0; i < n1; i++) {
        freq1[s1[i] - 'a']++;
        freq2[s2[i] - 'a']++;
    }
    if(freq1 == freq2) return true;
    for(int i = n1; i < n2; i++) {
        freq2[s2[i] - 'a']++;
        freq2[s2[i-n1] - 'a']--;
        if(freq1 == freq2) return true;
    }
    return false;
}
```

## Approach 3: Optimized Sliding Window with Frequency Count
**Time Complexity**: O(n + m)
**Space Complexity**: O(1)
```C++
bool checkInclusion(string s1, string s2) {
    if (s1.length() > s2.length()) return false;

    vector<int> s1Count(26, 0);
    vector<int> s2Count(26, 0);
    int matches = 0;

    for (char c : s1) s1Count[c - 'a']++;

    for (int i = 0; i < s2.length(); ++i) {
        if (i < s1.length()) {
            s2Count[s2[i] - 'a']++;
            if (s2Count[s2[i] - 'a'] == s1Count[s2[i] - 'a']) matches++;
            else if (s2Count[s2[i] - 'a'] == s1Count[s2[i] - 'a'] + 1) matches--;
        } else {
            int addIdx = s2[i] - 'a';
            int removeIdx = s2[i - s1.length()] - 'a';

            s2Count[addIdx]++;
            if (s2Count[addIdx] == s1Count[addIdx]) matches++;
            else if (s2Count[addIdx] == s1Count[addIdx] + 1) matches--;

            s2Count[removeIdx]--;
            if (s2Count[removeIdx] == s1Count[removeIdx]) matches++;
            else if (s2Count[removeIdx] == s1Count[removeIdx] - 1) matches--;
        }

        if (matches == 26) return true;
    }

    return false;
}
```