# 213. House Robber II �����¼
## ��Ŀ������
You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed. All houses at this place are **arranged in a circle**. That means the first house is the neighbor of the last one. Meanwhile, adjacent houses have security system connected and **it will automatically contact the police if two adjacent houses were broken into on the same night**.    
Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight **without alerting the police**.      
**Example 1:**    
```
Input: [2,3,2]
Output: 3
Explanation: You cannot rob house 1 (money = 2) and then rob house 3 (money = 2),
             because they are adjacent houses.
```  
**Example 2:**    
```
Input: [1,2,3,1]
Output: 4
Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
             Total amount you can rob = 1 + 3 = 4.
```
## ����˼·��
����Ľ���˼·��198.House Robber����һ�£����ƹ�ʽ**f(n)=max[f(n-1), f(n-2)+A(n)]**û�䣬ֻ�Ƿ���Χ���˻���Ҫ�ֳ�����������ǣ�  
  
1. ���ǵ�һ�����ӣ���ô��Ϊ���ڣ����һ�����Ӳ����ǡ�����ֻҪ����0��n-1�ķ��Ӽ��ɡ�
2. �����ǵ�һ�����ӣ���ô�������һ�����ӡ����Կ���1��n�ķ��ӡ�
## ���룺
``` C
class Solution {
public:
    int rob(vector<int>& nums) {
        int len = nums.size();
        if(len == 0)
            return 0;
        if(len == 1)
            return nums[0];
        if(len == 2)
            return max(nums[0], nums[1]);
        vector<int> rt1(len-1, 0), rt2(len-1, 0);
        rt1[0] = nums[0]; rt1[1] = max(nums[0], nums[1]);
        rt2[0] = nums[1]; rt2[1] = max(nums[1], nums[2]);
        for(int i = 2; i < len-1; i++){
            rt1[i] = max(rt1[i-1], rt1[i-2]+nums[i]);
            rt2[i] = max(rt2[i-1], rt2[i-2]+nums[i+1]);
        }
        return max(max(rt1[len-2], rt1[len-3]), max(rt2[len-2], rt2[len-3]));
    }
};
```