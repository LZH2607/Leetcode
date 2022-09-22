# 【Leetcode】二叉树



[toc]



```c++
// Definition for a binary tree node.
struct TreeNode {
	int val;
	TreeNode* left;
	TreeNode* right;
	TreeNode() : val(0), left(nullptr), right(nullptr) {}
	TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
	TreeNode(int x, TreeNode* left, TreeNode* right) : val(x), left(left), right(right) {}
};
```



## 94. 二叉树的中序遍历

![](D:\Notes\Leetcode\Leetcode.assets\94-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\94-2.png)

相关视频：
[数据结构-浙江大学](https://www.bilibili.com/video/BV1JW411i731)

我的AC代码（递归算法）：

```c++
class Solution {
public:
	vector<int> res;
	vector<int> inorderTraversal(TreeNode* root) {
		traverse(root);
		return res;
	}
	void traverse(TreeNode* root) {
		if (root == nullptr) {
			return;
		}
		traverse(root->left);
		res.push_back(root->val);
		traverse(root->right);
	}
};
```

我的AC代码（迭代算法）：

```c++
class Solution {
public:
	vector<int> res;
	stack<TreeNode*> s;
	vector<int> inorderTraversal(TreeNode* root) {
		TreeNode* tp = root;
		while (tp != nullptr || s.size() != 0) {
			while (tp != nullptr) {
				s.push(tp);
				tp = tp->left;
			}
			if (s.size() != 0) {
				tp = s.top();
				s.pop();
				res.push_back(tp->val);
				tp = tp->right;
			}
		}
		return res;
	}
};
```



## 100. 相同的树

![](D:\Notes\Leetcode\Leetcode.assets\100-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\100-2.png)
![](D:\Notes\Leetcode\Leetcode.assets\100-3.png)

相关视频：
[LeetCode 100. 相同的树](https://www.bilibili.com/video/BV19m4y1976i)

我的AC代码（递归算法）：

```c++
class Solution {
public:
	bool isSameTree(TreeNode* p, TreeNode* q) {
		if (p == nullptr && q == nullptr) {
			return true;
		}
		else if (p == nullptr && q != nullptr) {
			return false;
		}
		else if (p != nullptr && q == nullptr) {
			return false;
		}
		else if (p->val != q->val) {
			return false;
		}
		else { // p->val == q->val
			return isSameTree(p->left, q->left) && isSameTree(p->right, q->right);
		}
	}
};
```

我的AC代码（迭代算法）：

```c++
class Solution {
public:
	bool isSameTree(TreeNode* p, TreeNode* q) {
		TreeNode* tp = p;
		TreeNode* tq = q;
		stack<TreeNode*> sp;
		stack<TreeNode*> sq;

		while (tp != nullptr && tq != nullptr || sp.size() != 0 && sq.size() != 0) {
			while (tp != nullptr && tq != nullptr) {
				if (tp->val != tq->val) {
					return false;
				}
				sp.push(tp);
				sq.push(tq);
				tp = tp->left;
				tq = tq->left;
			}
			if (tp == nullptr && tq != nullptr || tp != nullptr && tq == nullptr) {
				return false;
			}
			if (sp.size() != 0 && sq.size() != 0) {
				tp = sp.top();
				tq = sq.top();
				sp.pop();
				sq.pop();
				tp = tp->right;
				tq = tq->right;
			}
		}

		if (tp == nullptr && tq == nullptr) {
			return true;
		}
		else {
			return false;
		}
	}
};
```



## 101. 对称二叉树

![](D:\Notes\Leetcode\Leetcode.assets\101-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\101-2.png)
![](D:\Notes\Leetcode\Leetcode.assets\101-3.png)

我的AC代码（解法1，递归算法）：

```c++
class Solution {
public:
	vector<int> order1;
	vector<int> order2;
	int Null = 0xffffffff;
	bool isSymmetric(TreeNode* root) {
		traverse1(root);
		traverse2(root);
		int len = order1.size();
		for (int i = 0; i < len; i++) {
			if (order1[i] != order2[i]) {
				return false;
			}
		}
		return true;
	}
	void traverse1(TreeNode* root) {
		order1.push_back(root->val);
		if (root->left != nullptr) {
			traverse1(root->left);
		}
		else {
			order1.push_back(Null);
		}
		if (root->right != nullptr) {
			traverse1(root->right);
		}
		else {
			order1.push_back(Null);
		}
	}
	void traverse2(TreeNode* root) {
		order2.push_back(root->val);
		if (root->right != nullptr) {
			traverse2(root->right);
		}
		else {
			order2.push_back(Null);
		}
		if (root->left != nullptr) {
			traverse2(root->left);
		}
		else {
			order2.push_back(Null);
		}
	}
};
```

我的AC代码（解法1，迭代算法）：

```c++
class Solution {
public:
	vector<int> order1;
	vector<int> order2;
	int Null = 0xffffffff;
	bool isSymmetric(TreeNode* root) {
		traverse1(root);
		traverse2(root);
		int len = order1.size();
		for (int i = 0; i < len; i++) {
			if (order1[i] != order2[i]) {
				return false;
			}
		}
		return true;
	}
	void traverse1(TreeNode* root) {
		stack<TreeNode*> s;
		TreeNode* tp = root;
		while (tp != nullptr || s.size() != 0) {
			while (tp != nullptr) {
				order1.push_back(tp->val);
				s.push(tp);
				tp = tp->left;
			}
			order1.push_back(Null);
			if (s.size() != 0) {
				tp = s.top();
				s.pop();
				tp = tp->right;
			}
		}
	}
	void traverse2(TreeNode* root) {
		stack<TreeNode*> s;
		TreeNode* tp = root;
		while (tp != nullptr || s.size() != 0) {
			while (tp != nullptr) {
				order2.push_back(tp->val);
				s.push(tp);
				tp = tp->right;
			}
			order2.push_back(Null);
			if (s.size() != 0) {
				tp = s.top();
				s.pop();
				tp = tp->left;
			}
		}
	}
};
```

我的AC代码（解法2，递归算法）：

```c++
class Solution {
public:
	bool isSymmetric(TreeNode* root) {
		if (root == nullptr) {
			return true;
		}
		else {
			return isSymmetricTree(root->left, root->right);
		}
	}
	bool isSymmetricTree(TreeNode* p, TreeNode* q) {
		if (p == nullptr && q == nullptr) {
			return true;
		}
		else if (p == nullptr && q != nullptr) {
			return false;
		}
		else if (p != nullptr && q == nullptr) {
			return false;
		}
		else if (p->val != q->val) {
			return false;
		}
		else { // p->val == q->val
			return isSymmetricTree(p->left, q->right) && isSymmetricTree(p->right, q->left);
		}
	}
};
```

我的AC代码（解法2，迭代算法）：

```c++
class Solution {
public:
	bool isSymmetric(TreeNode* root) {
		if (root == nullptr) {
			return true;
		}
		else {
			return isSymmetricTree(root->left, root->right);
		}
	}
	bool isSymmetricTree(TreeNode* p, TreeNode* q) {
		TreeNode* tp = p;
		TreeNode* tq = q;
		stack<TreeNode*> sp;
		stack<TreeNode*> sq;

		while (tp != nullptr && tq != nullptr || sp.size() != 0 && sq.size() != 0) {
			while (tp != nullptr && tq != nullptr) {
				if (tp->val != tq->val) {
					return false;
				}
				sp.push(tp);
				sq.push(tq);
				tp = tp->left;
				tq = tq->right;
			}
			if (tp == nullptr && tq != nullptr || tp != nullptr && tq == nullptr) {
				return false;
			}
			if (sp.size() != 0 && sq.size() != 0) {
				tp = sp.top();
				tq = sq.top();
				sp.pop();
				sq.pop();
				tp = tp->right;
				tq = tq->left;
			}
		}

		if (tp == nullptr && tq == nullptr) {
			return true;
		}
		else {
			return false;
		}
	}
};
```



## 102. 二叉树的层序遍历

![](D:\Notes\Leetcode\Leetcode.assets\102-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\102-2.png)

我的AC代码：

```

```



## 105. 从前序与中序遍历序列构造二叉树

![](D:\Notes\Leetcode\Leetcode.assets\105-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\105-2.png)

我的AC代码：

```c++
class Solution {
public:
	TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
		int len = preorder.size();
		return build(preorder, 0, len - 1, inorder, 0, len - 1);
	}
	TreeNode* build(vector<int>& preorder, int pl, int pr, vector<int>& inorder, int il, int ir) {
		if (pl > pr || il > ir) {
			return nullptr;
		}

		int root = preorder[pl];
		int rooti; // root在inorder中的下标
		for (int i = il; i <= ir; i++) {
			if (inorder[i] == root) {
				rooti = i;
				break;
			}
		}
		int lLen = rooti - il;
		int rLen = ir - rooti;

		int lpl, lpr; // 左子树在preorder中的范围
		int lil, lir; // 左子树在inorder中的范围
		int rpl, rpr; // 右子树在preorder中的范围
		int ril, rir; // 右子树在inorder中的范围
		lpl = pl + 1;			lpr = lpl + lLen - 1;
		lil = il;				lir = lil + lLen - 1;
		rpl = pl + lLen + 1;	rpr = rpl + rLen - 1;
		ril = il + lLen + 1;	rir = ril + rLen - 1;

		TreeNode* tp = new TreeNode;
		tp->val = root;
		tp->right = build(preorder, rpl, rpr, inorder, ril, rir);
		tp->left = build(preorder, lpl, lpr, inorder, lil, lir);
		return tp;
	}
};
```



## 106. 从中序与后序遍历序列构造二叉树

![](D:\Notes\Leetcode\Leetcode.assets\106-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\106-2.png)

我的AC代码：

```c++
class Solution {
public:
	TreeNode* buildTree(vector<int>& inorder, vector<int>& postorder) {
		int len = inorder.size();
		return build(inorder, 0, len - 1, postorder, 0, len - 1);
	}
	TreeNode* build(vector<int>& inorder, int il, int ir, vector<int>& postorder, int pl, int pr) {
		if (il > ir || pl > pr) {
			return nullptr;
		}

		int root = postorder[pr];
		int rooti; // root在inorder中的下标
		for (int i = il; i <= ir; i++) {
			if (inorder[i] == root) {
				rooti = i;
				break;
			}
		}
		int lLen = rooti - il;
		int rLen = ir - rooti;

		int lil, lir; // 左子树在inorder中的范围
		int lpl, lpr; // 左子树在postorder中的范围
		int ril, rir; // 右子树在inorder中的范围
		int rpl, rpr; // 右子树在postorder中的范围
		lil = il;				lir = lil + lLen - 1;
		lpl = pl;				lpr = lpl + lLen - 1;
		ril = il + lLen + 1;	rir = ril + rLen - 1;
		rpl = pl + lLen;		rpr = rpl + rLen - 1;

		TreeNode* tp = new TreeNode;
		tp->val = root;
		tp->left = build(inorder, lil, lir, postorder, lpl, lpr);
		tp->right = build(inorder, ril, rir, postorder, rpl, rpr);
		return tp;
	}
};
```



## 144. 二叉树的前序遍历

![](D:\Notes\Leetcode\Leetcode.assets\144-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\144-2.png)
![](D:\Notes\Leetcode\Leetcode.assets\144-3.png)

我的AC代码（递归方法）：

```c++
class Solution {
public:
	vector<int> res;
	vector<int> preorderTraversal(TreeNode* root) {
		traverse(root);
		return res;
	}
	void traverse(TreeNode* root) {
		if (root == nullptr) {
			return;
		}
		res.push_back(root->val);
		traverse(root->left);
		traverse(root->right);
	}
};
```

我的AC代码（迭代算法）：

```c++
class Solution {
public:
	vector<int> res;
	stack<TreeNode*> s;
	vector<int> preorderTraversal(TreeNode* root) {
		TreeNode* tp = root;
		while (tp != nullptr || s.size() != 0) {
			while (tp != nullptr) {
				res.push_back(tp->val);
				s.push(tp);
				tp = tp->left;
			}
			if (s.size() != 0) {
				tp = s.top();
				s.pop();
				tp = tp->right;
			}
		}
		return res;
	}
};
```




## 145. 二叉树的后序遍历

![](D:\Notes\Leetcode\Leetcode.assets\145-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\145-2.png)

我的AC代码（递归算法）：

```c++
class Solution {
public:
	vector<int> res;
	vector<int> postorderTraversal(TreeNode* root) {
		traverse(root);
		return res;
	}
	void traverse(TreeNode* root) {
		if (root == nullptr) {
			return;
		}
		traverse(root->left);
		traverse(root->right);
		res.push_back(root->val);
	}
};
```

我的AC代码（迭代算法）：

```c++
class Solution {
public:
	vector<int> res;
	stack<pair<TreeNode*, bool>> s;
	vector<int> postorderTraversal(TreeNode* root) {
		TreeNode* tp = root;
		while (tp != nullptr || s.size() != 0) {
			while (tp != nullptr) {
				s.push(pair<TreeNode*, bool>(tp, true));
				tp = tp->left;
			}
			if (s.size() != 0) {
				if (s.top().second) {
					tp = s.top().first;
					s.top().second = false;
					tp = tp->right;
				}
				else {
					res.push_back(s.top().first->val);
					s.pop();
				}
			}
		}
		return res;
	}
};
```

