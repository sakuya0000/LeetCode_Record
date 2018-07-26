# 338. Counting Bits �����¼
## ��Ŀ������
Given a non negative integer number num. For every numbers i in the range **0 �� i �� num** calculate the number of 1's in their binary representation and return them as an array.     
Example:  
For `num = 5` you should return `[0,1,1,2,1,2]`.   
## ����˼·��
��������ö�̬�滮����ɣ����ƹ�ʽΪf(a)=f(2<sup>n</sup>)+f(b)��(b<=2<sup>n</sup>)��
## ���룺
``` C
class Solution {
public:
    vector<int> countBits(int num) {
        if(num == 0) return vector<int>(1, 0);
        vector<int> ret(num+1, 1);
        ret[0] = 0;
        for(int t = 2; t < num; t *= 2){
            for(int i = 1; i < t && t+i <= num; i++){
                ret[i+t] = ret[t] + ret[i];
            }
        }
        return ret;
    }
};
```