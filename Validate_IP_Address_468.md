# 468. Validate IP Address
## 题目描述：
Write a function to check whether an input string is a valid IPv4 address or IPv6 address or neither.   
  
**IPv4** addresses are canonically represented in dot-decimal notation, which consists of four decimal numbers, each ranging from 0 to 255, separated by dots ("."), e.g.,`172.16.254.1`;  
  
Besides, leading zeros in the IPv4 is invalid. For example, the address `172.16.254.01` is invalid.  
  
**IPv6** addresses are represented as eight groups of four hexadecimal digits, each group representing 16 bits. The groups are separated by colons (":"). For example, the address `2001:0db8:85a3:0000:0000:8a2e:0370:7334` is a valid one. Also, we could omit some leading zeros among four hexadecimal digits and some low-case characters in the address to upper-case ones, so `2001:db8:85a3:0:0:8A2E:0370:7334` is also a valid IPv6 address(Omit leading zeros and using upper cases).   
  
However, we don't replace a consecutive group of zero value with a single empty group using two consecutive colons (::) to pursue simplicity. For example, `2001:0db8:85a3::8A2E:0370:7334` is an invalid IPv6 address.   
  
Besides, extra leading zeros in the IPv6 is also invalid. For example, the address `02001:0db8:85a3:0000:0000:8a2e:0370:7334` is invalid.   
  
**Note:** You may assume there is no extra space or special characters in the input string.   
  
**Example 1:**
```
Input: "172.16.254.1"

Output: "IPv4"

Explanation: This is a valid IPv4 address, return "IPv4".
```
  
**Example 2:**
```
Input: "2001:0db8:85a3:0:0:8A2E:0370:7334"

Output: "IPv6"

Explanation: This is a valid IPv6 address, return "IPv6".
```
  
**Example 3:**
```
Input: "256.256.256.256"

Output: "Neither"

Explanation: This is neither a IPv4 address nor a IPv6 address.
```
  
## 解题思路：
首先判断这个字符串是IPv4格式的还是IPv6格式的，然后分别进行检测是否符合地址规则。判断基准是：字符串中是否有`.`字符，有则进入IPv4判断函数，没有则进入IPv6判断函数。  
  
在判断IPv4的时候，将不符合的格式列出：
> 1. 出现不在`0-9`中或是不是`.`的字符；
> 2. 某一小串字符出现了前导零（只有一个0不算前导零）；
> 3. 连续出现两个`.`或字符串首尾出现`.`；
> 4. 某一小串字符代表的数字超过了255；
> 5. 出现`.`的数量不是3个。
  
在判断IPv6的时候，也将不符合的格式列出：
> 1. 出现不在`0-9`或`:`或`a-f`或`A-F`的字符；
> 2. 某小串字符的字符数超过了4；
> 3. 连续出现两个`:`或字符串首尾出现`:`；
> 4. 出现`:`的数量不是7个。
  
最后再根据判断的情况返回字符串就可以了。
## 代码：
``` C
class Solution {
    bool checkIPv4(string IP){
        bool res = 1;
        int t = 0;
        int n = IP.length();
        int dotcnt = 0, cnt = 0, last = 0;
        for(int i = 0; i < n; i++){
            if((!((IP[i]>='0'&&IP[i]<='9')||IP[i]=='.')) || t > 255){
                res = 0;
                break;
            }
            if(IP[i] == '.'){
                if((IP[last] == '0' && cnt != 1) || last == i){
                    res = 0;
                    break;
                }
                dotcnt++;
                t = 0;
                last = i+1;
                cnt = 0;
                continue;
            }
            cnt++;
            t *= 10;
            t += IP[i] - '0';
        }
        if(cnt == 0 || t > 255 || dotcnt!=3 || cnt > 3 || (cnt != 1 && IP[last] == '0'))
            res = 0;
        return res;
    }
    
    bool checkIPv6(string IP){
        int n = IP.length();
        bool res = 1;
        int cnt = 0;
        int last = 0;
        int dotcnt = 0;
        for(int i = 0; i < n; i++){
            if((!((IP[i]>='0'&&IP[i]<='9')||(IP[i]>='a'&&IP[i]<='f')||(IP[i]>='A'&&IP[i]<='F')||IP[i]==':')) || cnt > 4){
                res = 0;
                break;
            }
            if(IP[i] == ':'){
                if(i == last){
                    res = 0;
                    break;
                }
                dotcnt++;
                last = i+1;
                cnt = 0;
                continue;
            }
            cnt++;
        }
        if(cnt > 4 || dotcnt != 7 || cnt == 0) res = 0;
        return res;
    }
    
    
public:
    string validIPAddress(string IP) {
        bool isIPv4 = 0;
        bool ans = 0;
        string res;
        int n = IP.length();
        for(int i = 0; i < n; i++){
            if(IP[i] == '.'){
                isIPv4 = 1;
                break;
            }
            if(IP[i] == ':'){
                isIPv4 = 0;
                break;
            }
        }
        if(isIPv4){
            if(checkIPv4(IP))
                res = "IPv4";
            else 
                res = "Neither";
        }
        else{
            if(checkIPv6(IP))
                res = "IPv6";
            else
                res = "Neither";
        }
        return res;
    }
};
```