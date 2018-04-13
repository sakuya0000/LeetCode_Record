# 260. Single Number III
## 题目描述：
Given an array of numbers nums, in which exactly two elements appear only once and all the other elements appear exactly twice. Find the two elements that appear only once.  
For example:  
Given nums = `[1, 2, 1, 3, 2, 5]`, return `[3, 5]`.  
## 解题思路：
这题可以利用数组中只有两个单独元素的条件，先对数组进行排序，然后循环遍历数组，每次循环结婚素令i+2。  
因为排序完毕，第一个单独元素只可能出现在i为偶数的情况（从i=0开始遍历），所以比较nums[i]和nums[i+1]就可以得到第一个单独元素。  
然后令i+1,继续遍历数组，得到第二个单独元素。这时候要小心单独元素在数组末尾的时候，不能让i遍历到数组最后。不过如果遍历到最后，就说明最后一个单独元素在数组末尾，这个判断单独进行就好。  
## 代码：
``` C
class Solution {
public:
    vector<int> singleNumber(vector<int>& nums) {
        sort(nums.begin(),nums.end());
        int n = nums.size(), i = 0;
        vector<int> ret;
        for(; i < n-1; i += 2){
        //找第一个单独元素
            if(nums[i] != nums[i+1]){
                ret.push_back(nums[i]);
                break;
            }
        }
        for(i++; i < n-1; i += 2){
        //找第二个单独元素
            if(nums[i] != nums[i+1]){
                ret.push_back(nums[i]);
                break;
            }
        }
        if(ret.size() == 1)
        //判断单独元素是否在数组末尾
            ret.push_back(nums[n-1]);
        return ret;
    }
};
```
