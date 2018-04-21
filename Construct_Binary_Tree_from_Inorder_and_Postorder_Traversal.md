# 106. Construct Binary Tree from Inorder and Postorder Traversal 解题记录
## 题目描述：
Given inorder and postorder traversal of a tree, construct the binary tree.  
  
**Note:**  
You may assume that duplicates do not exist in the tree.  
  
For example, given  
```
inorder = [9,3,15,20,7]  
postorder = [9,15,7,20,3]  
```
Return the following binary tree:  
```
    3
   / \
  9  20
    /  \
   15   7
```
## 解题思路：
这题的思路和上一题没有多少区别，可以说连题目基本都一模一样，这题的postorder倒着看就相当于上一题的preorder，
只不过从优先左子树换成了优先右子树。  
## 代码：
```
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
    TreeNode* build(vector<int>& in, int inBeg, int inEnd, vector<int>& post, int postBeg, int postEnd){
        if(inBeg>inEnd || postBeg>postEnd)
            return NULL;
        int root_index = inBeg;
        for(; root_index <= inEnd; root_index++){
        //寻找根节点
            if(in[root_index] == post[postEnd])
                break;
        }
        TreeNode *root = new TreeNode(in[root_index]);
        int len = root_index - inBeg;
        root->right = build(in, root_index+1, inEnd, post, postBeg+len, postEnd-1);  //递归寻找右节点
        root->left = build(in, inBeg, root_index-1, post, postBeg, postBeg+len-1);  //递归寻找左节点
        return root;
    }
    TreeNode* buildTree(vector<int>& inorder, vector<int>& postorder) {
        int n = inorder.size()-1;
        return build(inorder, 0, n, postorder, 0, n);
    }
};
```