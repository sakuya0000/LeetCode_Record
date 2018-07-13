# 241.Different Ways to Add Parentheses 解题记录
## 题目描述：
Given a string of numbers and operators, return all possible results from computing all the different possible ways to group numbers and operators. 
The valid operators are `+`, `-` and `*`.
## 解题思路：
利用递归的方法依据计算符号将计算分为两个计算，求加、减、乘。这样一直递归化到最后就是最简单的加、减、乘问题。
然后再将下一层两个计算的可能性分别进行求加、减、乘，就得到当前计算层的所有可能性，将其返回上层。
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