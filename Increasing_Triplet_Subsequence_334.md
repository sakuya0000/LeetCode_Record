# 334. Increasing Triplet Subsequence 解题记录
## 题目描述：
Given an unsorted array return whether an increasing subsequence of length 3 exists or not in the array.    
Formally the function should:    
> Return true if there exists *i*, *j*, *k*   
> such that *arr[i]* < *arr[j]* < *arr[k]* given 0 ≤ *i* < *j* < *k* ≤ *n*-1 else return false.
  
Note: Your algorithm should run in O(n) time complexity and O(1) space complexity.    
**Example 1:**  
```
Input: [1,2,3,4,5]
Output: true
```    
**Example 2:**  
```
Input: [5,4,3,2,1]
Output: false
```
## 解题思路：
找较小的两个数，如果有第三个大于这两个数，那么就返回true。不过这种办法只能用在数组中没有重复数的情况下。
## 代码：
``` C
class Solution {
public:
    bool increasingTriplet(vector<int>& nums) {
        int m1 = INT_MAX, m2 = INT_MAX;
        for(int i = 0; i < nums.size(); i++){
            if(m1 >= nums[i]) m1 = nums[i];
            else if(m2 >= nums[i]) m2 = nums[i];
            else return true;
        }
        return false;
    }
};
```