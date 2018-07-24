# 268. Missing Number �����¼
## ��Ŀ������
Given an array containing n distinct numbers taken from `0, 1, 2, ..., n`, find the one that is missing from the array.    
**Example 1:**  
```
Input: [3,0,1]
Output: 2
```
**Example 2:**
```
Input: [9,6,4,2,3,5,7,0,1]
Output: 8
```
## ����˼·��
�Ƚ�������Ȼ�����һ�����ȶԼ��ɡ��������������δ�ҵ������������������
## ���룺
```
class Solution {
public:
    int missingNumber(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        int n = nums.size();
        for(int i = 0; i < n; i++){
            if(i != nums[i]){
                return i;
            }
        }
        return n;
    }
};
```