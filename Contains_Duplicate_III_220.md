# 220. Contains Duplicate III 解题记录
## 题目描述：
Given an array of integers, find out whether there are two distinct indices i and j in the array such that the `absolute` difference between `nums[i]` and `nums[j]` is at most t and the `absolute` difference between i and j is at most k.  
  
**Example 1:**
```
Input: [1,2,3,1], k = 4, t = 0
Output: true
```
**Example 2:**
```
Input: [1,0,1,1], k = 1, t = 0
Output: true
```
**Example 3:**
```
Input: [4,2], k = 2, t = 1 
Output: false
```
## 解题思路：
这题无非是要满足两个条件:
> |nums[i]-nums[j]|<=t
> |i-j|<=k
用遍历循环太耗时，所以用二叉树解决。
## 代码：
``` C
class Solution {
public:
    bool containsNearbyAlmostDuplicate(vector<int>& nums, int k, int t) {
        if(nums.size() ==0) return false;
        multiset<long long> st;
        for(int i = 0; i < nums.size(); i++)
        {
            if(i > k) 
                st.erase(st.find(nums[i-k-1]));
            auto it = st.lower_bound((long long)nums[i]-t);
            if(it!=st.end() && abs(*it-nums[i]) <=t)
                return true;
            st.insert(nums[i]);
        }
        return false;
    }
};
```