# 373. Find K Pairs with Smallest Sums 解题记录
## 题目描述：
You are given two integer arrays **nums1** and **nums2** sorted in ascending order and an integer k.    

Define a pair **(u,v)** which consists of one element from the first array and one element from the second array.    

Find the k pairs **(u1,v1),(u2,v2) ...(uk,vk)** with the smallest sums.    

**Example 1:**  
```
Given nums1 = [1,7,11], nums2 = [2,4,6],  k = 3

Return: [1,2],[1,4],[1,6]

The first 3 pairs are returned from the sequence:
[1,2],[1,4],[1,6],[7,2],[7,4],[11,2],[7,6],[11,4],[11,6]
```
**Example 2:**
```
Given nums1 = [1,1,2], nums2 = [1,2,3],  k = 2

Return: [1,1],[1,1]

The first 2 pairs are returned from the sequence:
[1,1],[1,1],[1,2],[2,1],[1,2],[2,2],[1,3],[1,3],[2,3]
```
**Example 3:**
```
Given nums1 = [1,2], nums2 = [3],  k = 3 

Return: [1,3],[2,3]

All possible pairs are returned from the sequence:
[1,3],[2,3]
```
## 解题思路：
这题我想不到什么高明的思路，把所有pair加入数组中排序再删减，不过缩小了添加到数组的pair数量。
## 代码：
``` C
class Solution {
    static bool cmp(pair<int, int> &a, pair<int, int> &b){
        return a.first+a.second < b.first+b.second;
    }
public:
    vector<pair<int, int>> kSmallestPairs(vector<int>& nums1, vector<int>& nums2, int k) {
        int n1 = min((int)nums1.size(), k), n2 = min((int)nums2.size(), k);
        vector<pair<int, int>> ret;
        for(int i = 0; i < n1; i++){
            for(int j = 0; j < n2; j++){
                ret.push_back(make_pair(nums1[i], nums2[j]));
            }
        }
        sort(ret.begin(), ret.end(), cmp);
        if(ret.size() > k) ret.erase(ret.begin()+k, ret.end());
        return ret;
    }
};
```