# 307. Range Sum Query - Mutable 解题记录
## 题目描述：
Given an integer array nums, find the sum of the elements between indices i and j (i ≤ j), inclusive.    
The update(i, val) function modifies nums by updating the element at index i to val.    
**Example:**
```
Given nums = [1, 3, 5]

sumRange(0, 2) -> 9
update(1, 2)
sumRange(0, 2) -> 8
```
## 解题思路：
这题我的思路是创建一个数组来存储从0位置到元素位置的所有数的和。然后求i到j和的时候只要减一下就可以了。但更新的效率好像不怎么高。
## 代码：
``` C
class NumArray {
    vector<int> newNums;
public:
    NumArray(vector<int> nums) {
        int n = nums.size();
        vector<int> temp(n+1, 0);
        newNums = temp;
        for(int i = 1; i < n+1; i++){
            newNums[i] = newNums[i-1] + nums[i-1];
        }
    }
    
    void update(int i, int val) {
        int minusNum = newNums[i+1] - newNums[i];
        i++;
        for(; i < newNums.size(); i++){
            newNums[i] -= minusNum;
            newNums[i] += val;
        }
    }
    
    int sumRange(int i, int j) {
        return newNums[j+1] - newNums[i];
    }
};

/**
 * Your NumArray object will be instantiated and called as such:
 * NumArray obj = new NumArray(nums);
 * obj.update(i,val);
 * int param_2 = obj.sumRange(i,j);
 */
```