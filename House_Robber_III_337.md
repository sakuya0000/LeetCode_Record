# 337. House Robber III 解题记录
## 题目描述：
The thief has found himself a new place for his thievery again. There is only one entrance to this area, called the "root." Besides the root, each house has one and only one parent house. After a tour, the smart thief realized that "all houses in this place forms a binary tree". It will automatically contact the police if two directly-linked houses were broken into on the same night.     
Determine the maximum amount of money the thief can rob tonight without alerting the police.       
**Example 1:**    
```
     3
    / \
   2   3
    \   \ 
     3   1
```  
Maximum amount of money the thief can rob = **3 + 3 + 1 = 7**.    
**Example 2:**
```
     3
    / \
   4   5
  / \   \ 
 1   3   1
```
Maximum amount of money the thief can rob = **4 + 5 = 9**.    
## 解题思路：
本题每个节点的情况有两种：  
1. 取了根节点，那么下一层的节点就不可取。  
2. 不取根节点，那么下一层的节点取或不取都行。    
所以递归的时候返回的数据就有两个，可用数组ret存起来。ret[0]代表取了情况1，ret[1]代表情况2。
## 代码：
``` C
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */

class Solution {
    vector<int> getMoney(TreeNode* node) {
        vector<int> ret(2, 0);
        if(!node) return ret;
        vector<int> lRet = getMoney(node->left);
        vector<int> rRet = getMoney(node->right);
        ret[0] = lRet[1] + rRet[1] + node->val;  //用下一层没取根节点的情况+根节点
        ret[1] = max(lRet[0], lRet[1]) + max(rRet[0], rRet[1]);  //因为下一层可取可不取根节点，所以都要比较
        return ret;
    }
public:
    int rob(TreeNode* root) {
        vector<int> ret = getMoney(root);
        return max(ret[0], ret[1]);
    }
};
```