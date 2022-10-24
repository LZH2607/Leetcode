# 【Leetcode】矩阵



[toc]



## 6. Z 字形变换

![](D:\Notes\Leetcode\Leetcode.assets\6.png)

我的AC代码（Java）：

```java
class Solution {
    public String convert(String s, int numRows) {
        if (numRows == 1) {
            return s;
        }
        int numCols = s.length();
        char[][] mat = new char[numRows][numCols];
        char[] arr = s.toCharArray();
        boolean down = true;
        int i = 0;
        int j = 0;
        for (char c : arr) {
            mat[i][j] = c;
            if (down && i < numRows - 1) {
                i++;
            } else if (down && i == numRows - 1) {
                down = false;
                i--;
                j++;
            } else if (!down & i > 0) {
                i--;
                j++;
            } else {  // !down & i == 0
                down = true;
                i++;
            }
        }
        String res = "";
        for (i = 0; i < mat.length; i++) {
            for (j = 0; j < mat[i].length; j++) {
                if (mat[i][j] != 0) {
                    res = res + mat[i][j];
                }
            }
        }
        return res;
    }
}
```



## 48. 旋转图像

![](D:\Notes\Leetcode\Leetcode.assets\48.png)

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

![](D:\Notes\Leetcode\Leetcode.assets\54.png)

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

![](D:\Notes\Leetcode\Leetcode.assets\59.png)

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

![](D:\Notes\Leetcode\Leetcode.assets\73.png)

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



## 531. 孤独像素 I

![](D:\Notes\Leetcode\Leetcode.assets\531.png)

我的AC代码（Java）：

```java
class Solution {
    public int findLonelyPixel(char[][] picture) {
        int m = picture.length;
        int n = picture[0].length;
        int[] cntRow = new int[m];
        int[] cntCol = new int[n];
        for (int r = 0; r < m; r++) {
            for (int c = 0; c < n; c++) {
                if (picture[r][c] == 'B') {
                    cntRow[r]++;
                    cntCol[c]++;
                }
            }
        }
        int cnt = 0;
        for (int r = 0; r < m; r++) {
            if (cntRow[r] > 1) {
                continue;
            }
            // cntRow[r] == 1
            for (int c = 0; c < n; c++) {
                if (picture[r][c] == 'W') {
                    continue;
                }
                // picture[r][c] == 'B'
                if (cntCol[c] == 1) {
                    cnt++;
                }
                break;
            }
        }
        return cnt;
    }
}
```



## 533. 孤独像素 II

![](D:\Notes\Leetcode\Leetcode.assets\533.png)

我的AC代码（Java）：

```java
class Solution {
    public int findBlackPixel(char[][] picture, int target) {
        int m = picture.length;
        int n = picture[0].length;
        int[] cntRow = new int[m];
        int[] cntCol = new int[n];
        Map<Integer, List<Integer>> map = new HashMap<>();
        for (int r = 0; r < m; r++) {
            for (int c = 0; c < n; c++) {
                if (picture[r][c] == 'B') {
                    cntRow[r]++;
                    cntCol[c]++;
                    if (!map.containsKey(c)) {
                        List<Integer> l = new ArrayList<>();
                        l.add(r);
                        map.put(c, l);
                        continue;
                    }
                    // m.containsKey(c)
                    map.get(c).add(r);
                }
            }
        }
        boolean[][] same = new boolean[m][m];
        for (int r1 = 0; r1 < m; r1++) {
            String s1 = new String(picture[r1]);
            for (int r2 = r1; r2 < m; r2++) {
                if (r1 == r2) {
                    same[r1][r2] = true;
                    continue;
                }
                String s2 = new String(picture[r2]);
                same[r1][r2] = s1.equals(s2);
                same[r2][r1] = same[r1][r2];
            }
        }
        int cnt = 0;
        for (int r = 0; r < m; r++) {
            if (cntRow[r] != target) {
                continue;
            }
            // cntRow[r] == target
            for (int c = 0; c < n; c++) {
                if (cntCol[c] != target) {
                    continue;
                }
                // cntCol[c] == target
                boolean flag = true;
                for (int i : map.get(c)) {
                    if (!same[r][i]) {
                        flag = false;
                        break;
                    }
                }
                if (flag) {
                    cnt++;
                }
            }
        }
        return cnt;
    }
}
```

