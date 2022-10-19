# 【Leetcode】回溯算法



[toc]



## 回溯算法

相关视频：
[带你学透回溯算法（理论篇）| 回溯法精讲！](https://www.bilibili.com/video/BV1cy4y167mM)

代码模板：

```java
void backtrack(参数) {
    if (终止条件) {
        保存结果;
        return;
    }
    for (新参数) {
        处理(参数);
        backtrack(新参数);
        撤销处理(参数);
    }
}
```

```java
void backtrack(参数) {
    if (终止条件) {
        保存结果;
        return;
    }
    for (新参数) {
        栈.push(参数);
        backtrack(新参数);
        栈.pop();
    }
}
```



## 17.电话号码的字母组合

![](D:\Notes\Leetcode\Leetcode.assets\17.png)

```java
class Solution {
    List<String> l;
    Map<Character, List<String>> m;
    char[] digits;
    int len;
    Deque<String> d;

    public List<String> letterCombinations(String digits) {
        init(digits);
        if (len > 0) {
            backtrack(0);
        }
        return l;
    }

    void init(String digits) {
        l = new ArrayList<>();
        m = new HashMap<>();
        m.put('2', Arrays.asList("a", "b", "c"));
        m.put('3', Arrays.asList("d", "e", "f"));
        m.put('4', Arrays.asList("g", "h", "i"));
        m.put('5', Arrays.asList("j", "k", "l"));
        m.put('6', Arrays.asList("m", "n", "o"));
        m.put('7', Arrays.asList("p", "q", "r", "s"));
        m.put('8', Arrays.asList("t", "u", "v"));
        m.put('9', Arrays.asList("w", "x", "y", "z"));
        this.digits = digits.toCharArray();
        len = digits.length();
        d = new ArrayDeque<>();
    }

    void backtrack(int i) {
        if (i == len) {
            String s = "";
            Iterator<String> it = d.descendingIterator();
            while (it.hasNext()) {
                s += it.next();
            }
            l.add(s);
            return;
        }
        for (String s : m.get(digits[i])) {
            d.push(s);
            backtrack(i + 1);
            d.pop();
        }
    }
}
```



## 22.括号生成

![](D:\Notes\Leetcode\Leetcode.assets\22.png)

相关视频：
[Leetcode 22 括号生成 【递归+剪枝， 也可以回溯】](https://www.bilibili.com/video/BV1x5411j7KN)

我的AC代码（Java）：

```java
class Solution {
    Deque<String> d;
    int l_cnt;
    int r_cnt;
    int n;
    List<String> l;

    public List<String> generateParenthesis(int n) {
        d = new ArrayDeque<>();
        l_cnt = 0;
        r_cnt = 0;
        this.n = n;
        l = new ArrayList<>();
        backtrack();
        return l;
    }

    void backtrack() {
        if (l_cnt == n && r_cnt == n) {
            String s = "";
            Iterator<String> it = d.descendingIterator();
            while (it.hasNext()) {
                s += it.next();
            }
            l.add(s);
            return;
        }
        if (l_cnt == n && r_cnt < n) {
            chooseRight();
        } else if (l_cnt == r_cnt) {  // l_cnt < n
            chooseLeft();
        } else {  // l_cnt > r_cnt
            chooseLeft();
            chooseRight();
        }
    }

    void chooseLeft() {
        d.push("(");
        l_cnt++;
        backtrack();
        d.pop();
        l_cnt--;
    }

    void chooseRight() {
        d.push(")");
        r_cnt++;
        backtrack();
        d.pop();
        r_cnt--;
    }
}
```



## 37. 解数独

![](D:\Notes\Leetcode\Leetcode.assets\37.png)

相关视频：
[【算法演示】回溯法求解数独，leetcode37题](https://www.bilibili.com/video/BV16U4y1E72g)

我的AC代码（Java）：

```java
class Solution {
    char[][] board;
    boolean[][] visitRow;
    boolean[][] visitCol;
    boolean[][] visitBox;

    public void solveSudoku(char[][] board) {
        init(board);
        backtrack(0, 0);
    }

    void init(char[][] board) {
        this.board = board;
        visitRow = new boolean[9][9];
        visitCol = new boolean[9][9];
        visitBox = new boolean[9][9];
        for (int r = 0; r < board.length; r++) {
            for (int c = 0; c < board[r].length; c++) {
                if (board[r][c] == '.') {
                    continue;
                }
                int i = (int) board[r][c] - (int) '1';
                int b = r / 3 + c / 3 * 3;
                visitRow[r][i] = true;
                visitCol[c][i] = true;
                visitBox[b][i] = true;
            }
        }
    }

    boolean backtrack(int r, int c) {
        if (r == 9) {
            return true;
        }
        if (board[r][c] != '.') {
            return backtrack(r + (c + 1) / 9, (c + 1) % 9);
        }
        int b = r / 3 + c / 3 * 3;
        for (int i = 0; i < 9; i++) {
            char ch = (char) (i + (int) '1');
            if (visitRow[r][i] || visitCol[c][i] || visitBox[b][i]) {
                continue;
            }
            board[r][c] = ch;
            visitRow[r][i] = true;
            visitCol[c][i] = true;
            visitBox[b][i] = true;
            if (backtrack(r + (c + 1) / 9, (c + 1) % 9)) {
                return true;
            }
            // !flag
            board[r][c] = '.';
            visitRow[r][i] = false;
            visitCol[c][i] = false;
            visitBox[b][i] = false;
        }
        return false;
    }
}
```



## 39. 组合总和

![](D:\Notes\Leetcode\Leetcode.assets\39.png)

相关视频：
[带你学透回溯算法-组合总和（对应「leetcode」力扣题目：39.组合总和）| 回溯法精讲！](https://www.bilibili.com/video/BV1KT4y1M7HJ)

我的AC代码（Java）：

```java
class Solution {
    int[] nums;
    int sum;
    int target;
    Deque<Integer> d;
    Set<List<Integer>> sl;

    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        nums = candidates;
        Arrays.sort(nums);
        this.target = target;
        d = new ArrayDeque<>();
        sl = new HashSet<>();
        backtrack();
        return new ArrayList<>(sl);
    }

    void backtrack() {
        if (sum == target) {
            List<Integer> l = Arrays.asList(d.toArray(new Integer[d.size()]));
            l.sort(Comparator.naturalOrder());
            sl.add(l);
            return;
        }
        // sum < target
        for (int num : nums) {
            if (sum + num > target) {
                return;
            }
            d.push(num);
            sum += num;
            backtrack();
            d.pop();
            sum -= num;
        }
    }
}
```



## 40. 组合总和 II

![](D:\Notes\Leetcode\Leetcode.assets\40.png)

相关视频：
[「力扣40组和总和②」](https://www.bilibili.com/video/BV1iS4y1J7hn/)

我的AC代码（Java）：

```java
class Solution {
    int[] nums;
    int target;
    int sum;
    int len;
    Deque<Integer> d;
    Set<List<Integer>> sl;

    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        nums = candidates;
        Arrays.sort(nums);
        this.target = target;
        sum = 0;
        len = nums.length;
        d = new ArrayDeque<>();
        sl = new HashSet<>();
        backtrack(0);
        return new ArrayList<>(sl);
    }

    void backtrack(int idx) {
        if (sum == target) {
            List<Integer> l = new ArrayList<>(d);
            l.sort(Comparator.naturalOrder());
            sl.add(l);
            return;
        }
        // sum < target
        for (int i = idx; i < len; i++) {
            if (i > idx && nums[i] == nums[idx]) {
                continue;
            }
            if (sum + nums[i] > target) {
                break;
            }
            sum += nums[i];
            d.push(nums[i]);
            backtrack(i + 1);
            sum -= nums[i];
            d.pop();
        }
    }
}
```



## 46. 全排列

![](D:\Notes\Leetcode\Leetcode.assets\46.png)

相关视频：
[Leetcode力扣46 手画图解版｜全排列 Permutation](https://www.bilibili.com/video/BV1up4y1s7yB/)

我的AC代码（Java）：

```java
class Solution {
    int len;
    boolean[] visit;
    int[] nums;
    Deque<Integer> d;
    List<List<Integer>> ll;

    public List<List<Integer>> permute(int[] nums) {
        len = nums.length;
        visit = new boolean[len];
        this.nums = nums;
        ll = new ArrayList<>();
        d = new ArrayDeque<>();
        backtrack();
        return ll;
    }

    void backtrack() {
        if (d.size() == len) {
            List<Integer> l = new ArrayList<>(d);
            ll.add(l);
            return;
        }
        for (int i = 0; i < len; i++) {
            if (!visit[i]) {
                d.push(nums[i]);
                visit[i] = true;
                backtrack();
                d.pop();
                visit[i] = false;
            }
        }
    }
}
```



## 47. 全排列 II

![](D:\Notes\Leetcode\Leetcode.assets\47.png)

我的AC代码（Java）：

```java
class Solution {
    int len;
    boolean[] visit;
    int[] nums;
    Deque<Integer> d;
    Set<List<Integer>> s;

    public List<List<Integer>> permuteUnique(int[] nums) {
        len = nums.length;
        visit = new boolean[len];
        this.nums = nums;
        s = new HashSet<>();
        d = new ArrayDeque<>();
        backtrack();
        return new ArrayList<>(s);
    }

    void backtrack() {
        if (d.size() == len) {
            List<Integer> l = new ArrayList<>(d);
            s.add(l);
            return;
        }
        for (int i = 0; i < len; i++) {
            if (!visit[i]) {
                visit[i] = true;
                d.push(nums[i]);
                backtrack();
                d.pop();
                visit[i] = false;
            }
        }
    }
}
```



## 51. N 皇后

![](D:\Notes\Leetcode\Leetcode.assets\51.png)

相关视频：
[【LeetCode 每日一题】51. N 皇后 | 手写图解版思路 + 代码讲解](https://www.bilibili.com/video/BV17L4y1g7es/)

我的AC代码（Java）：

```java
class Solution {
    int n;
    boolean[] col;
    boolean[] diag1;  // 对角线1：/
    boolean[] diag2;  // 对角线2：\
    char[][] mat;

    List<List<String>> ll;

    public List<List<String>> solveNQueens(int n) {
        init(n);
        backtrack(0);
        return ll;
    }

    void init(int n) {
        this.n = n;
        col = new boolean[n];
        diag1 = new boolean[2 * n - 1];
        diag2 = new boolean[2 * n - 1];
        mat = new char[n][n];
        for (char[] row : mat) {
            Arrays.fill(row, '.');
        }
        ll = new ArrayList<>();
    }

    void backtrack(int i) {
        if (i == n) {
            List<String> l = new ArrayList<>();
            for (char[] row : mat) {
                l.add(new String(row));
            }
            ll.add(l);
            return;
        }
        for (int j = 0; j < n; j++) {
            int idx1 = i + j;
            int idx2 = i - j + n - 1;
            if (col[j] || diag1[idx1] || diag2[idx2]) {
                continue;
            }
            col[j] = true;
            diag1[idx1] = true;
            diag2[idx2] = true;
            mat[i][j] = 'Q';
            backtrack(i + 1);
            col[j] = false;
            diag1[idx1] = false;
            diag2[idx2] = false;
            mat[i][j] = '.';
        }
    }
}
```



## 52. N皇后 II

![](D:\Notes\Leetcode\Leetcode.assets\52.png)

我的AC代码（Java）：

```java
class Solution {
    int n;
    boolean[] col;
    boolean[] diag1;  // 对角线1：/
    boolean[] diag2;  // 对角线2：\
    int total;

    public int totalNQueens(int n) {
        init(n);
        backtrack(0);
        return total;
    }

    void init(int n) {
        this.n = n;
        col = new boolean[n];
        diag1 = new boolean[2 * n - 1];
        diag2 = new boolean[2 * n - 1];
    }

    void backtrack(int i) {
        if (i == n) {
            total++;
            return;
        }
        for (int j = 0; j < n; j++) {
            int idx1 = i + j;
            int idx2 = i - j + n - 1;
            if (col[j] || diag1[idx1] || diag2[idx2]) {
                continue;
            }
            col[j] = true;
            diag1[idx1] = true;
            diag2[idx2] = true;
            backtrack(i + 1);
            col[j] = false;
            diag1[idx1] = false;
            diag2[idx2] = false;
        }
    }
}
```



## 77. 组合

![](D:\Notes\Leetcode\Leetcode.assets\77.png)

相关视频：
[带你学透回溯算法-组合问题（对应力扣题目：77.组合）| 回溯法精讲！](https://www.bilibili.com/video/BV1ti4y1L7cv)

我的AC代码（C++）：
```c++
class Solution {
public:
    int n;
    int k;
    vector<int> s;
    vector<vector<int>> res;
    vector<vector<int>> combine(int n, int k) {
        this->n = n;
        this->k = k;
        backtrack(0, 0);
        return res;
    }
    void backtrack(int idx, int len) {
        if (len == k) {
            res.push_back(s);
            return;
        }
        for (int i = idx + 1; i <= n - k + len + 1; i++) {
            s.push_back(i);
            backtrack(i, len + 1);
            s.pop_back();
        }
    }
};
```

我的AC代码（Java）：

```java
class Solution {
    int n;
    int k;
    Deque<Integer> d;
    List<List<Integer>> ll;

    public List<List<Integer>> combine(int n, int k) {
        this.n = n;
        this.k = k;
        d = new ArrayDeque<>();
        ll = new ArrayList<>();
        backtrack(1, 1);
        return ll;
    }

    void backtrack(int idx, int len) {
        if (d.size() == k) {
            ll.add(Arrays.asList(d.toArray(new Integer[d.size()])));
            return;
        }
        for (int i = idx; i <= n - k + len; i++) {
            d.push(i);
            backtrack(i + 1, len + 1);
            d.pop();
        }
    }
}
```

