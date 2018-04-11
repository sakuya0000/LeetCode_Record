# 238. Product of Array Except Self
## 题目描述：
Given an array of n integers where n > 1, nums, return an array output such that output[i] is equal to the product of all the elements of nums except nums[i].  
Solve it *without division* and in *O(n)*.  
For example, given *[1,2,3,4]*, return **`[24,12,8,6]`**.  
## 解题思路：
这题我们可以先创建一个数组ret，令ret的第一个数为1，然后用循环让ret数组中从第二个元素开始的值等于它的`上一个元素`乘`nums中的对应元素`。  
因此第一次遍历过后可以得到ret中的元素分布为
> [1, nums[0], nums[0]*nums[1],……, ∑nums[i](i<amp;n-1)]。  
接下来可以让一个数从nums数组的末尾开始乘，每一次乘后都要让ret的对应元素乘这个数以`补齐ret当前元素未乘的部分`，直到乘到nums[1]。
## 代码：
``` C
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        int n = nums.size();
        vector<int> ret(n, 1);
        for(int i = 1; i < n; i++){
        //第一次遍历
            ret [i] = nums[i-1] * ret[i-1];
        }
        for(int i = n - 1; i > 1; i--){
        //第二次遍历
            ret[0] *= nums[i];
            ret[i-1] *= ret[0];
        }
        ret[0] *= nums[1];  //避免乘相同的数
        return ret;
    }
};
```