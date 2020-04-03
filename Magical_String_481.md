# 481. Magical String
## 题目描述：
A magical string **S** consists of only '1' and '2' and obeys the following rules:     
The string **S** is magical because concatenating the number of contiguous occurrences of characters '1' and '2' generates the string **S** itself. 
The first few elements of string **S** is the following: **S** = "1221121221221121122……"     
If we group the consecutive '1's and '2's in **S**, it will be: 
1 22 11 2 1 22 1 22 11 2 11 22 ......     
and the occurrences of '1's or '2's in each group are: 
1 2 2 1 1 2 1 2 2 1 2 2 ......     
You can see that the occurrence sequence above is the **S** itself. 
Given an integer N as input, return the number of '1's in the first N number in the magical string **S**.     
**Note:** N will not exceed 100,000.     
**Example 1:**
```
Input: 6
Output: 3
Explanation: The first 6 elements of magical string S is "12211" and it contains three 1's, so return 3.
```
## 解题思路：
首先先找这组字符串的规律：下方那一行代表字符数列的字符串决定了上方那一行字符串如何演变，例如第2个字符为2，代表了第2、3两个字符一样。又因为第1个字符为1，所以2、3两个字符
为2。字符演变的时候只需要注意两点：    
1. 前面的字符代表演变字符的数量，所以要用两个下标来分别表示字符数量的下标和
字符结尾的下标。    
2. 代表字符数量的下标每递增一次，添加在字符串末尾的字符就要在1和2之间切换一次。    
最后在演变字符串的时候计数1就可以了。    
## 代码： 
``` C
class Solution {
public:
    int magicalString(int n) {
        int nums[200000];
        nums[1] = 1;     
        nums[2] = nums[3] = 2;
        int cnt_i = 1;   //代表字符串末尾的下标
        int curfig = 1;  //代表当前字符为1还是2
        int res = 0;     //计数1的个数
        for(int i = 1; i <= n; i++){
            nums[cnt_i++] = curfig;
            if(curfig == 1) res++;
            if(cnt_i > n) break;
            if(nums[i] == 2){
                nums[cnt_i++] = curfig;
                if(curfig == 1) res++;
            }
            if(cnt_i > n) break;    //当字符串末尾超过n就不必再演变了
            if(curfig == 1)
                curfig = 2;
            else curfig = 1;
        }
        return res;
    }
};
```