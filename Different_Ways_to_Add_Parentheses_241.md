# 241.Different Ways to Add Parentheses 解题记录
## 题目描述：
Given a string of numbers and operators, return all possible results from computing all the different possible ways to group numbers and operators. 
The valid operators are `+`, `-` and `*`.
## 解题思路：
利用递归将计算分为两边不同的可能性求加、减、乘。利用递归化到最后就是最简单的加、减、乘问题。
## 代码：
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
                vector<int> result1=diffWaysToCompute(input.substr(0,k));  //化成两边计算
                vector<int> result2=diffWaysToCompute(input.substr(k+1));
                for(vector<int>::iterator i=result1.begin();i!=result1.end();i++)  //对两边不同都进行求结果
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
        if(result.empty())  //只有数字的情况
            result.push_back(atoi(input.c_str()));
        return result;
    }
};
```