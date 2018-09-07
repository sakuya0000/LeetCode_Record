# 424. Longest Repeating Character Replacement �����¼
## ��Ŀ������
Given a string that consists of only uppercase English letters, you can replace any letter in the string with another letter at most k times. Find the length of a longest substring containing all repeating letters you can get after performing the above operations.    

**Note:**  
Both the string's length and k will not exceed 104.    

**Example 1:**  
```
Input:
s = "ABAB", k = 2

Output:
4

Explanation:
Replace the two 'A's with two 'B's or vice versa.
```

**Example 2:**  

```
Input:
s = "AABABBA", k = 1

Output:
4

Explanation:
Replace the one 'A' in the middle with 'B' and form "AABBBBA".
The substring "BBBB" has the longest repeating letters, which is 4.
```
## ����˼·��
������Ҫ�����ƶ����ڣ���¼������ÿ����ĸ��������Ȼ������һ��most��¼����������Ȼ����㿪ʼ�����ַ������Ƚϴ��ڵĳ�����most+k�������ڣ��ƶ�������ࣻ��С�ڣ��򽫷��ؽ���봰�ڴ�С�Ƚϡ�
## ���룺
``` C
class Solution {
public:
    int characterReplacement(string s, int k) {
        int n = s.length();
        if(n == 0) return 0;
        vector<int> map(91, 0);
        int ret = 1, left = 0, most = 0;
        for(int right = 0; right < n; right++){
            most = max(most, ++map[s[right]]);
            if(right - left >= most + k)
                map[s[left++]]--;
            else
                ret = max(ret, right - left + 1);
        }
        return ret;
    }
};
```