# 【Leetcode】规则



[toc]



## 36. 有效的数独

![](D:\Notes\Leetcode\Leetcode.assets\36-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\36-2.png)
![](D:\Notes\Leetcode\Leetcode.assets\36-3.png)

我的AC代码：

```java
class Solution {
	public boolean isValidSudoku(char[][] board) {
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

	private boolean checkRow(char[][] board, int i) {
		boolean cnt[] = new boolean[10];
		for (int j = 0; j < 9; j++) {
			if (board[i][j] != '.') {
				int idx = (int) board[i][j] - (int) '0';
				if (cnt[idx]) {
					return false;
				} else {
					cnt[idx] = true;
				}
			}
		}
		return true;
	}

	private boolean checkCol(char[][] board, int j) {
		boolean cnt[] = new boolean[10];
		for (int i = 0; i < 9; i++) {
			if (board[i][j] != '.') {
				int idx = (int) board[i][j] - (int) '0';
				if (cnt[idx]) {
					return false;
				} else {
					cnt[idx] = true;
				}
			}
		}
		return true;
	}

	private boolean checkSubBox(char[][] board, int r, int c) {
		boolean cnt[] = new boolean[10];
		for (int i = r; i < r + 3; i++) {
			for (int j = c; j < c + 3; j++) {
				if (board[i][j] != '.') {
					int idx = (int) board[i][j] - (int) '0';
					if (cnt[idx]) {
						return false;
					} else {
						cnt[idx] = true;
					}
				}
			}
		}
		return true;
	}
}
```

