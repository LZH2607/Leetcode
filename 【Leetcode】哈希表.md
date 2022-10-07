# 【Leetcode】哈希表



[toc]



## 1. 两数之和

![](D:\Notes\Leetcode\Leetcode.assets\1-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\1-2.png)

相关视频：
[二数之和题解分析](https://www.bilibili.com/video/BV1hV411e7MW)
[二数之和代码解析](https://www.bilibili.com/video/BV1si4y1P7Eg)

我的AC代码（C++）：

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

我的AC代码（Java）：

```java
class Solution {
	public int[] twoSum(int[] nums, int target) {
		HashMap<Integer, Integer> m = new HashMap<>();
		int len = nums.length;
		int ans[] = new int[2];
		for (int i = 0; i < len; i++) {
			if (m.containsKey(target - nums[i])) {
				ans[0] = i;
				ans[1] = m.get(target - nums[i]);
				break;
			} else {
				m.put(nums[i], i);
			}
		}
		return ans;
	}
}
```



## 12. 整数转罗马数字

![](D:\Notes\Leetcode\Leetcode.assets\12-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\12-2.png)
![](D:\Notes\Leetcode\Leetcode.assets\12-3.png)

相关视频：
[你真的识数么？一起认识罗马数字](https://www.bilibili.com/video/BV19541157Pm)
[罗马数字Roman Numerals](https://www.bilibili.com/video/BV1fx411b7HX)
[五分钟力扣 Leetcode 第12题 整数转罗马数字  Python入门算法刷题 两种解法 Leetcode删除了什么功能大揭秘](https://www.bilibili.com/video/BV1ft4y1m7SK)

我的AC代码（C++）：

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

我的AC代码（Java）：

```java
class Solution {
	public String intToRoman(int num) {
		HashMap<Integer, String> m = new HashMap<>();
		m.put(0, "");
		m.put(1, "I");
		m.put(2, "II");
		m.put(3, "III");
		m.put(4, "IV");
		m.put(5, "V");
		m.put(6, "VI");
		m.put(7, "VII");
		m.put(8, "VIII");
		m.put(9, "IX");

		m.put(10, "X");
		m.put(20, "XX");
		m.put(30, "XXX");
		m.put(40, "XL");
		m.put(50, "L");
		m.put(60, "LX");
		m.put(70, "LXX");
		m.put(80, "LXXX");
		m.put(90, "XC");

		m.put(100, "C");
		m.put(200, "CC");
		m.put(300, "CCC");
		m.put(400, "CD");
		m.put(500, "D");
		m.put(600, "DC");
		m.put(700, "DCC");
		m.put(800, "DCCC");
		m.put(900, "CM");

		m.put(1000, "M");
		m.put(2000, "MM");
		m.put(3000, "MMM");

		String s = "";
		int base = 1;
		while (num > 0) {
			int res = num % 10;
			num = num / 10;
			s = m.get(res * base) + s;
			base *= 10;
		}

		return s;
	}
}
```



## 13. 罗马数字转整数

![](D:\Notes\Leetcode\Leetcode.assets\13-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\13-2.png)
![](D:\Notes\Leetcode\Leetcode.assets\13-3.png)

我的AC代码（C++）：

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

我的AC代码（Java）：

```java
class Solution {
	public int romanToInt(String s) {
		HashMap<String, Integer> m = new HashMap<>();
		m.put("I", 1);
		m.put("II", 2);
		m.put("III", 3);
		m.put("IV", 4);
		m.put("V", 5);
		m.put("VI", 6);
		m.put("VII", 7);
		m.put("VIII", 8);
		m.put("IX", 9);

		m.put("X", 10);
		m.put("XX", 20);
		m.put("XXX", 30);
		m.put("XL", 40);
		m.put("L", 50);
		m.put("LX", 60);
		m.put("LXX", 70);
		m.put("LXXX", 80);
		m.put("XC", 90);

		m.put("C", 100);
		m.put("CC", 200);
		m.put("CCC", 300);
		m.put("CD", 400);
		m.put("D", 500);
		m.put("DC", 600);
		m.put("DCC", 700);
		m.put("DCCC", 800);
		m.put("CM", 900);

		m.put("M", 1000);
		m.put("MM", 2000);
		m.put("MMM", 3000);

		int num = 0;
		while (s.length() > 0) {
			int len = s.length();
			for (int l = 4; l > 0; l--) {
				if (len < l) {
					continue;
				}
				String subs = s.substring(0, l);
				if (m.containsKey(subs)) {
					num += m.get(subs);
					s = s.substring(l);
					break;
				}
			}
		}
		return num;
	}
}
```



## 49. 字母异位词分组

![](D:\Notes\Leetcode\Leetcode.assets\49-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\49-2.png)

我的AC代码（C++）：

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

我的AC代码（Java）：

```java
class Solution {
	public List<List<String>> groupAnagrams(String[] strs) {
		HashMap<String, List<String>> m = new HashMap<>();
		for (int i = 0; i < strs.length; i++) {
			char cs[] = strs[i].toCharArray();
			Arrays.sort(cs);
			String k = new String(cs);
			if (m.containsKey(k)) {
				m.get(k).add(strs[i]);
			} else {
				List<String> l = new ArrayList<>();
				l.add(strs[i]);
				m.put(k, l);
			}
		}
		List<List<String>> ll = new ArrayList<>();
		for (List<String> l : m.values()) {
			ll.add(l);
		}
		return ll;
	}
}
```



## 128. 最长连续序列

![](D:\Notes\Leetcode\Leetcode.assets\128.png)

相关视频：
[最长连续序列](https://www.bilibili.com/video/BV1M7411A79B)

我的AC代码（C++）：

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

我的AC代码（Java）：

```java
class Solution {
    public int longestConsecutive(int[] nums) {
        HashSet<Integer> s = new HashSet<>();
        HashMap<Integer, Integer> lm = new HashMap<>();
        HashMap<Integer, Integer> rm = new HashMap<>();
        int maxLen = 0;
        for (int num : nums) {
            if (s.contains(num)) {
                continue;
            }
            s.add(num);
            boolean l_flag = rm.containsKey(num + 1);
            boolean r_flag = lm.containsKey(num - 1);
            if (!l_flag && !r_flag) {
                lm.put(num, num);
                rm.put(num, num);
                if (maxLen == 0) {
                    maxLen = 1;
                }
            } else if (l_flag && !r_flag) {
                int r_num = rm.get(num + 1);
                rm.remove(num + 1);
                rm.put(num, r_num);
                lm.put(r_num, num);
                int len = r_num - num + 1;
                if (len > maxLen) {
                    maxLen = len;
                }
            } else if (!l_flag && r_flag) {
                int l_num = lm.get(num - 1);
                lm.remove(num - 1);
                lm.put(num, l_num);
                rm.put(l_num, num);
                int len = num - l_num + 1;
                if (len > maxLen) {
                    maxLen = len;
                }
            } else { // l_flag && r_flag
                int l_num = lm.get(num - 1);
                int r_num = rm.get(num + 1);
                lm.remove(num - 1);
                rm.remove(num + 1);
                lm.put(r_num, l_num);
                rm.put(l_num, r_num);
                int len = r_num - l_num + 1;
                if (len > maxLen) {
                    maxLen = len;
                }
            }
        }
        return maxLen;
    }
}
```



## 187. 重复的DNA序列

相关视频：
[Leetcode刷题187. 重复的DNA序列 Repeated DNA Sequences](https://www.bilibili.com/video/BV1PQ4y1P7se)

![](D:\Notes\Leetcode\Leetcode.assets\187.png)

我的AC代码（C++）：

```c++
class Solution {
public:
	vector<string> findRepeatedDnaSequences(string s) {
		vector<string> res;
		unordered_map<string, int> m;
		int sLen = s.size();
		int subLen = 10;
		for (int i = 0; i < sLen - subLen + 1; i++) {
			string sub = s.substr(i, subLen);
			unordered_map<string, int>::iterator it = m.find(sub);
			if (it == m.end()) {
				m[sub] = 1;
			}
			else {
				(*it).second++;
			}
		}
		for (unordered_map<string, int>::iterator it = m.begin(); it != m.end(); it++) {
			if ((*it).second > 1) {
				res.push_back((*it).first);
			}
		}
		return res;
	}
};
```

我的AC代码（Java）：

```java
class Solution {
    public List<String> findRepeatedDnaSequences(String s) {
        Map<String, Integer> m = new HashMap<>();
        List<String> l = new ArrayList<>();
        for (int i = 0; i <= s.length() - 10; i++) {
            String subStr = s.substring(i, i + 10);
            if (!m.containsKey(subStr)) {
                m.put(subStr, 1);
            } else {
                m.put(subStr, m.get(subStr) + 1);
            }
        }
        for (String subStr : m.keySet()) {
            if (m.get(subStr) > 1) {
                l.add(subStr);
            }
        }
        return l;
    }
}
```



## 217. 存在重复元素

![](D:\Notes\Leetcode\Leetcode.assets\217.png)

我的AC代码（Java）：

```java
class Solution {
    public boolean containsDuplicate(int[] nums) {
        Set<Integer> s = new HashSet<>();
        for (int num : nums) {
            if (s.contains(num)) {
                return true;
            }
            s.add(num);
        }
        return false;
    }
}
```



## 219. 存在重复元素 II

![](D:\Notes\Leetcode\Leetcode.assets\219-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\219-2.png)

我的AC代码（C++）：

```c++
class Solution {
public:
	bool containsNearbyDuplicate(vector<int>& nums, int k) {
		int len = nums.size();
		unordered_map<int, vector<int>> m;
		for (int i = 0; i < len; i++) {
			int num = nums[i];
			if (m.find(num) == m.end()) {
				vector<int> v;
				v.push_back(i);
				m[num] = v;
			}
			else {
				m[num].push_back(i);
			}
		}
		for (unordered_map<int, vector<int>>::iterator it = m.begin(); it != m.end(); it++) {
			vector<int> v = (*it).second;
			sort(v.begin(), v.end());
			int n = v.size();
			for (int i = 0; i < n - 1; i++) {
				if (abs(v[i] - v[i + 1]) <= k) {
					return true;
				}
			}
		}
		return false;
	}
};
```

我的AC代码（Java）：

```java
class Solution {
    public boolean containsNearbyDuplicate(int[] nums, int k) {
        Map<Integer, List<Integer>> m = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            int num = nums[i];
            if (!m.containsKey(num)) {
                List<Integer> l = new ArrayList<>();
                l.add(i);
                m.put(num, l);
            } else {
                m.get(num).add(i);
            }
        }
        for (int num : m.keySet()) {
            List<Integer> l = m.get(num);
            Collections.sort(l);
            for (int i = 0; i < l.size() - 1; i++) {
                if (Math.abs(l.get(i) - l.get(i + 1)) <= k) {
                    return true;
                }
            }
        }
        return false;
    }
}
```

