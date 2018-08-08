# 377. Combination Sum IV �����¼
## ��Ŀ������
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
## ����˼·��
��������ö�̬�滮���������1��ʼһ�������㵽target����ϸ���������������dp[3]=dp[1]+dp[2]��dp[4]=dp[1]+dp[2]+dp[3]�������1��2��3��4��ȥnums��Ԫ�صĽ������
## ���룺
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