# 412. Fizz Buzz 解题记录
## 题目描述：
Write a program that outputs the string representation of numbers from 1 to *n*.    
But for multiples of three it should output “Fizz” instead of the number and for the multiples of five output “Buzz”. For numbers which are multiples of both three and five output “FizzBuzz”.    
**Example: **
```
n = 15,

Return:
[
    "1",
    "2",
    "Fizz",
    "4",
    "Buzz",
    "Fizz",
    "7",
    "8",
    "Fizz",
    "Buzz",
    "11",
    "Fizz",
    "13",
    "14",
    "FizzBuzz"
]
```
## 解题思路：
整除3和整除5的时候加上相应的字符串就行了。
## 代码：
``` C
class Solution {
public:
    vector<string> fizzBuzz(int n) {
        vector<string> ret;
        for(int i = 1; i <= n; i++){
            bool flag = 0;
            string str;
            if(i % 3 == 0){
                str = "Fizz";
                flag = 1;
            }
            if(i % 5 == 0){
                str += "Buzz";
                flag = 1;
            }
            if(!flag){
                str = std::to_string(i);
            }
            ret.push_back(str);
        }
        return ret;
    }
};
```