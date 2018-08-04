# 374. Guess Number Higher or Lower 解题记录
## 题目描述：
We are playing the Guess Game. The game is as follows:    

I pick a number from **1** to **n**. You have to guess which number I picked.    

Every time you guess wrong, I'll tell you whether the number is higher or lower.    

You call a pre-defined API `guess(int num)` which returns 3 possible results (`-1`, `1`, or `0`):  
```
-1 : My number is lower
 1 : My number is higher
 0 : Congrats! You got it!
```
**Example:**  
```
n = 10, I pick 6.

Return 6.
```
## 解题思路：
用二分法解决，不过要注意有一个坑是int类型的数据会越界，要么用unsigned int，要么不要用(left+right)/2，改用left+(right-left)/2。
## 代码：
``` C
// Forward declaration of guess API.
// @param num, your guess
// @return -1 if my number is lower, 1 if my number is higher, otherwise return 0
int guess(int num);

class Solution {
public:
    int guessNumber(int n) {
        int left = 1, right = n, mid = left + (right - left) / 2;
        int result = guess(mid);
        while(result){
            if(result == 1) left = mid+1;
            else if(result == -1) right = mid-1;
            mid = left + (right - left) / 2;
            result = guess(mid);
        }
        return mid;
    }
};
```