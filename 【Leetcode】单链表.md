# 【Leetcode】单链表



[toc]



单链表结点的定义（Java）：

```java
public class ListNode {
    int val;
    ListNode next;
    ListNode() {}
    ListNode(int val) { this.val = val; }
    ListNode(int val, ListNode next) { this.val = val; this.next = next; }
}
```



## 2. 两数相加

![](D:\Notes\Leetcode\Leetcode.assets\2.png)

我的AC代码（Java）：

```java
class Solution {
    public static ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode l3 = new ListNode();
        ListNode p = l3;
        int s;
        int d;
        int c = 0;
        while (l1 != null && l2 != null) {
            s = l1.val + l2.val + c;
            d = s % 10;
            c = s / 10;
            p.next = new ListNode(d);
            p = p.next;
            l1 = l1.next;
            l2 = l2.next;
        }
        if (l1 == null && l2 != null) {
            while (l2 != null) {
                s = l2.val + c;
                d = s % 10;
                c = s / 10;
                p.next = new ListNode(d);
                p = p.next;
                l2 = l2.next;
            }
        } else if (l1 != null && l2 == null) {
            while (l1 != null) {
                s = l1.val + c;
                d = s % 10;
                c = s / 10;
                p.next = new ListNode(d);
                p = p.next;
                l1 = l1.next;
            }
        }
        if (c != 0) {
            p.next = new ListNode(c);
        }
        return l3.next;
    }
}
```



## 19. 删除链表的倒数第 N 个结点

![](D:\Notes\Leetcode\Leetcode.assets\19.png)

我的AC代码（Java，解法1，两趟遍历）：

```java
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode p = head;
        int len = 0;
        while (p != null) {
            len++;
            p = p.next;
        }
        if (len == 1 || len == n) {
            head = head.next;
        } else {  // 删除倒数第n个结点 = 删除正数第len-n+1个结点（从1开始计数）
            p = head;
            for (int i = 1; i < len - n; i++) {
                p = p.next;
            }
            p.next = p.next.next;
        }
        return head;
    }
}
```

我的AC代码（Java，解法2，一趟遍历）：

```java
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        List<ListNode> l = new ArrayList<>();
        ListNode p = head;
        int len = 0;
        while (p != null) {
            l.add(p);
            len++;
            p = p.next;
        }
        if (len == 1 || len == n) {
            head = head.next;
        } else {  // 删除倒数第n个结点 = 删除正数第len-n+1个结点（从1开始计数）
            l.get(len - n - 1).next = l.get(len - n - 1).next.next;
        }
        return head;
    }
}
```



## 21. 合并两个有序链表

![](D:\Notes\Leetcode\Leetcode.assets\21.png)

我的AC代码（Java）：

```java
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode l3 = new ListNode();
        ListNode p = l3;
        while (l1 != null && l2 != null) {
            if (l1.val <= l2.val) {
                p.next = l1;
                l1 = l1.next;
                p = p.next;
            } else {
                p.next = l2;
                l2 = l2.next;
                p = p.next;
            }
        }
        if (l1 != null && l2 == null) {
            p.next = l1;
            l1 = l1.next;
            p = p.next;
        } else if (l1 == null && l2 != null) {
            while (l2 != null) {
                p.next = l2;
                l2 = l2.next;
                p = p.next;
            }
        }
        return l3.next;
    }
}
```



## 23. 合并K个升序链表

![](D:\Notes\Leetcode\Leetcode.assets\23.png)

我的AC代码（Java）：

```java
class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
        int k = lists.length;
        ListNode[] ptrs = new ListNode[k];
        System.arraycopy(lists, 0, ptrs, 0, k);
        ListNode l = new ListNode();
        ListNode p = l;
        while (!isAllNull(ptrs)) {
            p.next = getMinNode(ptrs);
            p = p.next;
        }
        return l.next;
    }

    private boolean isAllNull(ListNode[] ptrs) {
        for (ListNode p : ptrs) {
            if (p != null) {
                return false;
            }
        }
        return true;
    }

    private ListNode getMinNode(ListNode[] ptrs) {
        long minVal = Long.MAX_VALUE;
        int minIdx = -1;
        ListNode minNode = null;
        for (int i = 0; i < ptrs.length; i++) {
            ListNode p = ptrs[i];
            if (p == null) {
                continue;
            }
            if (p.val < minVal) {
                minVal = p.val;
                minIdx = i;
                minNode = p;
            }
        }
        if (minIdx != -1) {
            ptrs[minIdx] = ptrs[minIdx].next;
        }
        return minNode;
    }
}
```



## 24. 两两交换链表中的节点

![](D:\Notes\Leetcode\Leetcode.assets\24.png)

我的AC代码（Java）：

```java
class Solution {
    public ListNode swapPairs(ListNode head) {
        if (head != null && head.next != null) {
            ListNode p1 = head;
            ListNode p2 = head.next;
            head = p2;
            p1.next = p2.next;
            p2.next = p1;
            while (p1.next != null && p1.next.next != null) {
                ListNode t = p1;
                p1 = t.next;
                p2 = p1.next;
                t.next = p2;
                p1.next = p2.next;
                p2.next = p1;
            }
        }
        return head;
    }
}
```



## 25. K 个一组翻转链表

![](D:\Notes\Leetcode\Leetcode.assets\25.png)

我的AC代码（Java）：

```java
class Solution {
    public ListNode reverseKGroup(ListNode head, int k) {
        ListNode l = new ListNode(0, head);
        ListNode t = l;
        ListNode p1 = t.next;
        ListNode p2 = t;
        int cnt = 0;
        while (p2.next != null) {
            p2 = p2.next;
            cnt++;
            if (cnt == k) {
                t.next = reverseList(p1, p2);
                t = p1;
                p1 = t.next;
                p2 = t;
                cnt = 0;
            }
        }
        return l.next;
    }

    private ListNode reverseList(ListNode head, ListNode tail) {
        ListNode p = tail.next;  // previous
        ListNode c = head;  // current
        ListNode n = c.next;  // next
        while (c != tail) {
            c.next = p;
            p = c;
            c = n;
            n = n.next;
        }
        c.next = p;
        return c;
    }
}
```



## 61. 旋转链表

![](D:\Notes\Leetcode\Leetcode.assets\61.png)

我的AC代码（Java）：

```java
class Solution {
    public ListNode rotateRight(ListNode head, int k) {
        if (head == null) {
            return head;
        }
        int len = 1;
        ListNode tail = head;
        while (tail.next != null) {
            tail = tail.next;
            len++;
        }
        k = k % len;
        if (k == 0) {
            return head;
        }
        tail.next = head;
        for (int i = 0; i < len - k; i++) {
            tail = tail.next;
        }
        head = tail.next;
        tail.next = null;
        return head;
    }
}
```

