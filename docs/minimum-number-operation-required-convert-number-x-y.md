# 将数字 x 转换为 y 所需的最小操作次数

> 原文:[https://www . geesforgeks . org/minimum-number-operation-required-convert-number-x-y/](https://www.geeksforgeeks.org/minimum-number-operation-required-convert-number-x-y/)

给定初始数字 x 和下面给出的两个操作:

1.  将数字乘以 2。
2.  从数字中减去 1。

任务是找出仅使用上述两个操作将数字 x 转换为 y 所需的最小操作数。我们可以多次应用这些操作。
约束:
1 < = x，y < = 1000
**示例:**

```
Input : x = 4, y = 7
Output : 2
We can transform x into y using following
two operations.
1\. 4*2  = 8
2\. 8-1  = 7

Input  : x = 2, y = 5
Output : 4
We can transform x into y using following
four operations.
1\. 2*2  = 4
2\. 4-1   = 3
3\. 3*2  = 6
4\. 6-1   = 5
Answer = 4
Note that other sequences of two operations 
would take more operations.
```

想法是用 [BFS](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) 来做这个。我们运行一个 BFS，通过乘以 2 再减去 1 来创建节点，这样我们就可以从起始数获得所有可能的数。
要点:
1)当我们从一个数字中减去 1，如果它变成< 0，即负，那么就没有理由从它创建下一个节点(根据输入约束，数字 x 和 y 是正的)。
2)同样，如果我们已经创造了一个数字，那么就没有理由再创造它。即，我们维护被访问的阵列。

## C++

```
// C++ program to find minimum number of steps needed
// to convert a number x into y with two operations
// allowed : (1) multiplication with 2 (2) subtraction
// with 1.
#include <bits/stdc++.h>
using namespace std;

// A node of BFS traversal
struct node {
    int val;
    int level;
};

// Returns minimum number of operations
// needed to convert x into y using BFS
int minOperations(int x, int y)
{
    // To keep track of visited numbers
    // in BFS.
    set<int> visit;

    // Create a queue and enqueue x into it.
    queue<node> q;
    node n = { x, 0 };
    q.push(n);

    // Do BFS starting from x
    while (!q.empty()) {
        // Remove an item from queue
        node t = q.front();
        q.pop();

        // If the removed item is target
        // number y, return its level
        if (t.val == y)
            return t.level;

        // Mark dequeued number as visited
        visit.insert(t.val);

        // If we can reach y in one more step
        if (t.val * 2 == y || t.val - 1 == y)
            return t.level + 1;

        // Insert children of t if not visited
        // already
        if (visit.find(t.val * 2) == visit.end()) {
            n.val = t.val * 2;
            n.level = t.level + 1;
            q.push(n);
        }
        if (t.val - 1 >= 0
            && visit.find(t.val - 1) == visit.end()) {
            n.val = t.val - 1;
            n.level = t.level + 1;
            q.push(n);
        }
    }
}

// Driver code
int main()
{
    int x = 4, y = 7;
    cout << minOperations(x, y);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum
// number of steps needed to
// convert a number x into y
// with two operations allowed :
// (1) multiplication with 2
// (2) subtraction with 1.

import java.util.HashSet;
import java.util.LinkedList;
import java.util.Set;

class GFG {
    int val;
    int steps;

    public GFG(int val, int steps)
    {
        this.val = val;
        this.steps = steps;
    }
}

public class GeeksForGeeks {
    private static int minOperations(int src, int target)
    {

        Set<GFG> visited = new HashSet<>(1000);
        LinkedList<GFG> queue = new LinkedList<GFG>();

        GFG node = new GFG(src, 0);

        queue.offer(node);
        visited.add(node);

        while (!queue.isEmpty()) {
            GFG temp = queue.poll();
            visited.add(temp);

            if (temp.val == target) {
                return temp.steps;
            }

            int mul = temp.val * 2;
            int sub = temp.val - 1;

            // given constraints
            if (mul > 0 && mul < 1000) {
                GFG nodeMul = new GFG(mul, temp.steps + 1);
                queue.offer(nodeMul);
            }
            if (sub > 0 && sub < 1000) {
                GFG nodeSub = new GFG(sub, temp.steps + 1);
                queue.offer(nodeSub);
            }
        }
        return -1;
    }

    // Driver code
    public static void main(String[] args)
    {
        // int x = 2, y = 5;
        int x = 4, y = 7;
        GFG src = new GFG(x, y);
        System.out.println(minOperations(x, y));
    }
}

// This code is contributed by Rahul
```

## 蟒蛇 3

```
# Python3 program to find minimum number of
# steps needed to convert a number x into y
# with two operations allowed :
# (1) multiplication with 2
# (2) subtraction with 1.
import queue

# A node of BFS traversal

class node:
    def __init__(self, val, level):
        self.val = val
        self.level = level

# Returns minimum number of operations
# needed to convert x into y using BFS

def minOperations(x, y):

    # To keep track of visited numbers
    # in BFS.
    visit = set()

    # Create a queue and enqueue x into it.
    q = queue.Queue()
    n = node(x, 0)
    q.put(n)

    # Do BFS starting from x
    while (not q.empty()):

        # Remove an item from queue
        t = q.get()

        # If the removed item is target
        # number y, return its level
        if (t.val == y):
            return t.level

        # Mark dequeued number as visited
        visit.add(t.val)

        # If we can reach y in one more step
        if (t.val * 2 == y or t.val - 1 == y):
            return t.level+1

        # Insert children of t if not visited
        # already
        if (t.val * 2 not in visit):
            n.val = t.val * 2
            n.level = t.level + 1
            q.put(n)
        if (t.val - 1 >= 0 and t.val - 1 not in visit):
            n.val = t.val - 1
            n.level = t.level + 1
            q.put(n)

# Driver code
if __name__ == '__main__':

    x = 4
    y = 7
    print(minOperations(x, y))

# This code is contributed by PranchalK
```

## C#

```
// C# program to find minimum
// number of steps needed to
// convert a number x into y
// with two operations allowed :
// (1) multiplication with 2
// (2) subtraction with 1.
using System;
using System.Collections.Generic;

public class GFG {
    public int val;
    public int steps;

    public GFG(int val, int steps)
    {
        this.val = val;
        this.steps = steps;
    }
}

public class GeeksForGeeks {
    private static int minOperations(int src, int target)
    {

        HashSet<GFG> visited = new HashSet<GFG>(1000);
        List<GFG> queue = new List<GFG>();

        GFG node = new GFG(src, 0);

        queue.Add(node);
        visited.Add(node);

        while (queue.Count != 0) {
            GFG temp = queue[0];
            queue.RemoveAt(0);
            visited.Add(temp);

            if (temp.val == target) {
                return temp.steps;
            }

            int mul = temp.val * 2;
            int sub = temp.val - 1;

            // given constraints
            if (mul > 0 && mul < 1000) {
                GFG nodeMul = new GFG(mul, temp.steps + 1);
                queue.Add(nodeMul);
            }
            if (sub > 0 && sub < 1000) {
                GFG nodeSub = new GFG(sub, temp.steps + 1);
                queue.Add(nodeSub);
            }
        }
        return -1;
    }

    // Driver code
    public static void Main(String[] args)
    {

        // int x = 2, y = 5;
        int x = 4, y = 7;
        GFG src = new GFG(x, y);
        Console.WriteLine(minOperations(x, y));
    }
}

// This code is contributed by aashish1995
```

**输出:**

```
2
```

本文由**唯品会**供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。

**优化方案**

在第二种方法中，我们将检查数字中最少的位，并根据该位的值做出决定。

我们将把 y 转换成 x，而不是把 x 转换成 y，并且将进行与把 x 转换成 y 相同次数的反向操作。

所以，y 的反向操作将是:

1.  将数字除以 2
2.  将数字增加 1

## C++14

```
#include <iostream>
using namespace std;

int min_operations(int x, int y) {

    // If both are equal then return 0
    if (x == y)
        return 0;

    // Check if conversion is possible or not
    if (x <= 0 && y > 0)
        return -1;

    // If x > y then we can just increase y by 1
    // Therefore return the number of increments required
    if (x > y)
        return x - y;

    // If last bit is odd
    // then increment y so that we can make it even
    if (y & 1)
        return 1 + min_operations(x, y + 1);

    // If y is even then divide it by 2 to make it closer to
    // x
    else
        return 1 + min_operations(x, y / 2);
}

// Driver code
signed main() {
    cout << min_operations(4, 7) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */
import java.io.*;

class GFG
{
    static int minOperations(int x, int y)
    {

        // If both are equal then return 0
        if (x == y)
            return 0;

        // Check if conversion is possible or not
        if (x <= 0 && y > 0)
            return -1;

        // If x > y then we can just increase y by 1
        // Therefore return the number of increments
        // required
        if (x > y)
            return x - y;

        // If last bit is odd
        // then increment y so that we can make it even
        if (y % 2 != 0)
            return 1 + minOperations(x, y + 1);

        // If y is even then divide it by 2 to make it
        // closer to x
        else
            return 1 + minOperations(x, y / 2);
    }

    public static void main(String[] args)
    {
        System.out.println(minOperations(4, 7));
    }
}

// This code is contributed by Shobhit Yadav
```

## 蟒蛇 3

```
def min_operations(x, y):
    # If both are equal then return 0
    if x == y:
        return 0

    # Check if conversion is possible or not
    if x <= 0 and y > 0:
        return -1

    # If x > y then we can just increase y by 1
    # Therefore return the number of increments required
    if x > y:
        return a-b

    # If last bit is odd
    # then increment y so that we can make it even
    if y & 1 == 1:
        return 1+min_operations(x, y+1)

    # If y is even then divide it by 2 to make it closer to x
    else:
        return 1+min_operations(x, y//2)

# Driver code
print(min_operations(4, 7))
```

**Output**

```
2
```

优化的解决方案是由**燃烧文件贡献的。**如果你喜欢 GeeksforGeeks 并想投稿，你也可以写一篇文章，把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。