# 372. Super Pow �����¼
## ��Ŀ������
Your task is to calculate ab mod 1337 where a is a positive integer and b is an extremely large positive integer given in the form of an array.    

**Example1:**
```
a = 2
b = [3]

Result: 8
```
**Example2:**
```
a = 2
b = [1,0]

Result: 1024
```
## ����˼·��
����һ����ѧ�⡣����Ҫ֪��һ����ʽ(a<sup>b</sup>)%c = (a%c)<sup>b</sup>%c�����ǽⷨ�ĺ��ġ�  
Ȼ����bΪż��������£�(a<sup>2*b/2</sup>)%c = (a<sup>2</sup>%c)<sup>b/2</sup>%c;  
������������ǣ�(a<sup>2*b/2</sup>*a)%c = [(a<sup>2</sup>%c)<sup>b/2</sup>%c*a]%c��  
Ȼ��һֱ������ȥ�Ϳ��Եõ����ˡ�
## ���룺
``` C
class Solution {
    vector<int> func(vector<int> &b, int &flag){//0
        vector<int> ret;
        bool beg = 0;
        for(int i = 0; i < b.size(); i++){
            flag *= 10;
            flag += b[i];
            int t = flag / 2;
            if(t > 0)
                beg = 1;
            if(beg)
                ret.push_back(t);
            flag %= 2;
        }
        return ret;
    }
public:
    int superPow(int a, vector<int>& b) {
        int ret = 1;
        a %= 1337;
        if(b.size() == 1 && b[0] == 0) return 1;
        while(b.size() > 0){
            int flag = 0;
            b = func(b, flag);
            if(flag == 1){
                ret = (ret * a) % 1337;
            }
            a = (a * a) % 1337;
        }
        return ret;
    }
};
```