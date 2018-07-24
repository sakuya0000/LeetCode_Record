# 326. Power of Three �����¼
## ��Ŀ������
Given an integer, write a function to determine if it is a power of three.    
**Example 1:**
```
Input: 27
Output: true
```  
**Example 2:**
```
Input: 0
Output: false
```
## ����˼·��
��nһֱ����3������������Ϊ0��ʱ������ѭ��������ж�һ��n�Ƿ����1��
## ���룺
``` C
class Solution {
public:
    bool isPowerOfThree(int n) {
        if(n == 0) return false;
        while(n%3 == 0){
            n /= 3;
        }
        if(n == 1) return true;
        return false;
    }
};
```