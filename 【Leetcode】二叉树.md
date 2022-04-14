# 【Leetcode】二叉树



[toc]



## 105. 从前序与中序遍历序列构造二叉树

![](D:\Notes\Leetcode\Leetcode.assets\105-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\105-2.png)

我的AC代码：

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

class Solution {
public:
	TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
		int len = preorder.size();
		return build(preorder, 0, len - 1, inorder, 0, len - 1);
	}
	TreeNode* build(vector<int>& preorder, int pl, int pr, vector<int>& inorder, int il, int ir) {
		if (pl > pr || il > ir) {
			return NULL;
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
// Definition for a binary tree node.
struct TreeNode {
	int val;
	TreeNode* left;
	TreeNode* right;
	TreeNode() : val(0), left(nullptr), right(nullptr) {}
	TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
	TreeNode(int x, TreeNode* left, TreeNode* right) : val(x), left(left), right(right) {}
};

class Solution {
public:
	TreeNode* buildTree(vector<int>& inorder, vector<int>& postorder) {
		int len = inorder.size();
		return build(inorder, 0, len - 1, postorder, 0, len - 1);
	}
	TreeNode* build(vector<int>& inorder, int il, int ir, vector<int>& postorder, int pl, int pr) {
		if (il > ir || pl > pr) {
			return NULL;
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

