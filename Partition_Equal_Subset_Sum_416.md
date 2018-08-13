# 416. Partition Equal Subset Sum 解题记录
## 题目描述：
Given a non-empty array containing only positive integers, find if the array can be partitioned into two subsets such that the sum of elements in both subsets is equal.    

**Example 1:**  
```
Input: [1, 5, 11, 5]

Output: true

Explanation: The array can be partitioned as [1, 5, 5] and [11].
```
**Example 2:**  
```
Input: [1, 2, 3, 5]

Output: false

Explanation: The array cannot be partitioned into equal sum subsets.
```
## 解题思路：
先求所有元素的总和，只有是偶数的情况下才会有解，奇数直接返回false。然后把和除以2，化成背包问题来解决。
## 代码：
``` C
class Solution {
public:
    bool canPartition(vector<int>& nums) {
        int n = nums.size(), sum = 0;
        for(int i = 0; i < n; i++){
            sum += nums[i];
        }
        if(sum % 2 == 1) return false;
        sum /= 2;
        vector<vector<int>> dp(n, vector<int>(sum + 1, 0));
		for (int i = nums[0]; i <= sum; i++) {
			dp[0][i] = nums[0];
		}
		for (int i = 1; i<n; i++) {
			for (int j = nums[i]; j <= sum; j++) {
				dp[i][j] = max(dp[i - 1][j], dp[i - 1][j - nums[i]] + nums[i]);
			}
		}
		if (dp[n - 1][sum] == sum)
			return true;
        return false;
    }
};
```