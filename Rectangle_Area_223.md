# 223. Rectangle Area �����¼
## ��Ŀ������
Find the total area covered by two rectilinear rectangles in a 2D plane.  
Each rectangle is defined by its bottom left corner and top right corner as shown in the figure.  
  
**Example:**  
```
Input: -3, 0, 3, 4, 0, -1, 9, 2
Output: 45
```
## ����˼·��
���������������֮�ͣ��ټ�ȥ�غϲ��֡�
## ���룺
```
class Solution {
public:
    int computeArea(int A, int B, int C, int D, int E, int F, int G, int H) {
        int area = (D - B) * (C - A) + (G - E) * (H - F); // �����
		int left = max(A, E);
		int down = max(B, F);
		int right = min(G, C);
		int up = min(D, H);
		if (up <= down || right <= left) {
                                //��������
			return area;
		}
		area = area - (right - left) * (up - down);
		return area;

    }
};
```