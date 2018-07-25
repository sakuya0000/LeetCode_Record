# 349. Intersection of Two Arrays 解题记录
## 题目描述：
Given two arrays, write a function to compute their intersection.     
Example:  
Given nums1 = `[1, 2, 2, 1]`, nums2 = `[2, 2]`, return `[2]`.   
## 解题思路：
运用set来解这道题。
## 代码：
``` C
class Solution {
public:
    vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
        set<int> n(nums1.begin(), nums1.end()), ret;
        for(int i = 0; i < nums2.size(); i++){
            if(n.count(nums2[i]))
                ret.insert(nums2[i]);
        }
        return vector<int>(ret.begin(), ret.end());
    }
};
```