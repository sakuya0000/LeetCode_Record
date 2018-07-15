# House Robber 解题记录
## 题目描述：
You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and **it will automatically contact the police if two adjacent houses were broken into on the same night.**    
Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight **without alerting the police**.    
**Example 1:**  
```
Input: [1,2,3,1]
Output: 4
Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
             Total amount you can rob = 1 + 3 = 4.
```  
**Example 2:**  
```
Input: [2,7,9,3,1]
Output: 12
Explanation: Rob house 1 (money = 2), rob house 3 (money = 9) and rob house 5 (money = 1).
             Total amount you can rob = 2 + 9 + 1 = 12.
```  
## 解题思路：
本题由题意可推出一个递推公式**f(n)=max[f(n-1), f(n-2)+A(n)]**，然后用动态规划的方法解决这道题。
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
        vector<int> rt(len, 0);
        rt[0] = nums[0];
        rt[1] = max(nums[1], nums[0]);
        for(int i = 2; i < len; i++){
            rt[i] = max(rt[i-1], rt[i-2]+nums[i]);
        }
        return max(rt[len-1], rt[len-2]);
    }
};
```