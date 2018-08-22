# 421. Maximum XOR of Two Numbers in an Array �����¼
## ��Ŀ������
Given a **non-empty** array of numbers, a<sub>0</sub>, a<sub>1</sub>, a<sub>2</sub>, �� , a<sub>n-1</sub>, where 0 �� a<sub>i</sub> < 2<sup>31</sup>.    

Find the maximum result of a<sub>i</sub> XOR a<sub>j</sub>, where 0 �� *i*, *j* < *n*.    

Could you do this in O(*n*) runtime?    

### Example: 
```
Input: [3, 10, 5, 25, 2, 8]

Output: 28

Explanation: The maximum result is 5 ^ 25 = 28.
```
## ����˼·��
��Ȼ��Ŀ˵��a<sub>i</sub>�Ķ�����λ����ൽ32λ����ô������λ��ʼ������һλһλ�ؼӵ����ֵret�С�
��������Ҫ��nums�е����ֶ����Ƶ�ǰ *i* λ������һ������hash�У�Ȼ�����Ǽ���nums�д���������������ʹret�� *i* λΪ1����`t = ret | (1 << i)`��
���ž�Ҫ����������һ������ ` a ^ b = c �� a ^ c = b`���� *t* ��ոմ����set�е�Ԫ�ؽ���������㣬���������set���ҵ�`t ^ hash[i]`����ô��˵�����ڼ����д�������Ԫ��`a ^ b = t`��
��Ȼ��ֻ��ǰ *i* λ�����ֵret�������������������ԣ�ǰ *i* λ�������ǿ��Ը��� *i* λ�ֿ��ģ�����ֻҪ���α����Ϳ��Եõ�����ret��
## ���룺
``` C
class Solution {
public:
    int findMaximumXOR(vector<int>& nums) {
        int mask = 0, ret = 0, n = nums.size();
        for(int i = 31; i >= 0; i--){
            mask |= (1 << i);
            unordered_set<int> hash;
            for(int j = 0; j < n; j++) hash.insert(mask & nums[j]);
            int t = ret | (1 << i);
            for(unordered_set<int>::iterator it = hash.begin(); it != hash.end(); it++){
                if(hash.count(t ^ *it)){
                    ret = t;
                    break;
                }
            }
        }
        return ret;
    }
};
```