# 96. Unique Binary Search Trees 解题记录
## 题目描述：
Given n, how many structurally unique `BST's` (binary search trees) that store values 1...n?  
  
For example,  
Given n = 3, there are a total of 5 unique BST's.  
```
   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3
```
## 解题思路：
这题可以用卡特兰数来解决这道题，其解h(n)=C(2n, n)/(n+1)!。  
## 代码：
``` C
class Solution {
public:
    int numTrees(int n) {
        long long ret = 1;
        for(int i = n+1; i <= 2*n; i++)
            ret = ret*i/(i-n);
        return ret/(n+1);
    }
};
```