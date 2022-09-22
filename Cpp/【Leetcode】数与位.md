# 【Leetcode】数与位



[toc]



## 7. 整数反转

![](D:\Notes\Leetcode\Leetcode.assets\7-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\7-2.png)

相关视频：
[7. 整数反转 - 力扣（LeetCode）C语言菜鸟通俗讲解](https://www.bilibili.com/video/BV1UL411T7yK)

我的AC代码：

```c++
class Solution {
public:
	int reverse(int x) {
		int maxInt = 0x7fffffff;
		int minInt = 0x80000000;
		int y = 0;
		while (x != 0) {
			int b = x % 10;
			if (y > maxInt / 10 || (y == maxInt / 10 && b > maxInt % 10)) {
				y = 0;
				break;
			}
			else if (y < minInt / 10 || (y == minInt / 10 && b < minInt % 10)) {
				y = 0;
				break;
			}
			y = y * 10 + b;
			x = x / 10;
		}
		return y;
	}
};
```



## 9. 回文数

![](D:\Notes\Leetcode\Leetcode.assets\9-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\9-2.png)

我的AC代码：

```c++
class Solution {
public:
	bool isPalindrome(int x) {
		if (x < 0) {
			return false;
		}
		vector<int> v;
		while (x != 0) {
			v.push_back(x % 10);
			x = x / 10;
		}
		int len = v.size();
		bool flag = true;
		if (len % 2 == 0) {
			for (int i = 0; i < len / 2; i++) {
				if (v[i] != v[len - 1 - i]) {
					flag = false;
					break;
				}
			}
		}
		else {
			for (int i = 0; i < len / 2; i++) {
				if (v[i] != v[len - 1 - i]) {
					flag = false;
					break;
				}
			}
		}
		return flag;
	}
};
```

