# 442. Find All Duplicates in an Array 解题记录
## 题目描述：
Given an array of integers, 1 ≤ a[i] ≤ *n* (*n* = size of array), some elements appear **twic** and others appear **once**.    
Find all the elements that appear **twice** in this array.    
Could you do it without extra space and in O(*n*) runtime?    
**Example:**
```
Input:
[4,3,2,7,8,2,3,1]

Output:
[2,3]
```
## 解题思路：
记录元素出现与否，方法为将元素`t`的对应的`nums[t-1]`变为负数，然后每次都检测一下`nums[t]`是否为负数，若为负数就说明出现过，添加进数组。
## 代码：
``` C
class Solution {
public:
    vector<int> findDuplicates(vector<int>& nums) {
        int n = nums.size();
        vector<int> ret;
        for(int i = 0; i < n; i++){
            int t = abs(nums[i]) -1;
            if(nums[t] < 0) ret.push_back(t + 1);
            nums[t] = -nums[t];
        }
        return ret;
    }
};
```