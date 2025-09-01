# Merge Sorted Array (LeetCode)
Link: https://leetcode.com/problems/merge-sorted-array/description/

Solution - 
## Approach 1: Brute Force
### Time Complexity: O((m + n) log(m + n)) Space Complexity: O(1)
```C++
void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
    for(int i = 0; i < n; ++i) {
        nums1[m + i] = nums2[i];
    }
    sort(nums1.begin(), nums1.begin() + m + n);
}
```

## Approach 2: Optimized Two Pointers (Start from the end)
### Time Complexity: O(m + n) Space Complexity: O(1)
```C++
void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
    int i = m-1, j = n-1, k = m + n - 1;
    while(j >= 0) {
        if( i>= 0 && nums1[i] > nums2[j])
            nums1[k--] = nums1[i--]; 
        else nums1[k--] = nums2[j--];
    }
}
```
