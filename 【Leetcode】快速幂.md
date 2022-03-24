# 【Leetcode】快速幂



[toc]



## 50. Pow(x, n)

![](D:\Notes\Leetcode\Leetcode.assets\50-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\50-2.png)

相关视频：
[5-7 「力扣」第 50 题：快速幂](https://www.bilibili.com/video/BV1HU4y1o7cN)

我的AC代码：

```c++
class Solution {
public:
	double myPow(double x, int n) {
		if (n == 0x80000000) {
			return myPow(x, 0x80000001) * x;
		}
		else if (n < 0) {
			return myPow(1 / x, -n);;
		}
		else if (n == 0) {
			return 1.0;
		}
		else if (n%2 == 1) {
			return myPow(x, n - 1) * x;
		}
		else{
			double p = myPow(x, n / 2);
			return p * p;
		}
	}
};
```

