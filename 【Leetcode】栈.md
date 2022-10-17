# 【Leetcode】栈



[toc]



## 20. 有效的括号（C++、Java）

![](D:\Notes\Leetcode\Leetcode.assets\20.png)

我的AC代码（C++）：

```c++
class Solution {
public:
	bool isValid(string s) {
		int len = s.size();
		bool flag = true;
		vector<char> v;
		for (int i = 0; i < len && flag; i++) {
			char c = s[i];
			switch (c)
			{
			case ')':
				if (v.size() == 0) {
					flag = false;
				}
				else if (v.back() != '(') {
					flag = false;
				}
				else {
					v.pop_back();
				}
				break;
			case ']':
				if (v.size() == 0) {
					flag = false;
				}
				else if (v.back() != '[') {
					flag = false;
				}
				else {
					v.pop_back();
				}
				break;
			case '}':
				if (v.size() == 0) {
					flag = false;
				}
				else if (v.back() != '{') {
					flag = false;
				}
				else {
					v.pop_back();
				}
				break;
			default:
				v.push_back(c);
			}
		}
		if (len == 1 || v.size() > 0) {
			flag = false;
		}
		return flag;
	}
};
```

我的AC代码（Java）：

```java
class Solution {
    public boolean isValid(String s) {
        int len = s.length();
        Deque<Character> d = new ArrayDeque<>();
        char c = s.charAt(0);
        if (!isLeft(c)) {
            return false;
        }
        d.push(c);
        for (int i = 1; i < len; i++) {
            c = s.charAt(i);
            if (isLeft(c)) {
                d.push(c);
                continue;
            }
            if (d.isEmpty()) {
                return false;
            }
            char ch = d.pop();
            if (!isPair(ch, c)) {
                return false;
            }
        }
        if (!d.isEmpty()) {
            return false;
        }
        return true;
    }

    boolean isLeft(char c) {
        switch (c) {
            case '(':
            case '[':
            case '{':
                return true;
            default:
        }
        return false;
    }

    boolean isPair(char c1, char c2) {
        return c1 == '(' && c2 == ')' || c1 == '[' && c2 == ']' || c1 == '{' && c2 == '}';
    }
}
```



## 56. 合并区间（Java）

![](D:\Notes\Leetcode\Leetcode.assets\56.png)

我的AC代码（Java）：

```java
class Solution {
    Deque<int[]> d;
    Deque<int[]> temp;

    public int[][] merge(int[][] intervals) {
        d = new ArrayDeque<>();
        temp = new ArrayDeque<>();
        for (int[] interval : intervals) {
            while (!d.isEmpty() && d.getFirst()[0] > interval[0]) {
                temp.push(d.pop());
            }
            push(interval);
            while (!temp.isEmpty()) {
                push(temp.pop());
            }
        }
        int[][] res = new int[d.size()][];
        int i = 0;
        while (!d.isEmpty()) {
            res[i] = d.pop();
            i++;
        }
        return res;
    }

    void push(int[] interval) {
        if (d.isEmpty()) {
            d.push(interval);
            return;
        }
        if (d.getFirst()[1] >= interval[0]) {
            d.getFirst()[1] = Math.max(d.getFirst()[1], interval[1]);
        } else {
            d.push(interval);
        }
    }
}
```



## 71. 简化路径（C++、Java）

![](D:\Notes\Leetcode\Leetcode.assets\71.png)

相关视频：
[【LeetCode 每日一题】71. 简化路径 | 手写图解版思路 + 代码讲解](https://www.bilibili.com/video/BV1qF411s7Jy)

我的AC代码（C++）：

```c++
class Solution {
public:
	string simplifyPath(string path) {
		vector<string> v;
		string res;
		path = path.substr(1);
		if (path.back() != '/') {
			path = path + "/";
		}
		int id = path.find('/');
		while (id != -1) {
			string file = path.substr(0, id);
			path = path.substr(id + 1);
			if (file == "..") {
				if (v.size() != 0) {
					v.pop_back();
				}
			}
			else if (file != "" && file != ".") {
				v.push_back(file);
			}
			id = path.find('/');
		}
		for (vector<string>::iterator it = v.begin(); it != v.end(); it++) {
			res = res + "/" + *it;
		}
		if (v.size() == 0) {
			res = "/";
		}
		return res;
	}
};
```

我的AC代码（Java）：

```java
class Solution {
    public String simplifyPath(String path) {
        String res = "";
        Deque<String> d = new ArrayDeque<>();
        String[] dirs = path.split("/+");

        for (String dir : dirs) {
            if (dir.equals("..")) {
                if (d.isEmpty()) {
                    continue;
                }
                d.pop();
            } else if (!dir.equals("") && !dir.equals(".")) {
                d.push(dir);
            }
        }

        Iterator<String> it = d.descendingIterator();
        while (it.hasNext()) {
            res = res + "/" + it.next();
        }

        return res.equals("") ? "/" : res;
    }
}
```



## 150. 逆波兰表达式求值（C++、Java）

![](D:\Notes\Leetcode\Leetcode.assets\150.png)

我的AC代码（C++）：

```c++
class Solution {
public:
	int evalRPN(vector<string>& tokens) {
		vector<int> v;
		int len = tokens.size();
		for (int i = 0; i < len; i++) {
			if (tokens[i] == "+") {
				int b = v.back();
				v.pop_back();

				int a = v.back();
				v.pop_back();

				int c = a + b;
				v.push_back(c);

			}
			else if (tokens[i] == "-") {
				int b = v.back();
				v.pop_back();

				int a = v.back();
				v.pop_back();

				int c = a - b;
				v.push_back(c);
			}
			else if (tokens[i] == "*") {
				int b = v.back();
				v.pop_back();

				int a = v.back();
				v.pop_back();

				int c = a * b;
				v.push_back(c);
			}
			else if (tokens[i] == "/") {
				int b = v.back();
				v.pop_back();

				int a = v.back();
				v.pop_back();

				int c = a / b;
				v.push_back(c);
			}
			else {
				int x = atoi(tokens[i].c_str());
				v.push_back(x);
			}
		}
		return v[0];
	}
};
```

我的AC代码（Java）：

```java
class Solution {
    public int evalRPN(String[] tokens) {
        Deque<Integer> d = new ArrayDeque<>();

        for (String token : tokens) {
            if (!token.equals("+") && !token.equals("-") && !token.equals("*") && !token.equals("/")) {
                d.push(Integer.parseInt(token));
                continue;
            }
            int i1 = d.pop();
            int i2 = d.pop();
            int i3;
            if (token.equals("+")) {
                i3 = i2 + i1;
            } else if (token.equals("-")) {
                i3 = i2 - i1;
            } else if (token.equals("*")) {
                i3 = i2 * i1;
            } else {  // token.equals("/")
                i3 = i2 / i1;
            }
            d.push(i3);
        }

        return d.pop();
    }
}
```



## 224. 基本计算器（Java）

![](D:\Notes\Leetcode\Leetcode.assets\224.png)

我的AC代码（Java）：

```java
class Solution {
    public int calculate(String s) {
        if (s.charAt(0) == '-') {
            s = "0" + s;
        }
        String[] strs = s.replace(" ", "").replace("(-", "(0-").split("(?<=\\+|-|\\*|/|\\(|\\))|(?=\\+|-|\\*|/|\\(|\\))");
        Deque<String> seq = new ArrayDeque<>();
        Deque<String> sign = new ArrayDeque<>();
        for (String str : strs) {
            if (!str.equals("+") && !str.equals("-") && !str.equals("*") && !str.equals("/") && !str.equals("(") && !str.equals(")")) {
                seq.push(str);
                continue;
            }
            if (str.equals("(")) {
                sign.push(str);
                continue;
            }
            if (str.equals(")")) {
                while (!sign.getFirst().equals("(")) {
                    seq.push(sign.pop());
                }
                sign.pop();
                continue;
            }
            while (!sign.isEmpty()) {
                if (!prior(str, sign.getFirst())) {
                    seq.push(sign.pop());
                    continue;
                }
                break;
            }
            sign.push(str);
        }
        while (!sign.isEmpty()) {
            seq.push(sign.pop());
        }
        Deque<Integer> d = new ArrayDeque<>();
        while (!seq.isEmpty()) {
            String str = seq.pollLast();
            if (!str.equals("+") && !str.equals("-") && !str.equals("*") && !str.equals("/")) {
                d.push(Integer.parseInt(str));
                continue;
            }
            int i1 = d.pop();
            int i2 = d.pop();
            int i3;
            if (str.equals("+")) {
                i3 = i2 + i1;
            } else if (str.equals("-")) {
                i3 = i2 - i1;
            } else if (str.equals("*")) {
                i3 = i2 * i1;
            } else {  // str.equals("/")
                i3 = i2 / i1;
            }
            d.push(i3);
        }
        return d.pop();
    }

    boolean prior(String s1, String s2) {
        int w1 = weight(s1);
        int w2 = weight(s2);
        return w1 > w2;
    }

    int weight(String s) {
        if (s.equals("(")) {
            return -1;
        } else if (s.equals("+") || s.equals("-")) {
            return 0;
        }
        return 1;  // s.equals("*") || s.equals("/")
    }
}
```



## 227. 基本计算器 II（Java）

![](D:\Notes\Leetcode\Leetcode.assets\227.png)

我的AC代码（Java）：

```java
class Solution {
    public int calculate(String s) {
        String[] strs = s.replace(" ", "").split("(?<=\\+|-|\\*|/)|(?=\\+|-|\\*|/)");
        Deque<String> seq = new ArrayDeque<>();
        Deque<String> sign = new ArrayDeque<>();
        for (String str : strs) {
            if (!str.equals("+") && !str.equals("-") && !str.equals("*") && !str.equals("/")) {
                seq.push(str);
                continue;
            }
            while (!sign.isEmpty()) {
                if (!prior(str, sign.getFirst())) {
                    seq.push(sign.pop());
                    continue;
                }
                break;
            }
            sign.push(str);
        }
        while (!sign.isEmpty()) {
            seq.push(sign.pop());
        }
        Deque<Integer> d = new ArrayDeque<>();
        while (!seq.isEmpty()) {
            String str = seq.pollLast();
            if (!str.equals("+") && !str.equals("-") && !str.equals("*") && !str.equals("/")) {
                d.push(Integer.parseInt(str));
                continue;
            }
            int i1 = d.pop();
            int i2 = d.pop();
            int i3;
            if (str.equals("+")) {
                i3 = i2 + i1;
            } else if (str.equals("-")) {
                i3 = i2 - i1;
            } else if (str.equals("*")) {
                i3 = i2 * i1;
            } else {  // str.equals("/")
                i3 = i2 / i1;
            }
            d.push(i3);
        }
        return d.pop();
    }

    boolean prior(String s1, String s2) {
        int w1 = weight(s1);
        int w2 = weight(s2);
        return w1 > w2;
    }

    int weight(String s) {
        if (s.equals("+") || s.equals("-")) {
            return 0;
        }
        return 1;  // s.equals("*") || s.equals("/")
    }
}
```



## 636. 函数的独占时间（Java）

![](D:\Notes\Leetcode\Leetcode.assets\636.png)

我的AC代码（Java）：

```java
class Solution {
    int[] total;

    public int[] exclusiveTime(int n, List<String> logs) {
        total = new int[n];
        Deque<Function> d = new ArrayDeque<>();
        for (String log : logs) {
            String[] strs = log.split(":");
            int id = Integer.parseInt(strs[0]);
            String status = strs[1];
            int timestamp = Integer.parseInt(strs[2]);
            if (status.equals("start")) {
                if (!d.isEmpty()) {
                    d.getFirst().sum += timestamp - d.getFirst().timestamp;
                    d.getFirst().timestamp = timestamp;
                }
                d.push(new Function(id, timestamp, 0));
            } else {  // status.equals("end")
                Function f = d.pop();
                f.sum += timestamp - f.timestamp + 1;
                total[f.id] += f.sum;
                if (!d.isEmpty()) {
                    d.getFirst().timestamp = timestamp + 1;
                }
            }
        }
        return total;
    }
}

class Function {
    int id;
    int timestamp;
    int sum;

    public Function(int id, int timestamp, int sum) {
        this.id = id;
        this.timestamp = timestamp;
        this.sum = sum;
    }
}
```



## 735. 行星碰撞（C++、Java）

![](D:\Notes\Leetcode\Leetcode.assets\735.png)

相关题解：
[行星碰撞](https://leetcode-cn.com/problems/asteroid-collision/solution/xing-xing-peng-zhuang-by-leetcode/)

我的AC代码（C++，解法1）：

```c++
class Solution {
public:
	vector<int> asteroidCollision(vector<int>& asteroids) {
		vector<int> res;
		vector<int> v;
		for (vector<int>::iterator it = asteroids.begin(); it != asteroids.end(); it++) {
			int a = *it;
			if (a > 0) {
				v.push_back(a);
			}
			else {
				while (v.size() != 0 && v.back() < abs(a)) {
					v.pop_back();
				}
				if (v.size() != 0 && v.back() == abs(a)) {
					v.pop_back();
					continue;
				}
				if (v.size() == 0) {
					res.push_back(a);
				}
			}
		}
		for (vector<int>::iterator it = v.begin(); it != v.end(); it++) {
			res.push_back(*it);
		}
		return res;
	}
};
```

我的AC代码（C++，解法2）：

```c++
class Solution {
public:
	vector<int> asteroidCollision(vector<int>& asteroids) {
		vector<int> v1;
		vector<int> v2 = asteroids;
		int len1 = v1.size();
		int len2 = v2.size();
		while (len1 != len2 && len2 > 1) {
			v1 = v2;
			v2 = {};
			len1 = v1.size();
			// first
			if (v1[0] < 0) {
				v2.push_back(v1[0]);
			}
			else { // v1[0] > 0
				if (v1[1] > 0 || v1[1] < 0 && abs(v1[0]) > abs(v1[1])) {
					v2.push_back(v1[0]);
				}
			}
			// middle
			for (int i = 1; i < len1 - 1; i++) {
				if (v1[i] < 0) {
					if (v1[i - 1] > 0 && abs(v1[i]) <= abs(v1[i - 1])) {
						continue;
					}

				}
				else { // v1[i] > 0
					if (v1[i + 1] < 0 && abs(v1[i]) <= abs(v1[i + 1])) {
						continue;
					}
				}
				v2.push_back(v1[i]);
			}
			// last
			if (v1[len1 - 1] > 0) {
				v2.push_back(v1[len1 - 1]);
			}
			else { // v1[len1 - 1] < 0
				if (v1[len1 - 2] < 0 || v1[len1 - 2] > 0 && abs(v1[len1 - 1]) > abs(v1[len1 - 2])) {
					v2.push_back(v1[len1 - 1]);
				}
			}
			len2 = v2.size();
		}
		return v2;
	}
};
```

我的AC代码（Java）：

```java
class Solution {
    public int[] asteroidCollision(int[] asteroids) {
        Deque<Integer> d = new ArrayDeque<>();
        for (int a : asteroids) {
            if (d.isEmpty()) {
                d.push(a);
                continue;
            }
            boolean flag = true;
            while (!d.isEmpty()) {
                int i = d.getFirst();
                if ((i > 0 && a > 0) || i < 0) {
                    break;
                } else if (i > -a) {  // i > 0 && a < 0
                    flag = false;
                    break;
                } else if (i == -a) {
                    d.pop();
                    flag = false;
                    break;
                } else {  // i < -a
                    d.pop();
                }
            }
            if (flag) {
                d.push(a);
            }
        }
        int len = d.size();
        int[] res = new int[len];
        Object[] arr = d.toArray();
        for (int i = 0; i < len; i++) {
            res[i] = (Integer) arr[len - i - 1];
        }
        return res;
    }
}
```



## 772. 基本计算器 III（Java）

![](D:\Notes\Leetcode\Leetcode.assets\772.png)

我的AC代码（Java）：

```java
class Solution {
    public int calculate(String s) {
        if (s.charAt(0) == '-') {
            s = "0" + s;
        }
        String[] strs = s.replace(" ", "").replace("(-", "(0-").split("(?<=\\+|-|\\*|/|\\(|\\))|(?=\\+|-|\\*|/|\\(|\\))");
        Deque<String> seq = new ArrayDeque<>();
        Deque<String> sign = new ArrayDeque<>();
        for (String str : strs) {
            if (!str.equals("+") && !str.equals("-") && !str.equals("*") && !str.equals("/") && !str.equals("(") && !str.equals(")")) {
                seq.push(str);
                continue;
            }
            if (str.equals("(")) {
                sign.push(str);
                continue;
            }
            if (str.equals(")")) {
                while (!sign.getFirst().equals("(")) {
                    seq.push(sign.pop());
                }
                sign.pop();
                continue;
            }
            while (!sign.isEmpty()) {
                if (!prior(str, sign.getFirst())) {
                    seq.push(sign.pop());
                    continue;
                }
                break;
            }
            sign.push(str);
        }
        while (!sign.isEmpty()) {
            seq.push(sign.pop());
        }
        Deque<Integer> d = new ArrayDeque<>();
        while (!seq.isEmpty()) {
            String str = seq.pollLast();
            if (!str.equals("+") && !str.equals("-") && !str.equals("*") && !str.equals("/")) {
                d.push(Integer.parseInt(str));
                continue;
            }
            int i1 = d.pop();
            int i2 = d.pop();
            int i3;
            if (str.equals("+")) {
                i3 = i2 + i1;
            } else if (str.equals("-")) {
                i3 = i2 - i1;
            } else if (str.equals("*")) {
                i3 = i2 * i1;
            } else {  // str.equals("/")
                i3 = i2 / i1;
            }
            d.push(i3);
        }
        return d.pop();
    }

    boolean prior(String s1, String s2) {
        int w1 = weight(s1);
        int w2 = weight(s2);
        return w1 > w2;
    }

    int weight(String s) {
        if (s.equals("(")) {
            return -1;
        } else if (s.equals("+") || s.equals("-")) {
            return 0;
        }
        return 1;  // s.equals("*") || s.equals("/")
    }
}
```

