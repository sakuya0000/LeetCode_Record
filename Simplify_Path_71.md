# 71. Simplify Path
## 题目描述：
Given an absolute path for a file (Unix-style), simplify it.  
> For example,  
> **path** = "/home/", => "/home"  
> **path** = "/a/./b/../../c/", => "/c"  

Corner Cases:  
- Did you consider the case where path = "/../"?  
	In this case, you should return "/".  
- Another corner case is the path might contain multiple slashes '/' together, such as "/home//foo/".  
	In this case, you should ignore redundant slashes and return "/home/foo".  
## 解题思路：
这题的特殊情况有三个：多个'/'字符，"../"字符串和"./"字符串。因此我在遍历的时候直接略过'/'添加其他数组，再将得到的子数组与".."和"."比较，每次比较清空得到的字符串。  
## 代码：
``` C
class Solution {
public:
    string simplifyPath(string path) {
        string ret, temp;
        int n = path.length();
        for (int i = 0; i < n; i++) {
            if (path[i] == '/') {
                        //以'/'为触发添加情况
                if (temp.empty())
                                //temp为空串
                    continue;
                if (temp == ".") {
                                //temp为'.'
                    temp.clear();
                    continue;
                }
                if (temp == "..") {
                                //temp为".."
                    int next = ret.rfind("/");
                    if (next > 0)
                                        //防止ret为空串，next为-1的情况
                        ret.erase(ret.begin() + next, ret.end());
                    else
                        ret.clear();
                    temp.clear();
                }
                else {
                                //添加
                    ret = ret + '/' + temp;
                    temp.clear();
                }
            }
            else
                temp += path[i];
        }
        if (temp == ".." && ret.length()>1) {
                //因为以'/'为添加条件，可能会碰到最后一个字符不是'/'的情况，所以最后要再比较一次
            ret.erase(ret.begin() + ret.rfind("/"), ret.end());
        }
        if (temp != "." && temp != ".." && !temp.empty())
            ret = ret + '/' + temp;
        if (ret.empty())
            ret = "/";
        return ret;
    }
};
```