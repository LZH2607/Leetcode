# 【Leetcode】规则



[toc]



## 36. 有效的数独

![](D:\Notes\Leetcode\Leetcode.assets\36-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\36-2.png)
![](D:\Notes\Leetcode\Leetcode.assets\36-3.png)

我的AC代码：

```c++
class Solution {
public:
	bool isValidSudoku(vector<vector<char>>& board) {
		for (int i = 0; i < 9; i++) {
			if (!checkRow(board, i)) {
				return false;
			}
		}
		for (int j = 0; j < 9; j++) {
			if (!checkCol(board, j)) {
				return false;
			}
		}
		for (int i = 0; i < 9; i += 3) {
			for (int j = 0; j < 9; j += 3) {
				if (!checkSubBox(board, i, j)) {
					return false;
				}
			}
		}
		return true;
	}
	bool checkRow(vector<vector<char>>& board, int i) {
		int cnt[10] = { false };
		for (int j = 0; j < 9; j++) {
			if (board[i][j] != '.') {
				int idx = (int)board[i][j] - (int)'0';
				if (cnt[idx]) {
					return false;
				}
				else {
					cnt[idx] = true;
				}
			}
		}
		return true;
	}
	bool checkCol(vector<vector<char>>& board, int j) {
		int cnt[10] = { false };
		for (int i = 0; i < 9; i++) {
			if (board[i][j] != '.') {
				int idx = (int)board[i][j] - (int)'0';
				if (cnt[idx]) {
					return false;
				}
				else {
					cnt[idx] = true;
				}
			}
		}
		return true;
	}
	bool checkSubBox(vector<vector<char>>& board, int r, int c) {
		int cnt[10] = { false };
		for (int i = r; i < r + 3; i++) {
			for (int j = c; j < c + 3; j++) {
				if (board[i][j] != '.') {
					int idx = (int)board[i][j] - (int)'0';
					if (cnt[idx]) {
						return false;
					}
					else {
						cnt[idx] = true;
					}
				}
			}
		}
		return true;
	}
};
```

