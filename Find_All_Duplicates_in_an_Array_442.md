# 442. Find All Duplicates in an Array �����¼
## ��Ŀ������
Given an array of integers, 1 �� a[i] �� *n* (*n* = size of array), some elements appear **twic** and others appear **once**.    
Find all the elements that appear **twice** in this array.    
Could you do it without extra space and in O(*n*) runtime?    
**Example:**
```
Input:
[4,3,2,7,8,2,3,1]

Output:
[2,3]
```
## ����˼·��
��¼Ԫ�س�����񣬷���Ϊ��Ԫ��`t`�Ķ�Ӧ��`nums[t-1]`��Ϊ������Ȼ��ÿ�ζ����һ��`nums[t]`�Ƿ�Ϊ��������Ϊ������˵�����ֹ�����ӽ����顣
## ���룺
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