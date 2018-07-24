# 319. Bulb Switcher 解题记录
## 题目描述：
There are n bulbs that are initially off. You first turn on all the bulbs. Then, you turn off every second bulb. On the third round, you toggle every third bulb (turning on if it's off or turning off if it's on). For the i-th round, you toggle every i bulb. For the n-th round, you only toggle the last bulb. Find how many bulbs are on after n rounds.    
**Example:**
```
Input: 3
Output: 1 
Explanation: 
At first, the three bulbs are [off, off, off].
After first round, the three bulbs are [on, on, on].
After second round, the three bulbs are [on, off, on].
After third round, the three bulbs are [on, off, off]. 

So you should return 1, because there is only one bulb is on.
```
## 解题思路：
本题要我们模拟开关灯的情况，观察上面的例子可以得出，某一位置i的灯亮与否与它的`质因数个数`有关：当i的质因数个数为奇数时亮；反之不亮。  
所以问题转化为只要找到质因数个数为奇数的数的个数。而质因数个数为奇数的情况只能是平方数。
因此问题转为找<=n的平方数个数。而平方数个数sqrt(n)取整数部分就可得到。
## 代码：
``` C
class Solution {
public:
    int bulbSwitch(int n) {
        return sqrt(n);
    }
};
```