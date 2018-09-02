# 423. Reconstruct Original Digits from English �����¼
## ��Ŀ������
Given a **non-empty** string containing an out-of-order English representation of digits `0-9`, output the digits in ascending order.    
**Note:**    
1. Input contains only lowercase English letters.

2. Input is guaranteed to be valid and can be transformed to its original digits. That means invalid inputs such as "abc" or "zerone" are not permitted.

3. Input length is less than 50,000.

**Example 1:**  
```
Input: "owoztneoer"

Output: "012"
```
**Example 2:**  
```
Input: "fviefuro"

Output: "45"
```
## ����˼·��
��������ͼ���ַ�����������࣬��¼ÿ����ĸ�ĸ�����Ȼ���ٸ���`0-9`Ӣ���к��еıȽ�������ַ�����¼ÿ�����ֵĸ���������`z`ֻ��`0`�У�`w`ֻ��`2`�еȵȡ������ת���ַ�����
## ���룺
``` C
class Solution {
public:
    string originalDigits(string s) {
        int n = s.length();
        vector<int> map(123, 0), nums(10, 0);
        for(int i = 0; i < n; i++){
            map[s[i]]++;
        }
        nums[0] = map['z'];
	    map['r'] -= nums[0];
        map['o'] -= nums[0];
	    nums[2] = map['w'];
        map['o'] -= nums[2];
	    nums[4] = map['u'];
        map['o'] -= nums[4];
	    map['r'] -= nums[4];
	    map['f'] -= nums[4];
	    nums[6] = map['x'];
	    map['s'] -= nums[6];
	    nums[7] = map['s'];
	    map['n'] -= nums[7];
	    nums[8] = map['g'];
	    nums[3] = map['r'];
	    map['e'] -= 2 * nums[3];
	    nums[5] = map['f'];
	    map['e'] -= nums[5];
	    nums[1] = map['o'];
	    map['n'] -= nums[1];
	    nums[9] = map['n'] / 2;
        string ret;
        for(int i = 0; i < 10; i++){
            while(nums[i]--){
                ret += char(i + '0');
            }
        }
        return ret;
    }
};
```