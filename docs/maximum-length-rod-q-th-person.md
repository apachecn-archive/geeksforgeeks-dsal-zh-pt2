# 第 Q 个人最大杆长

> 原文:[https://www . geesforgeks . org/最大长度-杆-q-th-person/](https://www.geeksforgeeks.org/maximum-length-rod-q-th-person/)

给定阵列中 n 根棒的长度**a【】**。如果任何人拿起任何杆，最长杆的一半(或(最大+ 1) / 2)被分配，剩余部分(最大-1)/2 被放回。可以假设总是有足够数量的杆可用，回答在数组 q[]中给出的 M 个查询，以找到对 **q <sup>和</sup>T5】人可用的最大杆长度，前提是**q<sup>I</sup>T9】是从 1 开始的有效的人号。
示例:**** 

```
Input : a[] = {6, 5, 9, 10, 12}
        q[] = {1, 3}
Output : 12 9
The first person gets maximum length as 12\. 
We remove 12 from array and put back (12 -1) / 2 = 5\. 
Second person gets maximum length as 10\.  
We put back (10 - 1)/2 which is 4.
Third person gets maximum length as 9.

Input : a[] = {6, 5, 9, 10, 12}
        q[] = {3, 1, 2, 7, 4, 8, 9, 5, 10, 6}
Output : 9 12 10 5 6 4 3 6 3 5
```

**进场:**
使用一叠和一个队列。首先对所有长度进行排序，并将其放入堆栈中。现在，取栈顶元素，除以 2，将剩余长度推到队列中。现在，从下一个客户开始:

1.  如果堆栈为空，弹出前队列并推回队列。如果非零，则为一半(前/ 2)。
2.  如果队列为空，从堆栈中弹出并推入队列，如果非零，则为一半(顶部/ 2)。
3.  如果两者都不是空的，比较顶部和前面，哪个更大，应该弹出，除以 2，然后推回来。
4.  如果两个都是空的，商店就是空的！停在这里！

在上面的每个步骤中，将第 i <sup>个</sup>客户可用的长度存储在单独的数组中，比如“ans”。现在，通过输出 ans[Q<sub>I</sub>开始回答问题。
**以下是上述方法的实施:**

## C++

```
// CPP code to find the length of largest
// rod available for Q-th customer
#include <bits/stdc++.h>
using namespace std;

// function to find largest length of
// rod available for Q-th customer
vector<int> maxRodLength(int ar[],
                        int n, int m)
{
    queue<int> q;

    // sort the rods according to lengths
    sort(ar, ar + n);

    // Push sorted elements to a stack
    stack<int> s;
    for (int i = 0; i < n; i++)
        s.push(ar[i]);

    vector<int> ans;

    while (!s.empty() || !q.empty()) {
        int val;

        // If queue is empty -> pop from stack
        // and push to queue it’s half(top/2),
        // if non zero.
        if (q.empty()) {
            val = s.top();
            ans.push_back(val);
            s.pop();
            val /= 2;

            if (val)
                q.push(val);
        }
        // If stack is empty -> pop front from
        // queue and push back to queue it’s
        // half(front/2), if non zero.
        else if (s.empty()) {
            val = q.front();
            ans.push_back(val);
            q.pop();
            val /= 2;
            if (val != 0)
                q.push(val);
        }
        // If both are non empty ->
        // compare top and front, whichsoever is
        // larger should be popped, divided by 2
        // and then pushed back.
        else {
            val = s.top();
            int fr = q.front();
            if (fr > val) {
                ans.push_back(fr);
                q.pop();
                fr /= 2;
                if (fr)
                    q.push(fr);
            }
            else {
                ans.push_back(val);
                s.pop();
                val /= 2;
                if (val)
                    q.push(val);
            }
        }
    }

    return ans;
}

// Driver code
int main()
{
    // n : number of rods
    // m : number of queries
    int n = 5, m = 10;

    int ar[n] = { 6, 5, 9, 10, 12 };

    vector<int> ans = maxRodLength(ar, n, m);

    int query[] = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
    int size = sizeof(query) / sizeof(query[0]);
    for (int i = 0; i < size; i++)
        cout << ans[query[i] - 1] << " ";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA code to find the length of largest
// rod available for Q-th customer
import java.util.*;

class GFG
{

// function to find largest length of
// rod available for Q-th customer
static Vector<Integer> maxRodLength(int ar[],
                        int n, int m)
{
    Queue<Integer> q = new LinkedList<>();

    // sort the rods according to lengths
    Arrays.sort(ar);

    // Push sorted elements to a stack
    Stack<Integer> s = new Stack<Integer>();
    for (int i = 0; i < n; i++)
        s.add(ar[i]);

    Vector<Integer> ans = new Vector<Integer>();

    while (!s.isEmpty() || !q.isEmpty())
    {
        int val;

        // If queue is empty.pop from stack
        // and push to queue its half(top/2),
        // if non zero.
        if (q.isEmpty())
        {
            val = s.peek();
            ans.add(val);
            s.pop();
            val /= 2;

            if (val > 0)
                q.add(val);
        }

        // If stack is empty.pop front from
        // queue and push back to queue its
        // half(front/2), if non zero.
        else if (s.isEmpty())
        {
            val = q.peek();
            ans.add(val);
            q.remove();
            val /= 2;
            if (val != 0)
                q.add(val);
        }

        // If both are non empty .
        // compare top and front, whichsoever is
        // larger should be popped, divided by 2
        // and then pushed back.
        else
        {
            val = s.peek();
            int fr = q.peek();
            if (fr > val)
            {
                ans.add(fr);
                q.remove();
                fr /= 2;
                if (fr > 0)
                    q.add(fr);
            }
            else
            {
                ans.add(val);
                s.pop();
                val /= 2;
                if (val > 0)
                    q.add(val);
            }
        }
    }
    return ans;
}

// Driver code
public static void main(String[] args)
{
    // n : number of rods
    // m : number of queries
    int n = 5, m = 10;

    int []ar = { 6, 5, 9, 10, 12 };

    Vector<Integer> ans = maxRodLength(ar, n, m);

    int query[] = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
    int size = query.length;
    for (int i = 0; i < size; i++)
        System.out.print(ans.get(query[i] - 1) + " ");
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 code to find the length of largest
# rod available for Q-th customer

# function to find largest length of
# rod available for Q-th customer
def maxRodLength(ar, n, m):
    q = []

    # sort the rods according to lengths
    ar.sort()

    # Push sorted elements to a stack
    s = []
    for i in range(n):
        s.append(ar[i])

    ans = []

    while len(s) != 0 or len(q) != 0 :
        # If queue is empty.pop from stack
        # and push to queue its half(top/2),
        # if non zero.
        if len(q) == 0:
            val = s[-1]
            ans.append(val)
            s.pop()
            val = int(val / 2)

            if (val > 0):
                q.append(val)

        # If stack is empty.pop front from
        # queue and push back to queue its
        # half(front/2), if non zero.
        elif len(s) == 0:
            val = q[0]
            ans.append(val)
            q.pop(0)
            val = int(val / 2)
            if (val != 0):
                q.append(val)

        # If both are non empty .
        # compare top and front, whichsoever is
        # larger should be popped, divided by 2
        # and then pushed back.
        else:
            val = s[-1]
            fr = q[0]
            if (fr > val):
                ans.append(fr)
                q.pop(0)
                fr = int(fr / 2)
                if (fr > 0):
                    q.append(fr)
            else:
                ans.append(val)
                s.pop()
                val = int(val / 2)
                if (val > 0):
                    q.append(val)
    return ans

# n : number of rods
# m : number of queries
n, m = 5, 10

ar = [ 6, 5, 9, 10, 12 ]

ans = maxRodLength(ar, n, m)

query = [ 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 ]
size = len(query)
for i in range(size):
    print(ans[query[i] - 1], end = " ")

    # This code is contributed by decode2207.
```

## C#

```
// C# code to find the length of largest
// rod available for Q-th customer
using System;
using System.Collections.Generic;
class GFG {

    // function to find largest length of
    // rod available for Q-th customer
    static List<int> maxRodLength(int[] ar, int n, int m)
    {
        Queue<int> q = new Queue<int>();

        // sort the rods according to lengths
        Array.Sort(ar);

        // Push sorted elements to a stack
        Stack<int> s = new Stack<int>();
        for (int i = 0; i < n; i++)
            s.Push(ar[i]);

        List<int> ans = new List<int>();

        while (s.Count > 0 || q.Count > 0)
        {
            int val;

            // If queue is empty.pop from stack
            // and push to queue its half(top/2),
            // if non zero.
            if (q.Count == 0)
            {
                val = s.Peek();
                ans.Add(val);
                s.Pop();
                val /= 2;

                if (val > 0)
                    q.Enqueue(val);
            }

            // If stack is empty.pop front from
            // queue and push back to queue its
            // half(front/2), if non zero.
            else if (s.Count == 0)
            {
                val = q.Peek();
                ans.Add(val);
                q.Dequeue();
                val /= 2;
                if (val != 0)
                    q.Enqueue(val);
            }

            // If both are non empty .
            // compare top and front, whichsoever is
            // larger should be popped, divided by 2
            // and then pushed back.
            else
            {
                val = s.Peek();
                int fr = q.Peek();
                if (fr > val)
                {
                    ans.Add(fr);
                    q.Dequeue();
                    fr /= 2;
                    if (fr > 0)
                        q.Enqueue(fr);
                }
                else
                {
                    ans.Add(val);
                    s.Pop();
                    val /= 2;
                    if (val > 0)
                        q.Enqueue(val);
                }
            }
        }
        return ans;
    }

  // Driver code
  static void Main()
  {

    // n : number of rods
    // m : number of queries
    int n = 5, m = 10;

    int[] ar = { 6, 5, 9, 10, 12 };

    List<int> ans = maxRodLength(ar, n, m);

    int[] query = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
    int size = query.Length;
    for (int i = 0; i < size; i++)
    {
        Console.Write(ans[query[i] - 1] + " ");
    }
  }
}

// This code is contributed by divyesh072019
```

## java 描述语言

```
<script>
    // Javascript code to find the length of largest
    // rod available for Q-th customer

    // function to find largest length of
    // rod available for Q-th customer
    function maxRodLength(ar, n, m)
    {
        let q = [];

        // sort the rods according to lengths
        ar.sort(function(a, b){return a - b});

        // Push sorted elements to a stack
        let s = [];
        for (let i = 0; i < n; i++)
            s.push(ar[i]);

        let ans = [];

        while (s.length > 0 || q.length > 0)
        {
            let val;

            // If queue is empty.pop from stack
            // and push to queue its half(top/2),
            // if non zero.
            if (q.length == 0)
            {
                val = s[s.length - 1];
                ans.push(val);
                s.pop();
                val = parseInt(val / 2, 10);

                if (val > 0)
                    q.push(val);
            }

            // If stack is empty.pop front from
            // queue and push back to queue its
            // half(front/2), if non zero.
            else if (s.length == 0)
            {
                val = q[0];
                ans.push(val);
                q.shift();
                val = parseInt(val / 2, 10);
                if (val != 0)
                    q.push(val);
            }

            // If both are non empty .
            // compare top and front, whichsoever is
            // larger should be popped, divided by 2
            // and then pushed back.
            else
            {
                val = s[s.length - 1];
                let fr = q[0];
                if (fr > val)
                {
                    ans.push(fr);
                    q.shift();
                    fr = parseInt(fr / 2, 10);
                    if (fr > 0)
                        q.push(fr);
                }
                else
                {
                    ans.push(val);
                    s.pop();
                    val = parseInt(val / 2, 10);
                    if (val > 0)
                        q.push(val);
                }
            }
        }
        return ans;
    }

    // n : number of rods
    // m : number of queries
    let n = 5, m = 10;

    let ar = [ 6, 5, 9, 10, 12 ];

    let ans = maxRodLength(ar, n, m);

    let query = [ 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 ];
    let size = query.length;
    for (let i = 0; i < size; i++)
        document.write(ans[query[i] - 1] + " ");

// This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
12 10 9 6 6 5 5 4 3 3
```

**时间复杂度:** O(N log(N))