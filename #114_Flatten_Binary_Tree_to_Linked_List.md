# 114. Flatten Binary Tree to Linked List 解题记录
## 题目描述：
Given a binary tree, flatten it to a linked list in-place.  
  
For example, given the following tree:  
```
    1
   / \
  2   5
 / \   \
3   4   6
```
The flattened tree should look like:  
```
1
 \
  2
   \
    3
     \
      4
       \
        5
         \
          6
```
## 解题思路：
本题要先将左子树和右子树调换位置，确保将最小的节点放在右边，以免对节点进行操作赋值后找不到右节点。  
然后就以添加根节点，右节点、左节点的顺序一直递归添加处理就行了。  
如果题目的要求是放在左节点的话就可以免掉调换位置的步骤，效率也会更高一点。
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
    TreeNode* ListRoot = NULL;  //用来记录添加的位置
    void transform(TreeNode* root){
        if(!root)
            return;
        TreeNode* temp_right =root->right;
        root->right = root->left;
        root->left = temp_right;
        ListRoot->right = root;  //添加根节点
        ListRoot = ListRoot->right;
        transform(root->right);  //先右
        transform(root->left);  //后左
        root->left = NULL;  //再将左节点清空
    }
    void flatten(TreeNode* root) {
        ListRoot = new TreeNode(0);
        transform(root);
    }
};
```