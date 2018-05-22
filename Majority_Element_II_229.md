# 229. Majority Element II �����¼
## ��Ŀ������
Given an integer array of size n, find all elements that appear more than `n/3` times.  
**Note:** The algorithm should run in linear time and in O(1) space.  
  
**Example 1:**  
```
Input: [3,2,3]
Output: [3]
```
  
**Example 2:**  
```
Input: [1,1,1,3,3,2,2,2]
Output: [1,2]
```
## ����˼·��
�Ƚ������򣬰���ͬ�����������źã��ټ���������Ƚϸ���������/3�Ĵ�С��
## ���룺
``` C
class Solution {
public:
    vector<int> majorityElement(vector<int>& nums) {
        int allTimes = nums.size();
        if(allTimes < 1)
            return vector<int>();
        allTimes /= 3;
        sort(nums.begin(), nums.end());
        vector<int> ret;
        int times = 1, preNum = nums[0];
        for(int i = 1; i < nums.size(); i++){
            if(nums[i] == preNum)
                times++;
            else{
                if(times > allTimes)
                    ret.push_back(nums[i-1]);
                times = 1;
                preNum = nums[i];
            }
        }
        if(times > allTimes)
            ret.push_back(*nums.rbegin());
        return ret;
    }
};
```