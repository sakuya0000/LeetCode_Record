# 386. Lexicographical Numbers 解题记录
## 题目描述：
Given an integer n, return 1 - *n* in lexicographical order.     
For example, given 13, return: [1,10,11,12,13,2,3,4,5,6,7,8,9].     
Please optimize your algorithm to use less time and space. The input size may be as large as 5,000,000.     
## 解题思路：
解这道题只要了解字典序数如何排序的，然后根据排序方法来逐个添加就可以了。  
1. 如果一个数乘10没有超过n，那么下一个数必定是这个数乘10;  
2. 如果一个数+1后不是10的倍数，那么下一个数是这个数+1;  
3. 如果是10的倍数，那么循环除10直到不是10的倍数，例如这个数为199时，下个数为200;  
4. 还有一种额外的情况就是这个数=n的情况，这个时候就不能直接+1了，但可以把这个数除以10后+1进行2，3情况的判断。例如n=159，下一个数为16。
## 代码：
``` C
class Solution {
public:
    vector<int> lexicalOrder(int n) {
        int cur = 1;
        vector<int> ret;
        for(int i = 1; i <= n; i++){
            ret.push_back(cur);
            if(cur*10 <= n){
                cur *= 10;
                continue;
            }
            if(cur == n){
                cur /= 10;
            }
            cur++;
            if(cur % 10 == 0){
                while(cur%10 == 0){
                    cur /= 10;
                }
            }
        }
        return ret;
    }
};
```