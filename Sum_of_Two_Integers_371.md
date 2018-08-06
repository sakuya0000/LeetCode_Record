# 371. Sum of Two Integers �����¼
## ��Ŀ������
Calculate the sum of two integers *a* and *b*, but you are **not allowed** to use the operator `+` and `-`.    
**Example:**  
Given *a* = 1 and *b* = 2, return 3. 
## ����˼·��
���ⲻ�����üӼ��ţ�����ֻ�ܿ���λ���㡣a^b��ʾa+b����Ӧλ��ӣ���û�п��ǽ�λ��Ҳ����˵19^1�Ľ��Ϊ10����a&b��ʾa+b�Ľ�λ
��Ҳ����˵19&1�Ľ��Ϊ1������һֱѭ��a^b����b�������λ�Ϳ��Եõ����Ľ���ˡ�
## ���룺
``` C
class Solution {
public:
    int getSum(int a, int b) {
        while(b){
            int t = a ^ b;  //��Ӧλ���
            b = (a & b) << 1;  //��λ
            a = t;
        }
        return a;
    }
};
```