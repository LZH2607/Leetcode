# 【Leetcode】前缀和



[toc]



|               题目               |                             链接                             | 难度 |
| :------------------------------: | :----------------------------------------------------------: | :--: |
|              前缀和              | [https://leetcode-cn.com/tag/prefix-sum/problemset/](https://leetcode-cn.com/tag/prefix-sum/problemset/) | 题库 |
|    238. 除自身以外数组的乘积     | [https://leetcode-cn.com/problems/product-of-array-except-self/](https://leetcode-cn.com/problems/product-of-array-except-self/) | 中等 |
|   303. 区域和检索 - 数组不可变   | [https://leetcode-cn.com/problems/range-sum-query-immutable/](https://leetcode-cn.com/problems/range-sum-query-immutable/) | 简单 |
| 304. 二维区域和检索 - 矩阵不可变 | [https://leetcode-cn.com/problems/range-sum-query-2d-immutable/](https://leetcode-cn.com/problems/range-sum-query-2d-immutable/) | 中等 |



## 238. 除自身以外数组的乘积

![](D:\Notes\Leetcode\Leetcode.assets\238-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\238-2.png)

相关视频：
[Leetcode 238. 除自身以外数组的乘积 前缀和](https://www.bilibili.com/video/BV1HP4y157FM)

我的AC代码：

```c++
class Solution {
public:
	vector<int> productExceptSelf(vector<int>& nums) {
		int len = nums.size();
		int* l_product = (int*)malloc(sizeof(int) * len);
		int* r_product = (int*)malloc(sizeof(int) * len);
		vector<int> res(len);
		memcpy(&res[0], l_product, sizeof(l_product));
		l_product[0] = nums[0];
		for (int i = 1; i < len; i++) {
			l_product[i] = l_product[i - 1] * nums[i];
		}
		r_product[len - 1] = nums[len - 1];
		for (int i = len - 2; i >= 0; i--) {
			r_product[i] = r_product[i + 1] * nums[i];
		}
		res[0] = r_product[1];
		res[len - 1] = l_product[len - 2];
		for (int i = 1; i < len - 1; i++) {
			res[i] = l_product[i - 1] * r_product[i + 1];
		}
		free(l_product);
		free(r_product);
		return res;
	}
};
```



## 303. 区域和检索 - 数组不可变

![](D:\Notes\Leetcode\Leetcode.assets\303-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\303-2.png)

我的AC代码：

```c++
class NumArray {
public:
	int* sum;
	int len;
	NumArray(vector<int>& nums) {
		len = nums.size();
		sum = (int*)malloc(sizeof(int) * len);
		sum[0] = nums[0];
		for (int i = 1; i < len; i++) {
			sum[i] = sum[i - 1] + nums[i];
		}
	}
	int sumRange(int left, int right) {
		if (left == 0) {
			return sum[right];
		}
		else {
			return sum[right] - sum[left - 1];
		}
	}
};
```



## 304. 二维区域和检索 - 矩阵不可变

![](D:\Notes\Leetcode\Leetcode.assets\304-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\304-2.png)

我的AC代码：

```c++
class NumMatrix {
public:
	int* sum;
	int row;
	int col;
	int convert(int i, int j) {
		// sum[i][j] = sum[i * col + j]
		return i * col + j;
	}
	NumMatrix(vector<vector<int>>& matrix) {
		row = matrix.size();
		col = (matrix[0]).size();
		sum = (int*)malloc(sizeof(int) * row * col);
		sum[0] = matrix[0][0];
		for (int i = 1; i < row; i++) {
			sum[convert(i, 0)] = sum[convert(i - 1, 0)] + matrix[i][0];
		}
		for (int j = 1; j < col; j++) {
			sum[convert(0, j)] = sum[convert(0, j - 1)] + matrix[0][j];
		}
		for (int i = 1; i < row; i++) {
			for (int j = 1; j < col; j++) {
				sum[convert(i, j)] = sum[convert(i - 1, j)] + sum[convert(i, j - 1)] - sum[convert(i - 1, j - 1)] + matrix[i][j];
			}
		}
	}
	int sumRegion(int row1, int col1, int row2, int col2) {
		if (row1 == 0) {
			if (col1 == 0) {
				return sum[convert(row2, col2)];
			}
			else {
				return sum[convert(row2, col2)] - sum[convert(row2, col1 - 1)];
			}
		}
		else if (col1 == 0) {
			return sum[convert(row2, col2)] - sum[convert(row1 - 1, col2)];
		}
		else {
			return sum[convert(row2, col2)] - sum[convert(row1 - 1, col2)] - sum[convert(row2, col1 - 1)] + sum[convert(row1 - 1, col1 - 1)];
		}
	}
};
```

