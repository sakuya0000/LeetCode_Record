# 435. Non-overlapping Intervals 解题记录
## 题目描述：
Given a collection of intervals, find the minimum number of intervals you need to remove to make the rest of the intervals non-overlapping.     
**Example 1:**
```
Input: [ [1,2], [2,3], [3,4], [1,3] ]

Output: 1

Explanation: [1,3] can be removed and the rest of intervals are non-overlapping.
```
**Example 2:**
```
Input: [ [1,2], [1,2], [1,2] ]

Output: 2

Explanation: You need to remove two [1,2] to make the rest of intervals non-overlapping.
```
**Example 3:**
```
Input: [ [1,2], [2,3] ]

Output: 0

Explanation: You don't need to remove any of the intervals since they're already non-overlapping.
```
## 解题思路：
先按end排序，然后找出没有覆盖的区间个数，然后将总个数减去这个个数。
## 代码：
``` C
/**
 * Definition for an interval.
 * struct Interval {
 *     int start;
 *     int end;
 *     Interval() : start(0), end(0) {}
 *     Interval(int s, int e) : start(s), end(e) {}
 * };
 */
class Solution {
    static bool cmp(Interval& a, Interval& b){
        return a.end < b.end;
    }
public:
    int eraseOverlapIntervals(vector<Interval>& intervals) {
        int n = intervals.size();
        if(n == 0) return 0;
        sort(intervals.begin(), intervals.end(), cmp);
        int last = 0, count = 1;
        for(int i = 1; i < n; i++){
            if(intervals[i].start >= intervals[last].end){
                last = i;
                count++;
            }
        }
        return n - count;
    }
};
```