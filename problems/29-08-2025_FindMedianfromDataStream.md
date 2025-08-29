# Find Median from Data Stream (LeetCode)
Link: https://leetcode.com/problems/find-median-from-data-stream/description/

Solution - 
```C++
class MedianFinder {
public:
    priority_queue<int> rightMaxHeap;
    priority_queue<int, vector<int>, greater<int>> leftMinHeap;
    MedianFinder() {
        
    }
    
    void addNum(int num) {
        leftMinHeap.push(num);
        rightMaxHeap.push(leftMinHeap.top());
        leftMinHeap.pop();
        if(rightMaxHeap.size() > leftMinHeap.size()) {
            leftMinHeap.push(rightMaxHeap.top());
            rightMaxHeap.pop();
        }
    }
    
    double findMedian() {
        double median;
        if(leftMinHeap.size() > rightMaxHeap.size()) return leftMinHeap.top();
        else median = (double)(leftMinHeap.top() + rightMaxHeap.top())/2;
        return median;
    }
};
```
