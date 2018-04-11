# 152. Maximum Product Subarray 解题记录
## 题目描述：
Find the contiguous subarray within an array (containing at least one number) which has the largest product.  
For example, given the array **[2,3,-2,4]**,  
the contiguous subarray **[2,3]** has the largest product = **6**. 
## 解题思路：
**这道题可分为两种情况：**  
1. 有非0的元素，首先分析当数组中有<0的元素，可分为2种情况；  
　 1)个数为`偶数`，这种情况只要把元素全乘一遍就会得到最大值；  
　 2)个数为`奇数`，首先看一个例子: 
***
`[-1, -2, -3, -4, -5]`  
*因为题目所要求返回的最大乘积，所以可以排除无用的排序将其分为两个数组*  
`[-1, -2, -3, -4]`  
`[-2, -3, -4, -5]`  
***
　　因此，奇数的情况只有两种可能性，分别是`从第一个元素乘到倒数第二个负数`和`从第二个负数乘到最后一个元素`。  
　　而`>0`的元素没有丝毫的影响，乘过去即可。就算负数与负数的中间或是前面或是后面夹杂着正数也只是扩大最后的结果。  
2.有0的元素，无论哪个数乘0都为0，所以0就相当一个终止符，把一个数组划分成两个数组。  
## 代码：
``` C
class Solution {
public:
    int maxProduct(vector<int>& nums) {
        int maxAll = nums[0], n = nums.size();
        int first = 1, second = 1;
        bool flag = 0; //是否遇到负数标志
        for(int i = 0; i < n; i++){
            first *= nums[i];
            second *= nums[i];
            maxAll = maxAll>first?maxAll:first;  //负数是奇数的第一个情况
            maxAll = maxAll>second?maxAll:second;  //奇数的第二个情况
            if(nums[i] < 0 && !flag){
            //第一次遇到负数
                second = 1;
                flag = 1;
            }
            if(nums[i] == 0){
            //遇到0的情况
                maxAll = 0>maxAll?0:maxAll;
                flag = 0;-5
                first = 1;
                second = 1;
            }
        }
        return maxAll;
    }
};
```