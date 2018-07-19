# 299. Bulls and Cows 解题记录
## 题目描述：
ou are playing the following Bulls and Cows game with your friend: You write down a number and ask your friend to guess what the number is. Each time your friend makes a guess, you provide a hint that indicates how many digits in said guess match your secret number exactly in both digit and position (called "bulls") and how many digits match the secret number but locate in the wrong position (called "cows"). Your friend will use successive guesses and hints to eventually derive the secret number.    
Write a function to return a hint according to the secret number and friend's guess, use A to indicate the bulls and B to indicate the cows.     
Please note that both secret number and friend's guess may contain duplicate digits.    
**Example 1:**
```
Input: secret = "1807", guess = "7810"

Output: "1A3B"

Explanation: 1 bull and 3 cows. The bull is 8, the cows are 0, 1 and 7.
```  
**Example 2:**
```
Input: secret = "1123", guess = "0111"

Output: "1A1B"

Explanation: The 1st 1 in friend's guess is a bull, the 2nd or 3rd 1 is a cow.
```
## 解题思路：
先遍历一遍字符串，把secret和guess中对应的数字找出来，用**A_num**记录**对应的数字数量**，同时也将secret中没有对应的数字用一个数组nums记录数量。  
然后遍历一遍guess字符串，查找B_num，即遍历每一个元素，查看nums数组中对应数字的数量是否不为0。若不为0则让B_num加1，且数量减1。
## 代码：
``` C
class Solution {
    string integerToString(int n) {
        ostringstream stream;
        stream << n;
        return stream.str();
    }
public:
    string getHint(string secret, string guess) {
        vector<int> nums(10, 0);
        int n = secret.length(), A_num = 0, B_num = 0;
        for(int i = 0; i < n; i++){  //查找A_num
            if(secret[i] == guess[i]){
                A_num++;
                guess[i] = 'A';
                continue;
            }
            nums[secret[i]-48]++;
        }
        for(int i = 0; i < n; i++){  //查找B_num
            if(guess[i] == 'A')
                continue;
            if(nums[guess[i]-48]){
                B_num++;
                nums[guess[i]-48]--;
            }
        }
        string ret = integerToString(A_num)+"A"+integerToString(B_num)+"B";
        return ret;
    }
};
```