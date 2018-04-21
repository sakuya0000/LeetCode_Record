# 105. Construct Binary Tree from Preorder and Inorder Traversal 解题记录
## 题目描述：
Given preorder and inorder traversal of a tree, construct the binary tree.  
**Note:**  
You may assume that duplicates do not exist in the tree.  
For example, given  
```
preorder = [3,9,20,15,7]
inorder = [9,3,15,20,7]
```
Return the following binary tree:  
```
    3
   / \
  9  20
    /  \
   15   7
``` C
## 解题思路：
这题的基本思路是从前序遍历的数组中获取根节点，然后在中序遍历的数组中找到根节点所在的位置，左边即为左子数组，右边为右子数组。  
用递归来进行遍历，每次递归缩小两个遍历数组的范围。
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
    TreeNode *build(vector<int>& pre, int preBeg, int preEnd, vector<int>& in, int inBeg, int inEnd){
        if(inBeg>inEnd || preBeg>preEnd)
            return NULL;
        int rootIndex = 0;
        for(int i = 0; i <= inEnd; i++)
            if(in[i] == pre[preBeg]){
                rootIndex = i;
                break;
            }
        int len = rootIndex - inBeg;
        TreeNode *root = new TreeNode(pre[preBeg]);
        root->left = build(pre, preBeg+1, preBeg+len, in, inBeg, rootIndex-1);
        root->right = build(pre, preBeg+len+1, preEnd, in, rootIndex+1, inEnd);
        return root;
    }
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        int preLen = preorder.size();
        return build(preorder, 0, preLen-1, inorder, 0, preLen-1);
    }
};
```