# 【Leetcode】矩阵



[toc]



## 48. 旋转图像

![](D:\Notes\Leetcode\Leetcode.assets\48-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\48-2.png)

相关视频：
[五分钟力扣 Leetcode 第48题 旋转图像 清晰易懂 例子阐述 时间67%](https://www.bilibili.com/video/BV1Ct4y1C7zf)

我的AC代码：

```c++
class Solution {
public:
	void rotate(vector<vector<int>>& matrix) {
		int n = matrix.size();
		for (int i = 0; i < n / 2; i++) {
			int len = n - i * 2 - 1;
			for (int j = i; j < i + len; j++) {
				int temp = matrix[i][j];
				matrix[i][j] = matrix[n - j - 1][i];
				matrix[n - j - 1][i] = matrix[n - i - 1][n - j - 1];
				matrix[n - i - 1][n - j - 1] = matrix[j][n - i - 1];
				matrix[j][n - i - 1] = temp;
			}
		}
	}
};
```

