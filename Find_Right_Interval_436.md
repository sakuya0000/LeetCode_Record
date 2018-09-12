# 436. Find Right Interval 解题记录
## 题目描述：
Given a set of intervals, for each of the interval i, check if there exists an interval j whose start point is bigger than or equal to the end point of the interval i, which can be called that j is on the "right" of i.     
For any interval i, you need to store the minimum interval j's index, which means that the interval j has the minimum start point to build the "right" relationship for interval i. If the interval j doesn't exist, store -1 for the interval i. Finally, you need output the stored value of each interval as an array.      
**Example 1:**
```
Input: [ [1,2] ]

Output: [-1]

Explanation: There is only one interval in the collection, so it outputs -1.
```
**Example 2:**
```
Input: [ [3,4], [2,3], [1,2] ]

Output: [-1, 0, 1]

Explanation: There is no satisfied "right" interval for [3,4].
For [2,3], the interval [3,4] has minimum-"right" start point;
For [1,2], the interval [2,3] has minimum-"right" start point.
```
**Example 3:**
```
Input: [ [1,4], [2,3], [3,4] ]

Output: [-1, 2, -1]

Explanation: There is no satisfied "right" interval for [1,4] and [3,4].
For [2,3], the interval [3,4] has minimum-"right" start point.
```
## 解题思路：
先将每个区间的开始位置按升序排列用一个map存储，然后依次遍历每个区间的结束位置，在map中找到和结束位置相等或略大的数。
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
public:
    vector<int> findRightInterval(vector<Interval>& intervals) {
        int n = intervals.size();
        if(n == 0) return vector<int>();
        map<int, int> indexs;
        for(int i = 0; i < n; i++){
            indexs[intervals[i].start] = i;
        }
        vector<int> ret(n, 0);
        for(int i = 0; i < n; i++){
            map<int, int>::iterator it = indexs.lower_bound(intervals[i].end);
            if(it != indexs.end()) 
                ret[i] = it->second;
            else ret[i] = -1;
        }
        return ret;
    }
};
```
