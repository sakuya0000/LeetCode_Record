# 213. House Robber II 解题记录
## 题目描述：
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
## 解题思路：
本题的解题思路跟198.House Robber基本一致，递推公式**f(n)=max[f(n-1), f(n-2)+A(n)]**没变，只是房子围成了环。要分成两种情况考虑：  
  
1. 考虑第一个房子，那么因为相邻，最后一个房子不考虑。所以只要考虑0到n-1的房子即可。
2. 不考虑第一个房子，那么考虑最后一个房子。所以考虑1到n的房子。
## 代码：
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