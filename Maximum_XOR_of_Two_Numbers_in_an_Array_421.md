# 421. Maximum XOR of Two Numbers in an Array 解题记录
## 题目描述：
Given a **non-empty** array of numbers, a<sub>0</sub>, a<sub>1</sub>, a<sub>2</sub>, … , a<sub>n-1</sub>, where 0 ≤ a<sub>i</sub> < 2<sup>31</sup>.    

Find the maximum result of a<sub>i</sub> XOR a<sub>j</sub>, where 0 ≤ *i*, *j* < *n*.    

Could you do this in O(*n*) runtime?    

### Example: 
```
Input: [3, 10, 5, 25, 2, 8]

Output: 28

Explanation: The maximum result is 5 ^ 25 = 28.
```
## 解题思路：
既然题目说了a<sub>i</sub>的二进制位数最多到32位，那么可以首位开始遍历，一位一位地加到最大值ret中。
首先我们要把nums中的数字二进制的前 *i* 位储存在一个集合hash中，然后我们假设nums中存在两个数字异或后使ret的 *i* 位为1，即`t = ret | (1 << i)`。
接着就要用异或运算的一个性质 ` a ^ b = c 则 a ^ c = b`，将 *t* 与刚刚储存的set中的元素进行异或运算，如果可以在set中找到`t ^ hash[i]`，那么就说明存在集合中存在两个元素`a ^ b = t`。
当然这只是前 *i* 位的最大值ret，但根据异或运算的特性，前 *i* 位的运算是可以跟后 *i* 位分开的，所以只要依次遍历就可以得到最后的ret。
## 代码：
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