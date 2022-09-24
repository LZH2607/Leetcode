# 【Leetcode】矩阵



[toc]



## 48. 旋转图像

![](D:\Notes\Leetcode\Leetcode.assets\48-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\48-2.png)

相关视频：
[五分钟力扣 Leetcode 第48题 旋转图像 清晰易懂 例子阐述 时间67%](https://www.bilibili.com/video/BV1Ct4y1C7zf)

我的AC代码（C++）：

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



## 54. 螺旋矩阵

![](D:\Notes\Leetcode\Leetcode.assets\54-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\54-2.png)

我的AC代码（C++）：

```c++
class Solution {
public:
	bool visit[12][12];
	vector<int> order;
	int m;
	int n;
	vector<int> spiralOrder(vector<vector<int>>& matrix) {
		init(matrix);
		int i = 1;
		int j = 0;
		char dir = 'l';
		int cnt = 0;
		while (cnt < 4) {
			if (dir == 'l') {
				if (visit[i][j + 1]) {
					dir = 'd';
					cnt++;
				}
				else {
					j = j + 1;
					order.push_back(matrix[i - 1][j - 1]);
					visit[i][j] = true;
					cnt = 0;
				}
			}
			if (dir == 'd') {
				if (visit[i + 1][j]) {
					dir = 'r';
					cnt++;
				}
				else {
					i = i + 1;
					order.push_back(matrix[i - 1][j - 1]);
					visit[i][j] = true;
					cnt = 0;
				}
			}
			if (dir == 'r') {
				if (visit[i][j - 1]) {
					dir = 'u';
					cnt++;
				}
				else {
					j = j - 1;
					order.push_back(matrix[i - 1][j - 1]);
					visit[i][j] = true;
					cnt = 0;
				}
			}
			if (dir == 'u') {
				if (visit[i - 1][j]) {
					dir = 'l';
					cnt++;
				}
				else {
					i = i - 1;
					order.push_back(matrix[i - 1][j - 1]);
					visit[i][j] = true;
					cnt = 0;
				}
			}
		}
		return order;
	}
	void init(vector<vector<int>>& matrix) {
		m = matrix.size();
		n = matrix[0].size();
		for (int i = 0; i < m + 2; i++) {
			for (int j = 0; j < n + 2; j++) {
				visit[i][j] = false;
			}
		}
		for (int j = 0; j < n + 2; j++) {
			visit[0][j] = true;
			visit[m + 1][j] = true;
		}
		for (int i = 0; i < m + 2; i++) {
			visit[i][0] = true;
			visit[i][n + 1] = true;
		}
	}
};
```



## 59. 螺旋矩阵 II

![](D:\Notes\Leetcode\Leetcode.assets\59-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\59-2.png)

我的AC代码（C++）：

```c++
class Solution {
public:
	bool visit[22][22];
	vector<vector<int>> vv;
	vector<vector<int>> generateMatrix(int n) {
		init(n);
		int i = 1;
		int j = 0;
		char dir = 'l';
		int cnt = 0;
		int num = 1;
		while (cnt < 4) {
			if (dir == 'l') {
				if (visit[i][j + 1]) {
					dir = 'd';
					cnt++;
				}
				else {
					j = j + 1;
					vv[i - 1][j - 1] = num;
					visit[i][j] = true;
					num++;
					cnt = 0;
				}
			}
			if (dir == 'd') {
				if (visit[i + 1][j]) {
					dir = 'r';
					cnt++;
				}
				else {
					i = i + 1;
					vv[i - 1][j - 1] = num;
					visit[i][j] = true;
					num++;
					cnt = 0;
				}
			}
			if (dir == 'r') {
				if (visit[i][j - 1]) {
					dir = 'u';
					cnt++;
				}
				else {
					j = j - 1;
					vv[i - 1][j - 1] = num;
					visit[i][j] = true;
					num++;
					cnt = 0;
				}
			}
			if (dir == 'u') {
				if (visit[i - 1][j]) {
					dir = 'l';
					cnt++;
				}
				else {
					i = i - 1;
					vv[i - 1][j - 1] = num;
					visit[i][j] = true;
					num++;
					cnt = 0;
				}
			}
		}
		return vv;
	}
	void init(int n) {
		for (int i = 0; i < n + 2; i++) {
			for (int j = 0; j < n + 2; j++) {
				visit[i][j] = false;
			}
		}
		for (int j = 0; j < n + 2; j++) {
			visit[0][j] = true;
			visit[n + 1][j] = true;
		}
		for (int i = 0; i < n + 2; i++) {
			visit[i][0] = true;
			visit[i][n + 1] = true;
		}
		for (int i = 0; i < n; i++) {
			vector<int> v;
			for (int j = 0; j < n; j++) {
				v.push_back(0);
			}
			vv.push_back(v);
		}
	}
};
```



## 73. 矩阵置零

![](D:\Notes\Leetcode\Leetcode.assets\73-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\73-2.png)
![](D:\Notes\Leetcode\Leetcode.assets\73-3.png)

相关视频：
[【LeetCode 每日一题】73. 矩阵置零 | 手写图解版思路 + 代码讲解](https://www.bilibili.com/video/BV1jL411w7ar)

我的AC代码（C++）：

```c++
class Solution {
public:
	void setZeroes(vector<vector<int>>& matrix) {
		int m = matrix.size();
		int n = matrix[0].size();
		bool row0 = false;
		bool col0 = false;
		for (int j = 0; j < n; j++) {
			if (matrix[0][j] == 0) {
				row0 = true;
				break;
			}
		}
		for (int i = 0; i < m; i++) {
			if (matrix[i][0] == 0) {
				col0 = true;
				break;
			}
		}
		for (int i = 1; i < m; i++) {
			for (int j = 1; j < n; j++) {
				if (matrix[i][j] == 0) {
					matrix[0][j] = 0;
					matrix[i][0] = 0;
				}
			}
		}
		for (int i = 1; i < m; i++) {
			if (matrix[i][0] == 0) {
				for (int j = 0; j < n; j++) {
					matrix[i][j] = 0;
				}
			}
		}
		for (int j = 1; j < n; j++) {
			if (matrix[0][j] == 0) {
				for (int i = 0; i < m; i++) {
					matrix[i][j] = 0;
				}
			}
		}
		if (row0) {
			for (int j = 0; j < n; j++) {
				matrix[0][j] = 0;
			}
		}
		if (col0) {
			for (int i = 0; i < m; i++) {
				matrix[i][0] = 0;
			}
		}
	}
};
```

