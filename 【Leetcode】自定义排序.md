# 【Leetcode】自定义排序



[toc]



## 1366. 通过投票对团队排名

![](D:\Notes\Leetcode\Leetcode.assets\1366.png)

我的AC代码（Java）：

```java
class Solution {
    public String rankTeams(String[] votes) {
        int n = votes[0].length();
        HashMap<String, Team> m = new HashMap<>();
        ArrayList<Team> l;
        String res = "";
        for (String vote : votes) {
            for (int i = 0; i < vote.length(); i++) {
                String s = vote.substring(i, i + 1);
                if (m.containsKey(s)) {
                    m.get(s).cnt[i]++;
                } else {
                    Team t = new Team(s);
                    t.cnt[i]++;
                    m.put(s, t);
                }
            }
        }
        l = new ArrayList<Team>(m.values());
        Collections.sort(l, new Comparator<Team>() {
            public int compare(Team t1, Team t2) {
                for (int i = 0; i < n; i++) {
                    if (t1.cnt[i] != t2.cnt[i]) {
                        return t2.cnt[i] - t1.cnt[i];
                    }
                }
                return (int) t1.s.charAt(0) - (int) t2.s.charAt(0);
            }
        });
        for (Team t : l) {
            res += t.s;
        }
        return res;
    }
}

class Team {
    String s;
    int[] cnt = new int[26];

    Team(String s) {
        this.s = s;
    }
}
```



## 1387. 将整数按权重排序

![](D:\Notes\Leetcode\Leetcode.assets\1387.png)

我的AC代码（Java）：

```java
class Solution {
    public int getKth(int lo, int hi, int k) {
        ArrayList<Int> l = new ArrayList<>();
        for (int i = lo; i <= hi; i++) {
            l.add(new Int(i, calWeight(i)));
        }
        Collections.sort(l, new Comparator<Int>() {
            public int compare(Int i1, Int i2) {
                if (i1.weight != i2.weight) {
                    return i1.weight - i2.weight;
                } else {
                    return i1.val - i2.val;
                }
            }
        });
        return l.get(k - 1).val;
    }

    private int calWeight(int num) {
        int cnt = 0;
        while (num != 1) {
            cnt++;
            if (num % 2 == 0) {
                num /= 2;
            } else {
                num *= 3;
                num++;
            }
        }
        return cnt;
    }
}

class Int {
    int val;
    int weight;

    Int(int val, int weight) {
        this.val = val;
        this.weight = weight;
    }
}
```



## 1451. 重新排列句子中的单词

![](D:\Notes\Leetcode\Leetcode.assets\1451.png)

我的AC代码（Java，解法1）：

```java
class Solution {
    public String arrangeWords(String text) {
        String[] strs = text.toLowerCase().split(" ");
        ArrayList<Str> l = new ArrayList<>();
        String res = "";
        for (int i = 0; i < strs.length; i++) {
            l.add(new Str(strs[i], i));
        }
        Collections.sort(l, new Comparator<Str>() {
            public int compare(Str s1, Str s2) {
                if (s1.str.length() != s2.str.length()) {
                    return s1.str.length() - s2.str.length();
                } else {
                    return s1.idx - s2.idx;
                }
            }
        });
        for (Str s : l) {
            res += s.str + " ";
        }
        return res.substring(0, 1).toUpperCase() + res.substring(1, res.length() - 1);
    }
}

class Str {
    String str;
    int idx;

    Str(String str, int idx) {
        this.str = str;
        this.idx = idx;
    }
}
```

我的AC代码（Java，解法2）：

```java
class Solution {
    public String arrangeWords(String text) {
        String[] strs = text.toLowerCase().split(" ");
        String res = "";
        Arrays.sort(strs, new Comparator<String>() {
            public int compare(String str1, String str2) {
                return str1.length() - str2.length();
            }
        });
        for (String str : strs) {
            res += str + " ";
        }
        return res.substring(0, 1).toUpperCase() + res.substring(1, res.length() - 1);
    }
}
```

