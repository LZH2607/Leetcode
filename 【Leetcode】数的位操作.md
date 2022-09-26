# 【Leetcode】数的位操作



[toc]



## 数的位操作

### 十进制数的位操作

取十进制整数的每一位（C++）：

```c++
vector<int> getDigits(int x) {
	vector<int> v;
	while (x > 0) {
		int d = x % 10;
		x = x / 10;
		v.push_back(d);
	}
	return v;
}
```

取十进制小数的前n位（C++）：

```c++
vector<int> getDigits(double x, int n) {
	vector<int> v;
	for (int i = 0; i < n; i++) {
		x = x - (int)x;
		x = x * 10;
		int d = x;
		v.push_back(d);
	}
	return v;
}
```



### 二进制数的位操作

取二进制整数的每一位（C++）：

```c++
vector<int> getBits(int x) {
	vector<int> v;
	while (x > 0) {
		int b = x & 1;
		x = x >> 1;
		v.push_back(b);
	}
	return v;
}
```

取二进制小数的前n位（C++）：

```c++
vector<int> getBits(double x, int n) {
	vector<int> v;
	for (int i = 0; i < n; i++) {
		x = x - (int)x;
		x = x * 2;
		int d = x;
		v.push_back(d);
	}
	return v;
}
```



### R进制数的位操作

取R进制整数的每一位（C++）：

```c++
vector<int> getDigits(int x, int r) {
	vector<int> v;
	while (x > 0) {
		int d = x % r;
		x = x / r;
		v.push_back(d);
	}
	return v;
}
```

取R进制小数的前n位（C++）：

```c++
vector<int> getDigits(double x, int r, int n) {
	vector<int> v;
	for (int i = 0; i < n; i++) {
		x = x - (int)x;
		x = x * r;
		int d = x;
		v.push_back(d);
	}
	return v;
}
```



## 7. 整数反转

![](D:\Notes\Leetcode\Leetcode.assets\7-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\7-2.png)

相关视频：
[7. 整数反转 - 力扣（LeetCode）C语言菜鸟通俗讲解](https://www.bilibili.com/video/BV1UL411T7yK)

我的AC代码（C++）：

```c++
class Solution {
public:
	int reverse(int x) {
		int minInt = 0x80000000;
		int maxInt = 0x7fffffff;
		int y = 0;
		while (x != 0) {
			int d = x % 10;
			x = x / 10;
			if (y > maxInt / 10 - d / 10 || y < minInt / 10 - d / 10) {
				return 0;
			}
			y = y * 10 + d;
		}
		return y;
	}
};
```

我的AC代码（Java）：

```java
class Solution {
    public int reverse(int x) {
        int y = 0;
        while (x != 0) {
            int d = x % 10;
            x = x / 10;
            if (((y * 10 + d) - d) / 10 != y) {
                return 0;
            }
            y = y * 10 + d;
        }
        return y;
    }
}
```



## 9. 回文数

![](D:\Notes\Leetcode\Leetcode.assets\9-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\9-2.png)

我的AC代码（C++，解法1）：

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

我的AC代码（C++，解法2）：

```c++
class Solution {
public:
	bool isPalindrome(int x) {
		if (x < 0) {
			return false;
		}
		long t = x;
		long y = 0;
		while (x > 0) {
			int d = x % 10;
			x = x / 10;
			y = y * 10 + d;
		}
		if (y != t) {
			return false;
		}
		return true;
	}
};
```

我的AC代码（Java）：

```java
class Solution {
    public boolean isPalindrome(int x) {
        if (x < 0) {
            return false;
        }
        int t = x;
        int y = 0;
        while (x > 0) {
            int d = x % 10;
            x = x / 10;
            y = y * 10 + d;
        }
        if (y != t) {
            return false;
        }
        return true;
    }
}
```



## 393. UTF-8 编码验证

![](D:\Notes\Leetcode\Leetcode.assets\393-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\393-2.png)

我的AC代码（Java）：

```java
class Solution {
    public boolean validUtf8(int[] data) {
        int num = 0;
        int cnt = 0;
        for (int i = 0; i < data.length; i++) {
            if (cnt == 0) {
                num = getNum(data, i);
                cnt = num;
            }
            if (num != 0 && (num == cnt || (data[i] & 192) == 128)) {
                cnt--;
                continue;
            }
            return false;
        }
        return true;
    }

    private int getNum(int[] data, int i) {
        if ((data[i] & 128) == 0 && i <= data.length - 1) {
            return 1;
        } else if ((data[i] & 224) == 192 && i <= data.length - 2) {
            return 2;
        } else if ((data[i] & 240) == 224 && i <= data.length - 3) {
            return 3;
        } else if ((data[i] & 248) == 240 && i <= data.length - 4) {
            return 4;
        }
        return 0;
    }
}
```

