# 396. Rotate Function 解题记录
## 题目描述：
Given an array of integers `A` and let *n* to be its length.     
Assume `B<sub>k</sub>` to be an array obtained by rotating the array `A` *k* positions clock-wise, we define a "rotation function" `F` on `A` as follow:     
`F(k) = 0 * B<sub>k</sub>[0] + 1 * B<sub>k</sub>[1] + ... + (n-1) * B<sub>k</sub>[n-1]`.    
Calculate the maximum value of `F(0), F(1), ..., F(n-1)`.     
**Note:**    
*n* is guaranteed to be less than 10<sup>5</sup>.     
**Example: **
```
A = [4, 3, 2, 6]

F(0) = (0 * 4) + (1 * 3) + (2 * 2) + (3 * 6) = 0 + 3 + 4 + 18 = 25
F(1) = (0 * 6) + (1 * 4) + (2 * 3) + (3 * 2) = 0 + 4 + 6 + 6 = 16
F(2) = (0 * 2) + (1 * 6) + (2 * 4) + (3 * 3) = 0 + 6 + 8 + 9 = 23
F(3) = (0 * 3) + (1 * 2) + (2 * 6) + (3 * 4) = 0 + 2 + 12 + 12 = 26

So the maximum value of F(0), F(1), F(2), F(3) is F(3) = 26.
```
## 解题思路：
由例子中可以看出从F(1) = F(0) + 4 + 3 + 2 + 6 - 4*6。所以得到递推公式F(n) = F(n-1) + sum - 元素个数*A[i]。
## 代码：
``` C
class Solution {
public:
    int maxRotateFunction(vector<int>& A) {
        int ret = INT_MIN, n = A.size();
        if(n == 0) return 0;
        int sum = 0, cur = 0;
        for(int i = 0; i < n; i++){
            cur += i * A[i];
            sum += A[i];
        }
        ret = max(ret, cur);
        for(int i = n-1; i >= 0; i--){
            cur += sum;
            cur -= n * A[i];
            ret = max(ret, cur);
        }
        return ret;
    }
};
```