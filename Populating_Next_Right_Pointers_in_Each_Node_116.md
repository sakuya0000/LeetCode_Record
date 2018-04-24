# 116. Populating Next Right Pointers in Each Node 解题记录
## 题目描述：
Given a binary tree  
```
struct TreeLinkNode {
  TreeLinkNode *left;
  TreeLinkNode *right;
  TreeLinkNode *next;
}
```
Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to `NULL`.  
  
Initially, all next pointers are set to `NULL`.  
  
**Note:**  
  
- You may only use constant extra space  
- Recursive approach is fine, implicit stack space does not count as extra space for this problem.  
- You may assume that it is a perfect binary tree (ie, all leaves are at the same level, and every parent has two children).  
  
**Exmaple:**  
  
Given the following perfect binary tree,  
```
     1
   /  \
  2    3
 / \  / \
4  5  6  7
```
After calling your function, the tree should look like:  
```
     1 -> NULL
   /  \
  2 -> 3 -> NULL
 / \  / \
4->5->6->7 -> NULL
```
## 解题思路：
本题我的解题思路是建立在Note中的第三个信息：  
```
You may assume that it is a perfect binary tree (ie, all leaves are at the same level, and every parent has two children).
```
既然层数相同就不必用递归来解决，可以直接用循环来遍历，避免消耗多余的空间。  
  
- 首先可以在第一层进行连接下一层，也就是第二层，然后让指针转移到下一层的最左节点。  
- 然后在n层也是如此，进行连接下一层，就是n+1层，然后转移到下一层的最左节点。
- 以此循环往复就可以遍历到所有节点。
## 代码：
``` C
/**
 * Definition for binary tree with next pointer.
 * struct TreeLinkNode {
 *  int val;
 *  TreeLinkNode *left, *right, *next;
 *  TreeLinkNode(int x) : val(x), left(NULL), right(NULL), next(NULL) {}
 * };
 */
class Solution {
public:
    void connect(TreeLinkNode *root) {
        if(!root)
            return;
        TreeLinkNode *cur;
        while(root->left){
            cur = root;  //用于遍历当前层的所有节点
            while(cur){
            //遍历当前层
                cur->left->next = cur->right;  //连接下一层左到右节点
                if(cur->next)
                    cur->right->next = cur->next->left;  //若当前节点右边存在节点，则连接下一层右节点到左节点
                cur = cur->next;
            }
            root = root->left;  //连接下一层完毕后转移指针到下一层最左
        }
    }
};
```