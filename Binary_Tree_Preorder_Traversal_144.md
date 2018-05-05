# 144. Binary Tree Preorder Traversal 解题记录
## 题目描述：
Given a binary tree, return the preorder traversal of its nodes' values.  
  
**Example:**  
```
<strong>Input:</strong> [1,null,2,3]
   1
    \
     2
    /
   3

<strong>Output: </strong>[1,2,3]
```
  
**Follow up:** Recursive solution is trivial, could you do it iteratively?  
## 解题思路：
利用递归进行前序遍历。
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
public:
    void preorder(TreeNode* root, vector<int> &ret){
        if(!root)
            return;
        ret.push_back(root->val);
        preorder(root->left, ret);
        preorder(root->right, ret);
    }
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> ret;
        preorder(root, ret);
        return ret;
    }
};
```