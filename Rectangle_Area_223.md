# 223. Rectangle Area 解题记录
## 题目描述：
Find the total area covered by two rectilinear rectangles in a 2D plane.  
Each rectangle is defined by its bottom left corner and top right corner as shown in the figure.  
  
**Example:**  
```
Input: -3, 0, 3, 4, 0, -1, 9, 2
Output: 45
```
## 解题思路：
先算两个矩形面积之和，再减去重合部分。
## 代码：
```
class Solution {
public:
    int computeArea(int A, int B, int C, int D, int E, int F, int G, int H) {
        int area = (D - B) * (C - A) + (G - E) * (H - F); // 总面积
		int left = max(A, E);
		int down = max(B, F);
		int right = min(G, C);
		int up = min(D, H);
		if (up <= down || right <= left) {
                                //分离的情况
			return area;
		}
		area = area - (right - left) * (up - down);
		return area;

    }
};
```