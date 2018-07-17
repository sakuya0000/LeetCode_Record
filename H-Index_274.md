# 274. H-Index �����¼
## ��Ŀ������
Pick One

Given an array of citations (each citation is a non-negative integer) of a researcher, write a function to compute the researcher's h-index.  
  **Example:**  
```
Input: citations = [3,0,6,1,5]
Output: 3 
Explanation: [3,0,6,1,5] means the researcher has 5 papers in total and each of them had 
             received 3, 0, 6, 1, 5 citations respectively. 
             Since the researcher has 3 papers with at least 3 citations each and the remaining 
             two with no more than 3 citations each, her h-index is 3.
```
## ����˼·��
�����İ��������Ӵ�С�ţ���ű���������ľ���Hָ����
## ���룺
``` C
class Solution {
public:
    int hIndex(vector<int>& citations) {
        int n = citations.size();
        if(n == 0)
            return 0;
        sort(citations.begin(), citations.end());
        int result = 0;
        for(int i = 1; i <= n; i++){
            if(citations[n - i] >= i)
                result = i;
            else 
                break;
        }
        return result;

    }
};
```