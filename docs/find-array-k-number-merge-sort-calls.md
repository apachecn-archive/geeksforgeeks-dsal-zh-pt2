# 找到 k 个合并排序调用的数组

> 原文:[https://www . geesforgeks . org/find-array-k-number-merge-sort-calls/](https://www.geeksforgeeks.org/find-array-k-number-merge-sort-calls/)

给定两个数字 n 和 k，找到一个包含[1，n]中值的数组，并且需要对[递归合并排序函数](https://www.geeksforgeeks.org/merge-sort/)进行 k 次调用。
示例:

```
Input : n = 3
        k = 3
Output : a[] = {2, 1, 3}
Explanation:
Here, a[] = {2, 1, 3}
First of all, mergesort(0, 3) will be called,
which then sets mid = 1 and calls mergesort(0, 
1) and mergesort(1, 3), which do not perform
any recursive calls because segments (0, 1) 
and (1, 3) are sorted.
Hence, total mergesort calls are 3.

Input : n = 4
        k = 1
Output : a[] = {1, 2, 3, 4}
Explanation:
Here, a[] = {1, 2, 3, 4} then there will be
1 mergesort call — mergesort(0, 4), which 
will check that the array is sorted and then
end.
```

如果我们有一个 k 偶数的值，那么没有解决办法，因为调用的数量总是奇数(开始时一个调用，每个调用进行 0 或 2 个递归调用)。
如果 k 是奇数，让我们尝试从一个排序的排列开始，并尝试“取消排序”。让我们做一个函数 unsort(l，r)来实现它。当我们“取消排序”一个片段时，我们可以保持它的排序(如果我们已经进行了足够的调用)，或者使它不排序，然后调用取消排序(l，mid)和取消排序(mid，r)，如果我们需要更多的调用。当我们让一个片段不排序时，最好保持两半都排序；处理这个问题的一个简单方法是交换两个中间元素。
很容易看出 unsort 调用的数量等于 mergesort 调用的数量来对得到的排列进行排序，因此我们可以使用这种方法来尝试获得恰好 k 个调用。
以下是上述问题的代码。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to find an array that can be
// sorted with k merge sort calls.
#include <iostream>
using namespace std;

void unsort(int l, int r, int a[], int& k)
{
    if (k < 1 || l + 1 == r)
        return;

    // We make two recursive calls, so
    // reduce k by 2.
    k -= 2;

    int mid = (l + r) / 2;
    swap(a[mid - 1], a[mid]);
    unsort(l, mid, a, k);
    unsort(mid, r, a, k);
}

void arrayWithKCalls(int n, int k)
{
    if (k % 2 == 0) {
        cout << " NO SOLUTION ";
        return;
    }

    // Create an array with values
    // in [1, n]
    int a[n+1];
    a[0] = 1;
    for (int i = 1; i < n; i++)
        a[i] = i + 1;
    k--;

    // calling unsort function
    unsort(0, n, a, k);

    for (int i = 0; i < n; ++i)
        cout << a[i] << ' ';
}

// Driver code
int main()
{
    int n = 10, k = 17;
    arrayWithKCalls(n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find an array that can be
// sorted with k merge sort calls.
class GFG {

    static void unsort(int l, int r, int a[], int k)
    {

        if (k < 1 || l + 1 == r)
            return;

        // We make two recursive calls, so
        // reduce k by 2.
        k -= 2;

        int mid = (l + r) / 2;
        int temp = a[mid - 1];
        a[mid - 1] = a[mid];
        a[mid] = temp;

        unsort(l, mid, a, k);
        unsort(mid, r, a, k);
    }

    static void arrayWithKCalls(int n, int k)
    {
        if (k % 2 == 0) {
            System.out.print("NO SOLUTION");
            return;
        }

        // Create an array with values
        // in [1, n]
        int a[] = new int[n + 1];
        a[0] = 1;

        for (int i = 1; i < n; i++)
            a[i] = i + 1;
        k--;

        // calling unsort function
        unsort(0, n, a, k);

        for (int i = 0; i < n; ++i)
            System.out.print(a[i] + " ");
    }

    // Driver code
    public static void main(String[] args)
    {

        int n = 10, k = 17;

        arrayWithKCalls(n, k);
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python program to find
# an array that can be
# sorted with k merge
# sort calls.

def unsort(l,r,a,k):

    if (k < 1 or l + 1 == r):
        return

    # We make two recursive calls, so
    # reduce k by 2.
    k -= 2

    mid = (l + r) // 2
    temp = a[mid - 1]
    a[mid-1] = a[mid]
    a[mid] = temp

    unsort(l, mid, a, k)
    unsort(mid, r, a, k)

def arrayWithKCalls(n,k):

    if (k % 2 == 0):
        print("NO SOLUTION")
        return

    # Create an array with values
    # in [1, n]
    a = [0 for i in range(n + 2)]
    a[0] = 1
    for i in range(1, n):
        a[i] = i + 1
    k-=1

    # calling unsort function
    unsort(0, n, a, k)

    for i in range(n):
        print(a[i] ," ",end="")

# Driver code

n = 10
k = 17
arrayWithKCalls(n, k)

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to find an array that can
// be sorted with k merge sort calls.
using System;

class GFG {

    static void unsort(int l, int r,
                       int []a, int k)
    {
        if (k < 1 || l + 1 == r)
            return;

        // We make two recursive calls,
        // so reduce k by 2.
        k -= 2;

        int mid = (l + r) / 2;
        int temp = a[mid - 1];
        a[mid - 1] = a[mid];
        a[mid] = temp;

        unsort(l, mid, a, k);
        unsort(mid, r, a, k);
    }

    static void arrayWithKCalls(int n, int k)
    {
        if (k % 2 == 0)
        {
            Console.WriteLine("NO SOLUTION");
            return;
        }

        // Create an array with
        // values in [1, n]
        int []a = new int[n + 1];
        a[0] = 1;

        for (int i = 1; i < n; i++)
            a[i] = i + 1;
        k--;

        // calling unsort function
        unsort(0, n, a, k);

        for (int i = 0; i < n; ++i)
            Console.Write(a[i] + " ");
    }

    // Driver code
    public static void Main()
    {

        int n = 10, k = 17;

        arrayWithKCalls(n, k);
    }
}

// This code is contributed by vt_m.
```

## java 描述语言

```
<script>

// JavaScript program to find an array that can be
// sorted with k merge sort calls.

var k;

function unsort(l, r, a)
{
    if (k < 1 || l + 1 == r)
        return;

    // We make two recursive calls, so
    // reduce k by 2.
    k -= 2;

    var mid = parseInt((l + r) / 2);
    [a[mid - 1], a[mid]] = [a[mid], a[mid - 1]];
    unsort(l, mid, a);
    unsort(mid, r, a);
}

function arrayWithKCalls(n)
{
    if (k % 2 == 0) {
        document.write( " NO SOLUTION ");
        return;
    }

    // Create an array with values
    // in [1, n]
    var a = Array(n+1);
    a[0] = 1;
    for (var i = 1; i < n; i++)
        a[i] = i + 1;
    k--;

    // calling unsort function
    unsort(0, n, a);

    for (var i = 0; i < n; ++i)
        document.write( a[i] + ' ');
}

// Driver code
var n = 10
k = 17;
arrayWithKCalls(n);

</script>
```

**输出:**

```
3 1 4 6 2 8 5 9 7 10
```