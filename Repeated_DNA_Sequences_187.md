# 187. Repeated DNA Sequences �����¼
## ��Ŀ������
All DNA is composed of a series of nucleotides abbreviated as A, C, G, and T, for example: "ACGAATTCCG". When studying DNA, it is sometimes useful to identify repeated sequences within the DNA.  
  
Write a function to find all the 10-letter-long sequences (substrings) that occur more than once in a DNA molecule.  
  
**Example:**  
```
Input: s = "AAAAACCCCCAAAAACCCCCCAAAAAGGGTTT"

Output: ["AAAAACCCCC", "CCCCCAAAAA"]
```
## ����˼·��
ֱ��10���ַ��ӽ�ȥһ��һ���Ƚϡ�
## ���룺
``` C
class Solution {
public:
    vector<string> findRepeatedDnaSequences(string s) {
        set<string> res, st;
        for (int i = 0; i + 9 < s.size(); ++i) {
            string t = s.substr(i, 10);
            if (st.count(t))
                res.insert(t);
            else
                st.insert(t);
        }
        return vector<string>{res.begin(), res.end()};
    }
};
```