# 【Leetcode】二叉搜索树



[toc]



树节点的代码（C++）：

```c++
struct TreeNode {
	int val;
	TreeNode* left;
	TreeNode* right;
	TreeNode() : val(0), left(nullptr), right(nullptr) {}
	TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
	TreeNode(int x, TreeNode* left, TreeNode* right) : val(x), left(left), right(right) {}
};
```



## 95. 不同的二叉搜索树 II

![](D:\Notes\Leetcode\Leetcode.assets\95-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\95-2.png)

相关视频：
[【LeetCode 每日一题】95. 不同的二叉搜索树 II | 手写图解版思路 + 代码讲解](https://www.bilibili.com/video/BV1LZ4y127cJ)

我的AC代码（C++）：

```c++
class Solution {
public:
	vector<TreeNode*> dp[10][10];
	vector<TreeNode*> generateTrees(int n) {
		init();
		return generate(1, n);
	}
	void init() {
		for (int i = 1; i < 10; i++) {
			for (int j = 1; j < 10; j++) {
				if (i == j) {
					TreeNode* tp = new TreeNode(i);
					dp[i][j] = { tp };
				}
				else {
					dp[i][j] = { nullptr };
				}
			}
		}
	}
	vector<TreeNode*> generate(int l, int r) {
		if (l < r && dp[l][r][0] == nullptr) {
			dp[l][r].pop_back();
			vector<TreeNode*> left = generate(l, r - 1);
			vector<TreeNode*> right = generate(l + 1, r);
			for (vector<TreeNode*>::iterator lit = left.begin(); lit != left.end(); lit++) {
				TreeNode* tp = new TreeNode(r, *lit, nullptr);
				dp[l][r].push_back(tp);
			}
			for (vector<TreeNode*>::iterator rit = right.begin(); rit != right.end(); rit++) {
				TreeNode* tp = new TreeNode(l, nullptr, *rit);
				dp[l][r].push_back(tp);
			}
			for (int i = l + 1; i <= r - 1; i++) {
				left = generate(l, i - 1);
				right = generate(i + 1, r);
				for (vector<TreeNode*>::iterator lit = left.begin(); lit != left.end(); lit++) {
					for (vector<TreeNode*>::iterator rit = right.begin(); rit != right.end(); rit++) {
						TreeNode* tp = new TreeNode(i, *lit, *rit);
						dp[l][r].push_back(tp);
					}
				}
			}
		}
		return dp[l][r];
	}
};
```



## 96. 不同的二叉搜索树

![](D:\Notes\Leetcode\Leetcode.assets\96-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\96-2.png)

我的AC代码（C++）：

```c++
class Solution {
public:
	int dp[20][20];
	int numTrees(int n) {
		init();
		return num(1, n);
	}
	void init() {
		for (int i = 1; i < 20; i++) {
			for (int j = 1; j < 20; j++) {
				if (i == j) {
					dp[i][i] = 1;
				}
				else {
					dp[i][j] = 0;
				}
			}
		}
	}
	int num(int l, int r) {
		if (l < r && dp[l][r] == 0) {
			dp[l][r] += num(l + 1, r);
			dp[l][r] += num(l, r - 1);
			for (int i = l + 1; i <= r - 1; i++) {
				dp[l][r] += num(l, i - 1) * num(i + 1, r);
			}
		}
		return dp[l][r];
	}
};
```



## 98. 验证二叉搜索树

![](D:\Notes\Leetcode\Leetcode.assets\98-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\98-2.png)
![](D:\Notes\Leetcode\Leetcode.assets\98-3.png)

相关视频：
[应届必备大厂面试题详解：验证二叉搜索树](https://www.bilibili.com/video/BV1c3411W7uX)

我的AC代码（C++）：

```c++
class Solution {
public:
	vector<int> order;
	bool isValidBST(TreeNode* root) {
		if (root == nullptr) {
			return true;
		}
		bool bl = isValidBST(root->left);
		if (order.size() != 0 && order.back() >= root->val) {
			return false;
		}
		else {
			order.push_back(root->val);
		}
		bool br = isValidBST(root->right);
		return bl && br;
	}
};
```

