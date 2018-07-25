# 349. Intersection of Two Arrays �����¼
## ��Ŀ������
Given two arrays, write a function to compute their intersection.     
Example:  
Given nums1 = `[1, 2, 2, 1]`, nums2 = `[2, 2]`, return `[2]`.   
## ����˼·��
����set��������⡣
## ���룺
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