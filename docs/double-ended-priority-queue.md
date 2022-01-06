# 双端优先队列

> 原文:[https://www.geeksforgeeks.org/double-ended-priority-queue/](https://www.geeksforgeeks.org/double-ended-priority-queue/)

双端优先级队列支持[最大堆](https://www.geeksforgeeks.org/binary-heap/)(最大优先级队列)和[最小堆](https://www.geeksforgeeks.org/binary-heap/)(最小优先级队列)的操作。双端优先级队列中预期有以下操作。

1.  getMax():返回最大元素。
2.  getMin():返回最小元素。
3.  deleteMax():删除最大元素。
4.  deleteMin():删除最小元素。
5.  size():返回元素计数。
6.  isEmpty():如果队列为空，则返回 true。

我们可以尝试不同的数据结构，比如[链表](https://www.geeksforgeeks.org/linked-list-set-1-introduction/)。在链表的情况下，如果我们按照排序的顺序维护元素，那么除了需要 O(n)时间的操作 insert()之外，所有操作的时间复杂度都变成 O(1)。
我们可以试试**两堆**(最小堆和最大堆)。我们维护最小堆中每个最大堆元素的指针。为了得到最小元素，我们简单地返回根。为了得到最大元素，我们返回最大堆的根。为了插入一个元素，我们同时在最小堆和最大堆中插入。主要思想是保持一一对应，这样 deleteMin()和 deleteMax()就可以在 O(Log n)时间内完成。

1.  getMax():或(1)
2.  getmin():或(1)
3.  deleteMax():或(Log n)
4.  deletemin()-或(Log n)
5.  大小():O(1)
6.  isEmpty():或(1)

另一种解决方案是使用**自平衡二叉查找树。**一个自平衡 BST 实现为 C++中的[集和 Java 中的](https://www.geeksforgeeks.org/set-in-cpp-stl/)[树集](https://www.geeksforgeeks.org/treeset-in-java-with-examples/)。

1.  getMax():或(1)
2.  getmin():或(1)
3.  deleteMax():或(Log n)
4.  deletemin()-或(Log n)
5.  大小():O(1)
6.  isEmpty():或(1)

以下是上述方法的实现:

## C++

```
// C++ program to implement double-ended
// priority queue using self balancing BST.
#include <bits/stdc++.h>
using namespace std;

struct DblEndedPQ {
    set<int> s;

    // Returns size of the queue. Works in
    // O(1) time
    int size()
    {
       return s.size();
    }

    // Returns true if queue is empty. Works
    // in O(1) time
    bool isEmpty()
    {
       return (s.size() == 0);
    }

    // Inserts an element. Works in O(Log n)
    // time
    void insert(int x)
    {
        s.insert(x);
    }

    // Returns minimum element. Works in O(1)
    // time
    int getMin()
    {
        return *(s.begin());
    }

    // Returns maximum element. Works in O(1)
    // time
    int getMax()
    {
        return *(s.rbegin());
    }

    // Deletes minimum element. Works in O(Log n)
    // time 
    void deleteMin()
    {
        if (s.size() == 0)
            return;
        s.erase(s.begin());
    }

    // Deletes maximum element. Works in O(Log n)
    // time 
    void deleteMax()
    {
        if (s.size() == 0)
            return;
        auto it = s.end();
        it--;
        s.erase(it);
    }
};

// Driver code
int main()
{
    DblEndedPQ d;
    d.insert(10);
    d.insert(50);
    d.insert(40);
    d.insert(20);
    cout << d.getMin() << endl;
    cout << d.getMax() << endl;
    d.deleteMax();
    cout << d.getMax() << endl;
    d.deleteMin();
    cout << d.getMin() << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement double-ended
// priority queue using self balancing BST.
import java.util.*;
class solution
{

static class DblEndedPQ {
    Set<Integer> s;
    DblEndedPQ()
    {
        s= new HashSet<Integer>();
    }
    // Returns size of the queue. Works in
    // O(1) time
    int size()
    {
    return s.size();
    }

    // Returns true if queue is empty. Works
    // in O(1) time
    boolean isEmpty()
    {
    return (s.size() == 0);
    }

    // Inserts an element. Works in O(Log n)
    // time
    void insert(int x)
    {
        s.add(x);

    }

    // Returns minimum element. Works in O(1)
    // time
    int getMin()
    {
        return Collections.min(s,null);
    }

    // Returns maximum element. Works in O(1)
    // time
    int getMax()
    {
        return Collections.max(s,null);
    }

    // Deletes minimum element. Works in O(Log n)
    // time
    void deleteMin()
    {
        if (s.size() == 0)
            return ;
        s.remove(Collections.min(s,null));

    }

    // Deletes maximum element. Works in O(Log n)
    // time
    void deleteMax()
    {
        if (s.size() == 0)
            return ;
        s.remove(Collections.max(s,null));

    }
};

// Driver code
public static void main(String args[])
{
    DblEndedPQ d= new DblEndedPQ();
    d.insert(10);
    d.insert(50);
    d.insert(40);
    d.insert(20);
    System.out.println( d.getMin() );
    System.out.println(d.getMax() );
    d.deleteMax();
    System.out.println( d.getMax() );
    d.deleteMin();
    System.out.println( d.getMin() );
}
}
//contributed by Arnab Kundu
```

## C#

```
// C# program to implement double-ended
// priority queue using self balancing BST.
using System;
using System.Linq;
using System.Collections.Generic;

class GFG
{

public class DblEndedPQ
{
    HashSet<int> s;
    public DblEndedPQ()
    {
        s = new HashSet<int>();
    }

    // Returns size of the queue. Works in
    // O(1) time
    public int size()
    {
        return s.Count;
    }

    // Returns true if queue is empty. Works
    // in O(1) time
    public bool isEmpty()
    {
        return (s.Count == 0);
    }

    // Inserts an element. Works in O(Log n)
    // time
    public void insert(int x)
    {
        s.Add(x);

    }

    // Returns minimum element. Works in O(1)
    // time
    public int getMin()
    {
        return s.Min();
    }

    // Returns maximum element. Works in O(1)
    // time
    public int getMax()
    {
        return s.Max();
    }

    // Deletes minimum element. Works in O(Log n)
    // time
    public void deleteMin()
    {
        if (s.Count == 0)
            return ;
        s.Remove(s.Min());

    }

    // Deletes maximum element. Works in O(Log n)
    // time
    public void deleteMax()
    {
        if (s.Count == 0)
            return ;
        s.Remove(s.Max());

    }
};

// Driver code
public static void Main(String[] args)
{
    DblEndedPQ d= new DblEndedPQ();
    d.insert(10);
    d.insert(50);
    d.insert(40);
    d.insert(20);
    Console.WriteLine( d.getMin() );
    Console.WriteLine(d.getMax() );
    d.deleteMax();
    Console.WriteLine( d.getMax() );
    d.deleteMin();
    Console.WriteLine( d.getMin() );
}
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>
      // JavaScript program to implement double-ended
      // priority queue using self balancing BST.
      class DblEndedPQ {
        constructor() {
          this.s = new Set();
        }

        // Returns size of the queue. Works in
        // O(1) time
        size() {
          return this.s.size;
        }

        // Returns true if queue is empty. Works
        // in O(1) time
        isEmpty() {
          return this.s.size == 0;
        }

        // Inserts an element. Works in O(Log n)
        // time
        insert(x) {
          this.s.add(x);
        }

        // Returns minimum element. Works in O(1)
        // time
        getMin() {
          return Math.min(...Array.from(this.s.values()));
        }

        // Returns maximum element. Works in O(1)
        // time
        getMax() {
          return Math.max(...Array.from(this.s.values()));
        }

        // Deletes minimum element. Works in O(Log n)
        // time
        deleteMin() {
          if (this.s.size == 0) return;
          this.s.delete(this.getMin());
        }

        // Deletes maximum element. Works in O(Log n)
        // time
        deleteMax() {
          if (this.s.size == 0) return;
          this.s.delete(this.getMax());
        }
      }

      // Driver code
      var d = new DblEndedPQ();
      d.insert(10);
      d.insert(50);
      d.insert(40);
      d.insert(20);
      document.write(d.getMin() + "<br>");
      document.write(d.getMax() + "<br>");
      d.deleteMax();
      document.write(d.getMax() + "<br>");
      d.deleteMin();
      document.write(d.getMin() + "<br>");

      // This code is contributed by rdtank.
    </script>
```

**Output:** 

```
10
50
40
20
```

**堆和 BST 解决方案的比较**
基于堆的解决方案需要 O(n)个额外的空间用于额外的堆。基于 BST 的解决方案不需要额外的空间。基于堆的解决方案的优点是缓存友好。