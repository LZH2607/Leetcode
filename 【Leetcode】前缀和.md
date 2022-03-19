# 【Leetcode】前缀和



[toc]



|           题目            |                             链接                             | 难度 |
| :-----------------------: | :----------------------------------------------------------: | :--: |
|          前缀和           | [https://leetcode-cn.com/tag/prefix-sum/problemset/](https://leetcode-cn.com/tag/prefix-sum/problemset/) | 题库 |
| 238. 除自身以外数组的乘积 | [https://leetcode-cn.com/problems/product-of-array-except-self/](https://leetcode-cn.com/problems/product-of-array-except-self/) | 中等 |
|                           |                                                              |      |



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

