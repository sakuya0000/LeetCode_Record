# 365. Water and Jug Problem 解题记录
## 题目描述：
You are given two jugs with capacities x and y litres. There is an infinite amount of water supply available. You need to determine whether it is possible to measure exactly z litres using these two jugs.    

If z liters of water is measurable, you must have z liters of water contained within **one or both buckets** by the end.    

Operations allowed:    

- Fill any of the jugs completely with water.  
- Empty any of the jugs.  
- Pour water from one jug into another till the other jug is completely full or the first jug itself is empty.

**Example 1: **(From the famous "Die Hard" example)
```
Input: x = 3, y = 5, z = 4
Output: True
```    
**Example 2:**
```
Input: x = 2, y = 6, z = 5
Output: False
```
## 解题思路：
这道问题可以转换为有一个z升的容器，有两个杯子容量分别为x升和y升。然后我们用这个两个杯子舀进和舀出水，使得水正好填满z升容器。  
用数学语言来表达就是z=m*x+n*y(m, n为任意整数)，又通过裴蜀定理得到z是x和y的最大公约数的倍数。所以问题最后变为找x和y的最大公约数。  
这道题再次向我们展示了数学在算法设计中是多么重要。
## 代码：
``` C
class Solution {
public:
    bool canMeasureWater(int x, int y, int z) {
        return z == 0 || (x + y >= z && z % gcd(x, y) == 0);
    }
    int gcd(int x, int y) {
        return y == 0 ? x : gcd(y, x % y);
    }
};
```