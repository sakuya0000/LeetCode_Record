# 241.Different Ways to Add Parentheses �����¼
## ��Ŀ������
Given a string of numbers and operators, return all possible results from computing all the different possible ways to group numbers and operators. 
The valid operators are `+`, `-` and `*`.
## ����˼·��
���õݹ�ķ������ݼ�����Ž������Ϊ�������㣬��ӡ������ˡ�����һֱ�ݹ黯����������򵥵ļӡ����������⡣
Ȼ���ٽ���һ����������Ŀ����Էֱ������ӡ������ˣ��͵õ���ǰ���������п����ԣ����䷵���ϲ㡣
## ���룺
``` C
class Solution {
public:
    vector<int> diffWaysToCompute(string input) {
        vector<int> result;
        int len=input.size();
        for(int k=0;k<len;k++)
        {
            if(input[k]=='+'||input[k]=='-'||input[k]=='*')
            {
                vector<int> result1=diffWaysToCompute(input.substr(0,k));  //�������߼���
                vector<int> result2=diffWaysToCompute(input.substr(k+1));
                for(vector<int>::iterator i=result1.begin();i!=result1.end();i++)  //�����߲�ͬ����������
                    for(vector<int>::iterator j=result2.begin();j!=result2.end();j++)
                    {
                        if(input[k]=='+')
                            result.push_back((*i)+(*j));
                        else if(input[k]=='-')
                            result.push_back((*i)-(*j));
                        else
                            result.push_back((*i)*(*j));
                    }
            }
        }
        if(result.empty())  //ֻ�����ֵ����
            result.push_back(atoi(input.c_str()));
        return result;
    }
};
```