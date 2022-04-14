# 【Leetcode】哈希表



[toc]



## 1. 两数之和

![](D:\Notes\Leetcode\Leetcode.assets\1-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\1-2.png)

相关视频：
[二数之和题解分析](https://www.bilibili.com/video/BV1hV411e7MW)
[二数之和代码解析](https://www.bilibili.com/video/BV1si4y1P7Eg)

我的AC代码：

```c++
class Solution {
public:
	vector<int> twoSum(vector<int>& nums, int target) {
		unordered_map<int, int> m;
		int len = nums.size();
		vector<int> v;
		for (int i = 0; i < len; i++) {
			unordered_map<int, int>::iterator it = m.find(target - nums[i]);
			if (it == m.end()) {
				m.insert(pair<int, int>(nums[i], i));
			}
			else {
				v.push_back(it->second);
				v.push_back(i);
				break;
			}
		}
		return v;
	}
};
```



## 12. 整数转罗马数字

![](D:\Notes\Leetcode\Leetcode.assets\12-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\12-2.png)
![](D:\Notes\Leetcode\Leetcode.assets\12-3.png)

相关视频：
[你真的识数么？一起认识罗马数字](https://www.bilibili.com/video/BV19541157Pm)
[罗马数字Roman Numerals](https://www.bilibili.com/video/BV1fx411b7HX)
[五分钟力扣 Leetcode 第12题 整数转罗马数字  Python入门算法刷题 两种解法 Leetcode删除了什么功能大揭秘](https://www.bilibili.com/video/BV1ft4y1m7SK)

我的AC代码：

```c++
class Solution {
public:
	string intToRoman(int num) {
		unordered_map<int, string> m;
		m[1] = "I";
		m[2] = "II";
		m[3] = "III";
		m[4] = "IV";
		m[5] = "V";
		m[6] = "VI";
		m[7] = "VII";
		m[8] = "VIII";
		m[9] = "IX";
		
		m[10] = "X";
		m[20] = "XX";
		m[30] = "XXX";
		m[40] = "XL";
		m[50] = "L";
		m[60] = "LX";
		m[70] = "LXX";
		m[80] = "LXXX";
		m[90] = "XC";

		m[100] = "C";
		m[200] = "CC";
		m[300] = "CCC";
		m[400] = "CD";
		m[500] = "D";
		m[600] = "DC";
		m[700] = "DCC";
		m[800] = "DCCC";
		m[900] = "CM";

		m[1000] = "M";
		m[2000] = "MM";
		m[3000] = "MMM";

		string s = "";
		int base = 1;
		while (num > 0) {
			int res = num % 10;
			num = num / 10;
			s = m[res * base] + s;
			base *= 10;
		}

		return s;
	}
};
```



## 13. 罗马数字转整数

![](D:\Notes\Leetcode\Leetcode.assets\13-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\13-2.png)
![](D:\Notes\Leetcode\Leetcode.assets\13-3.png)

我的AC代码：

```c++
class Solution {
public:
	int romanToInt(string s) {
		unordered_map<string, int> m;
		m["I"] = 1;
		m["II"] = 2;
		m["III"] = 3;
		m["IV"] = 4;
		m["V"] = 5;
		m["VI"] = 6;
		m["VII"] = 7;
		m["VIII"] = 8;
		m["IX"] = 9;
		
		m["X"] = 10;
		m["XX"] = 20;
		m["XXX"] = 30;
		m["XL"] = 40;
		m["L"] = 50;
		m["LX"] = 60;
		m["LXX"] = 70;
		m["LXXX"] = 80;
		m["XC"] = 90;

		m["C"] = 100;
		m["CC"] = 200;
		m["CCC"] = 300;
		m["CD"] = 400;
		m["D"] = 500;
		m["DC"] = 600;
		m["DCC"] = 700;
		m["DCCC"] = 800;
		m["CM"] = 900;

		m["M"] = 1000;
		m["MM"] = 2000;
		m["MMM"] = 3000;

		int num = 0;
		while (s.size() > 0) {
			int len = s.size();
			for (int l = 4; l > 0; l--) {
				if (len < l) {
					continue;
				}
				string subs = s.substr(0, l);
				if (m.find(subs) != m.end()) {
					num += m[subs];
					s = s.substr(l);
					break;
				}
			}
		}
		return num;
	}
};
```



## 49. 字母异位词分组

![](D:\Notes\Leetcode\Leetcode.assets\49-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\49-2.png)

我的AC代码：

```c++
class Solution {
public:
	vector<vector<string>> groupAnagrams(vector<string>& strs) {
		vector<vector<string>> vv;
		unordered_map<string, int> m;
		int idx = 0;
		for (vector<string>::iterator it = strs.begin(); it != strs.end(); it++) {
			string s = *it;
			sort(s.begin(), s.end());
			if (m.find(s) == m.end()) {
				m[s] = idx;
				vector<string> v;
				v.push_back(*it);
				vv.push_back(v);
				idx++;
			}
			else {
				vv[m[s]].push_back(*it);
			}
		}
		return vv;
	}
};
```



## 128. 最长连续序列

![](D:\Notes\Leetcode\Leetcode.assets\128.png)

相关视频：
[最长连续序列](https://www.bilibili.com/video/BV1M7411A79B)

我的AC代码：

```c++
class Solution {
public:
	int longestConsecutive(vector<int>& nums) {
		unordered_map<int, int> m;
		int maxLen = 0;
		for (vector<int>::iterator it = nums.begin(); it != nums.end(); it++) {
			int num = *it;
			if (m.find(num) == m.end()) {
				unordered_map<int, int>::iterator left = m.find(num - 1);
				unordered_map<int, int>::iterator right = m.find(num + 1);
				int len;
				int lEnd;
				int rEnd;
				if (left == m.end() && right == m.end()) {
					len = 1;
					lEnd = num;
					rEnd = num;
				}
				else if (left != m.end() && right == m.end()) {
					len = (*left).second + 1;
					lEnd = num - (*left).second;
					rEnd = num;
				}
				else if (left == m.end() && right != m.end()) {
					len = (*right).second + 1;
					lEnd = num;
					rEnd = num + (*right).second;
				}
				else {
					len = (*left).second + (*right).second + 1;
					lEnd = num - (*left).second;
					rEnd = num + (*right).second;
					m[num] = len;
				}
				m[lEnd] = len;
				m[rEnd] = len;
				if (len > maxLen) {
					maxLen = len;
				}
			}
		}
		return maxLen;
	}
};
```

