# 377. Combination Sum IV 解题记录
## 题目描述：
Given an integer array with all positive numbers and no duplicates, find the number of possible combinations that add up to a positive integer target.    
**Example: **
```
nums = [1, 2, 3]
target = 4

The possible combination ways are:
(1, 1, 1, 1)
(1, 1, 2)
(1, 2, 1)
(1, 3)
(2, 1, 1)
(2, 2)
(3, 1)

Note that different sequences are counted as different combinations.

Therefore the output is 7.
```
## 解题思路：
本题可以用动态规划来解决，从1开始一步步计算到target的组合个数。比如例子中dp[3]=dp[1]+dp[2]，dp[4]=dp[1]+dp[2]+dp[3]（这里的1，2，3是4减去nums中元素的结果）。
## 代码：
``` C
class Solution {
public:
    int combinationSum4(vector<int>& nums, int target) {
        vector<int> dp(target + 1);
        dp[0] = 1;
        sort(nums.begin(), nums.end());
        for (int i = 1; i <= target; ++i) {
            for (int j = 0; j < nums.size(); j++) {
                if (i < nums[j]) break;
                dp[i] += dp[i - nums[j]];
            }
        }
        return dp.back();
    }
};
```