# 145. Binary Tree Postorder Traversal 解题记录
## 题目描述：
Given a binary tree, return the postorder traversal of its nodes' values.  
  
**Example:**  
  
```
Input: [1,null,2,3]
   1
    \
     2
    /
   3

Output: [3,2,1]
```
  
**Follow up:** Recursive solution is trivial, could you do it iteratively?  
## 解题思路：
一开始没有看到那个Follow up，用递归做了一遍，后来写报告的时候看到了，就重新用迭代做了一遍。  
  
因为递归的实现很容易，思路也就没什么好讲了。  
  
用迭代来写的话就不好直接从二叉树的末尾开始加了，所以我采用从根节点开始加，然后再加右子树，最后加左子树的方法。  
最后再反转数组就可以得到逆序前序遍历的数组了。
## 代码（递归）：
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
public:
    void addElement(TreeNode* cur, vector<int> &ret){
        if(!cur)
            return;
        addElement(cur->left, ret);
        addElement(cur->right, ret);
        ret.push_back(cur->val);
    }
    vector<int> postorderTraversal(TreeNode* root) {
        vector<int> ret;
        addElement(root, ret);
        return ret;
    }
};
```
## 代码（迭代）：
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
public:
    vector<int> postorderTraversal(TreeNode* root) {
        vector<int> ret;
        stack<TreeNode*> leftNodes;  //用栈来储存左节点位置
        while(root){
            ret.push_back(root->val);
            if(root->right){
            //先查看右节点是否存在
                if(root->left){
                //若有左节点就让其进栈
                    leftNodes.push(root->left);
                }
                root = root->right;
                continue;
            }
            if(root->left){
            //左节点不存在，再看右节点是否存在
                root = root->left;
                continue;
            }
            if(leftNodes.size()){
            //都不存在再看栈中是否存在节点
                root = leftNodes.top();
                leftNodes.pop();
                continue;
            }
            break;  //最后全都不存在就退出循环
        }
        reverse(ret.begin(), ret.end());
        return ret;
    }
};
```