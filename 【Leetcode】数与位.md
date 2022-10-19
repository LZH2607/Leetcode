# 【Leetcode】数与位



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

![](D:\Notes\Leetcode\Leetcode.assets\7.png)

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



## 8. 字符串转换整数 (atoi)

![](D:\Notes\Leetcode\Leetcode.assets\8.png)

我的AC代码（Java）：

```java
class Solution {
    public int myAtoi(String s) {
        s = s.trim();
        long sign = 1;
        long num = 0;
        long res = sign * num;
        if (s.length() > 0 && s.charAt(0) == '-') {
            sign = -1;
            s = s.substring(1);
        } else if (s.length() > 0 && s.charAt(0) == '+') {
            s = s.substring(1);
        }

        char[] arr = s.toCharArray();
        for (char c : arr) {
            if (c > '9' || c < '0') {
                break;
            }
            res = sign * (num * 10 + (c - '0'));
            if (res > Integer.MAX_VALUE) {
                num = Integer.MAX_VALUE;
                break;
            } else if (res < Integer.MIN_VALUE) {
                num = Integer.MIN_VALUE;
                break;
            }
            num = num * 10 + (c - '0');
        }
        res = sign * num;
        return (int) res;
    }
}
```



## 9. 回文数

![](D:\Notes\Leetcode\Leetcode.assets\9.png)

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



## 29. 两数相除

![](D:\Notes\Leetcode\Leetcode.assets\29.png)

相关视频：
[五分钟力扣 Leetcode 第29题 两数相除 Python入门算法刷题 极简解法 13行代码 67% 位移操作](https://www.bilibili.com/video/BV1SQ4y1K7z5/)

我的AC代码（Java）:

```java
class Solution {
    public int divide(int dividend, int divisor) {
        if (divisor == 0) {
            return Integer.MAX_VALUE;
        }
        boolean neg = false;
        boolean flag = false;
        if ((dividend > 0 && divisor < 0) || (dividend < 0 && divisor > 0)) {
            neg = true;
        }
        if (dividend == Integer.MIN_VALUE) {
            if (divisor == -1) {
                return Integer.MAX_VALUE;
            } else if (divisor == Integer.MIN_VALUE) {
                return 1;
            } else {
                flag = true;
                dividend++;
            }
        } else if (divisor == Integer.MIN_VALUE) {  // dividend != Integer.MIN_VALUE
            return 0;
        }
        if (dividend < 0) {
            dividend = get2sComplement(dividend);
        }
        if (divisor < 0) {
            divisor = get2sComplement(divisor);
        }
        int res = 0;
        while (dividend >= divisor) {
            int i = getI(dividend, divisor);
            dividend -= divisor << i;
            res += 1 << i;
        }
        if (flag && (dividend + 1) >= divisor) {
            res++;
        }
        if (neg) {
            res = get2sComplement(res);
        }
        return res;
    }

    int get2sComplement(int i) {
        return ~i + 1;
    }

    int getI(int dividend, int divisor) {
        int i = 0;
        while ((dividend >> 1) > divisor) {
            i++;
            dividend >>= 1;
        }
        return i;
    }
}
```



## 43. 字符串相乘

![](D:\Notes\Leetcode\Leetcode.assets\43.png)

我的AC代码（Java）：

```java
class Solution {
    String[] mul;

    public String multiply(String num1, String num2) {
        if (compare(num1, num2) == -1) {
            String temp = num1;
            num1 = num2;
            num2 = temp;
        }
        init(num1);
        int len = num2.length();
        num2 = new StringBuffer(num2).reverse().toString();
        String res = "";
        String zeros = "";
        for (int i = 0; i < len; i++) {
            res = add(mul[Integer.parseInt(num2.substring(i, i + 1))] + zeros, res);
            zeros += "0";
        }
        return res;
    }

    void init(String num) {
        mul = new String[10];
        mul[0] = "0";
        for (int i = 1; i < 10; i++) {
            mul[i] = add(mul[i - 1], num);
        }
    }

    int compare(String num1, String num2) {
        int len1 = num1.length();
        int len2 = num2.length();
        if (len1 > len2) {
            return 1;
        } else if (len1 < len2) {
            return -1;
        }
        // len1 == len2
        for (int i = 0; i < len1; i++) {
            int d1 = Integer.parseInt(num1.substring(i, i + 1));
            int d2 = Integer.parseInt(num2.substring(i, i + 1));
            if (d1 > d2) {
                return 1;
            } else if (d1 < d2) {
                return -1;
            }
            // d1 == d2
        }
        return 0;
    }

    String add(String num1, String num2) {
        num1 = new StringBuffer(num1).reverse().toString();
        num2 = new StringBuffer(num2).reverse().toString();
        int len1 = num1.length();
        int len2 = num2.length();
        Deque<Integer> seq = new ArrayDeque<>();
        int c = 0;
        int i = 0;
        while (i < len1 && i < len2) {
            int s = Integer.parseInt(num1.substring(i, i + 1)) + Integer.parseInt(num2.substring(i, i + 1)) + c;
            int d = s % 10;
            c = s / 10;
            seq.push(d);
            i++;
        }
        while (i < len1) {
            int s = Integer.parseInt(num1.substring(i, i + 1)) + c;
            int d = s % 10;
            c = s / 10;
            seq.push(d);
            i++;
        }
        while (i < len2) {
            int s = Integer.parseInt(num2.substring(i, i + 1)) + c;
            int d = s % 10;
            c = s / 10;
            seq.push(d);
            i++;
        }
        if (c > 0) {
            seq.push(c);
        }
        String res = "";
        while (!seq.isEmpty()) {
            res += seq.pollFirst();
        }
        return res;
    }
}
```



## 66. 加一

![](D:\Notes\Leetcode\Leetcode.assets\66.png)

我的AC代码（Java）：

```java
class Solution {
    public int[] plusOne(int[] digits) {
        Deque<Integer> seq = new ArrayDeque<>();
        int c = 1;
        for (int i = digits.length - 1; i >= 0; i--) {
            int s = digits[i] + c;
            int d = s % 10;
            c = s / 10;
            seq.push(d);
        }
        if (c > 0) {
            seq.push(c);
        }
        int[] ans = new int[seq.size()];
        for (int i = 0; i < ans.length; i++) {
            ans[i] = seq.pollFirst();
        }
        return ans;
    }
}
```



## 67. 二进制求和

![](D:\Notes\Leetcode\Leetcode.assets\67.png)

我的AC代码（Java）：

```java
class Solution {
    public String addBinary(String a, String b) {
        a = new StringBuffer(a).reverse().toString();
        b = new StringBuffer(b).reverse().toString();
        int len1 = a.length();
        int len2 = b.length();
        Deque<Integer> seq = new ArrayDeque<>();
        int i = 0;
        int c = 0;
        while (i < len1 && i < len2) {
            int s = Integer.parseInt(a.substring(i, i + 1)) + Integer.parseInt(b.substring(i, i + 1)) + c;
            int d = s % 2;
            c = s / 2;
            seq.push(d);
            i++;
        }
        while (i < len1) {
            int s = Integer.parseInt(a.substring(i, i + 1)) + c;
            int d = s % 2;
            c = s / 2;
            seq.push(d);
            i++;
        }
        while (i < len2) {
            int s = Integer.parseInt(b.substring(i, i + 1)) + c;
            int d = s % 2;
            c = s / 2;
            seq.push(d);
            i++;
        }
        if (c > 0) {
            seq.push(c);
        }
        String res = "";
        while (!seq.isEmpty()) {
            res += seq.pollFirst();
        }
        return res;
    }
}
```



## 393. UTF-8 编码验证

![](D:\Notes\Leetcode\Leetcode.assets\393.png)

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

