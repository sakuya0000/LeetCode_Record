# 390. Elimination Game 解题记录
## 题目描述：
There is a list of sorted integers from 1 to *n*. Starting from left to right, remove the first number and every other number afterward until you reach the end of the list.    
Repeat the previous step again, but this time from right to left, remove the right most number and every other number from the remaining numbers.    
We keep repeating the steps again, alternating left to right and right to left, until a single number remains.    
Find the last number that remains starting with a list of length *n*.    
**Example: **
```
Input:
n = 9,
1 2 3 4 5 6 7 8 9
2 4 6 8
2 6
6

Output:
6
```
## 解题思路：
消除游戏的第一步就是把奇数全都消去留下偶数，即2, 4, 6, 8, ... , 2\*(n/2)。换个角度看就是2\*(1, 2, 3, 4, ... , n/2)。所以只要一直递归取2\*func(n/2)的值。但因为第二步要倒着数，所以实际要取得时2\*(n/2 + 1 - func(n/2))。
## 代码：
``` C
class Solution {
public:
    int lastRemaining(int n) {
        if(n == 1) return 1;
        return 2*(n/2 + 1 - lastRemaining(n/2));
    }
};
```