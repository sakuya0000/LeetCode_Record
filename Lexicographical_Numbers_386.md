# 386. Lexicographical Numbers �����¼
## ��Ŀ������
Given an integer n, return 1 - *n* in lexicographical order.     
For example, given 13, return: [1,10,11,12,13,2,3,4,5,6,7,8,9].     
Please optimize your algorithm to use less time and space. The input size may be as large as 5,000,000.     
## ����˼·��
�������ֻҪ�˽��ֵ������������ģ�Ȼ��������򷽷��������ӾͿ����ˡ�  
1. ���һ������10û�г���n����ô��һ�����ض����������10;  
2. ���һ����+1����10�ı�������ô��һ�����������+1;  
3. �����10�ı�������ôѭ����10ֱ������10�ı��������������Ϊ199ʱ���¸���Ϊ200;  
4. ����һ�ֶ����������������=n����������ʱ��Ͳ���ֱ��+1�ˣ������԰����������10��+1����2��3������жϡ�����n=159����һ����Ϊ16��
## ���룺
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