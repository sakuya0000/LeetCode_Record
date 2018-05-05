# 144. Binary Tree Preorder Traversal �����¼
## ��Ŀ������
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
## ����˼·��
���õݹ����ǰ�������
## ���룺
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