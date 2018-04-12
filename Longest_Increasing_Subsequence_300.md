# 300. Longest Increasing Subsequence
## 题目描述：
Given an unsorted array of integers, find the length of longest increasing subsequence.  
For example,  
Given **`[10, 9, 2, 5, 3, 7, 101, 18]`**,  
The longest increasing subsequence is **`[2, 3, 7, 101]`**, therefore the length is **`4`**. Note that there may be more than one LIS combination, it is only necessary for you to return the length.  
Your algorithm should run in O(n2) complexity.  
## 解题思路：
这题可以采用动态规划的办法,新建一个等长数组count来记录子数组的最长长度,遍历数组nums,第二层依次遍历count数组得到当前元素的最长数组长度。:bowtie:  
例：
> [10, 9, 2, 5, 3, 7, 101, 18]  
> *上述的例子在经过遍历后后得到的count数组为：*  
> [1, 1, 1, 2, 2, 3, 4, 4]  

## 代码：
``` C
ass Solution {
public:
    int lengthOfLIS(vector<int>& nums) {
        int ret = 0, n = nums.size();
        vector<int> count(n, 1);
        for(int i = 0; i < n; i++){
            for(int j = 0; j < i; j ++){
                if(nums[i]>nums[j] && count[j]>=count[i])
                //当前元素大于遍历元素 且 遍历元素代表的最长长度+1大于当前元素长度
                    count[i] = count[j]+1;
            }
            ret = ret>count[i]?ret:count[i];  //每次得到当前元素的最长长度时与ret进行比较，毕竟当前元素的最长长度不代表所有元素中的最长长度
        }
        return ret;
    }
};
```
