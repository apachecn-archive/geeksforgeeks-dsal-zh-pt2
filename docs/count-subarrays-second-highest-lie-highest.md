# 统计第二高位于最高之前的子阵列

> 原文:[https://www . geesforgeks . org/count-subarrays-第二高-lie-high/](https://www.geeksforgeeks.org/count-subarrays-second-highest-lie-highest/)

给定至少大小为 2 的不同元素的数组。数组中的一对(a，b)定义为“a”是第二高元素的索引，“b”是数组中最高元素的索引。任务是计算所有子阵列中 a < b 所在的所有不同对。

**示例:**

```
Input : arr[] = { 1, 3, 2, 4 }
Output : 3
```

**说明:**
子阵列{ 1 }、{ 3 }、{ 2 }、{ 4 }不包含任何这样的对
子阵列{ 1，3 }、{ 2，4 }包含(1，2)作为对
子阵列{ 3，2 }不包含任何这样的对
子阵列{ 3，2，4 }包含(1，3)作为对
子阵列{ 1，3， 2 }不包含任何这样的对
子阵列{ 1，3，2，4 }包含(2，4)作为一对
因此，有 3 个不同的对，它们是(1，2)、(1，3)和(2，4)。

**方法 1:(蛮力)–**简单的做法可以，
1。找到所有的子阵列。
2。对于每个子阵列，找到第二大和最大的元素。
3。检查第二大元素是否位于最大元素之前。
4。如果是，检查这样的索引对是否已经被计数。如果不存储该对并将计数增加 1，则忽略。
**时间复杂度:** O(n <sup>2</sup> )。

**方法 2:(使用堆栈)–**
对于给定的数组 A，假设对于索引 *curr* (A[curr])处的元素，大于它的第一个元素是 A[next]，大于它的第一个元素是 A[prev]。请注意，对于从范围[prev + 1，curr]中的任何索引开始到下一个索引结束的所有子阵列，A[curr]是第二大的，A[next]是最大的，它们总共生成(curr–prev+1)对，最大值和第二大值之间的差值为(next–curr+1)。

如果我们在一个数组中得到下一个和上一个更大的元素，并记录任何差异(最大和第二大的)可能的最大对数。我们需要把这些数字加起来。

现在唯一剩下的工作就是获得更大的元素(在任何元素之前和之后)。为此，请参考[下一个更大的元素](https://www.geeksforgeeks.org/next-greater-element/)。
从数组中的起始元素开始遍历，按降序跟踪堆栈中的所有数字。到达任意数字后，从堆栈中弹出小于当前元素的所有元素，以获得大于它的数字的位置，并将当前元素推送到其上。这将为数组中的所有数字生成所需的值。

## C++

```
// C++ program to count number of distinct instance
// where second highest number lie
// before highest number in all subarrays.
#include <bits/stdc++.h>
#define MAXN 100005
using namespace std;

// Finding the next greater element of the array.
void makeNext(int arr[], int n, int nextBig[])
{
    stack<pair<int, int> > s;

    for (int i = n - 1; i >= 0; i--) {

        nextBig[i] = i;
        while (!s.empty() && s.top().first < arr[i])
            s.pop();

        if (!s.empty())
            nextBig[i] = s.top().second;

        s.push(pair<int, int>(arr[i], i));
    }
}

// Finding the previous greater element of the array.
void makePrev(int arr[], int n, int prevBig[])
{
    stack<pair<int, int> > s;
    for (int i = 0; i < n; i++) {

        prevBig[i] = -1;
        while (!s.empty() && s.top().first < arr[i])
            s.pop();

        if (!s.empty())
            prevBig[i] = s.top().second;

        s.push(pair<int, int>(arr[i], i));
    }
}

// Wrapper Function
int wrapper(int arr[], int n)
{
    int nextBig[MAXN];
    int prevBig[MAXN];
    int maxi[MAXN];
    int ans = 0;

    // Finding previous largest element
    makePrev(arr, n, prevBig);

    // Finding next largest element
    makeNext(arr, n, nextBig);

    for (int i = 0; i < n; i++)
        if (nextBig[i] != i)
            maxi[nextBig[i] - i] = max(maxi[nextBig[i] - i],
                                       i - prevBig[i]);

    for (int i = 0; i < n; i++)
        ans += maxi[i];

    return ans;
}

// Driven Program
int main()
{
    int arr[] = { 1, 3, 2, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << wrapper(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of distinct instance
// where second highest number lie
// before highest number in all subarrays.
import java.util.*;

class GFG
{

static int MAXN = 100005;

static class pair
{
    int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}
// Finding the next greater element of the array.
static void makeNext(int arr[], int n, int nextBig[])
{
    Stack<pair> s = new Stack<>();

    for (int i = n - 1; i >= 0; i--)
    {

        nextBig[i] = i;
        while (!s.empty() && s.peek().first < arr[i])
            s.pop();

        if (!s.empty())
            nextBig[i] = s.peek().second;

        s.push(new pair(arr[i], i));
    }
}

// Finding the previous greater element of the array.
static void makePrev(int arr[], int n, int prevBig[])
{
    Stack<pair> s = new Stack<>();
    for (int i = 0; i < n; i++)
    {

        prevBig[i] = -1;
        while (!s.empty() && s.peek().first < arr[i])
            s.pop();

        if (!s.empty())
            prevBig[i] = s.peek().second;

        s.push(new pair(arr[i], i));
    }
}

// Wrapper Function
static int wrapper(int arr[], int n)
{
    int []nextBig = new int[MAXN];
    int []prevBig = new int[MAXN];
    int []maxi = new int[MAXN];
    int ans = 0;

    // Finding previous largest element
    makePrev(arr, n, prevBig);

    // Finding next largest element
    makeNext(arr, n, nextBig);

    for (int i = 0; i < n; i++)
        if (nextBig[i] != i)
            maxi[nextBig[i] - i] = Math.max(maxi[nextBig[i] - i],
                                    i - prevBig[i]);

    for (int i = 0; i < n; i++)
        ans += maxi[i];

    return ans;
}

// Driver code
public static void main(String[] args)
{

    int arr[] = { 1, 3, 2, 4 };
    int n = arr.length;

    System.out.println(wrapper(arr, n));
    }
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program to count number of distinct
# instance where second highest number lie
# before highest number in all subarrays.
from typing import List

MAXN = 100005

# Finding the next greater element
# of the array.
def makeNext(arr: List[int], n: int,
         nextBig: List[int]) -> None:

    # Stack
    s = []

    for i in range(n - 1, -1, -1):
        nextBig[i] = i

        while len(s) and s[-1][0] < arr[i]:
            s.pop()

        if len(s):
            nextBig[i] = s[-1][1]

        s.append((arr[i], i))

# Finding the previous greater
# element of the array.
def makePrev(arr: List[int], n: int,
         prevBig: List[int]) -> None:

    # Stack
    s = []
    for i in range(n):
        prevBig[i] = -1

        while (len(s) and s[-1][0] < arr[i]):
            s.pop()

        if (len(s)):
            prevBig[i] = s[-1][1]

        s.append((arr[i], i))

# Wrapper Function
def wrapper(arr: List[int], n: int) -> int:

    nextBig = [0] * MAXN
    prevBig = [0] * MAXN
    maxi = [0] * MAXN
    ans = 0

    # Finding previous largest element
    makePrev(arr, n, prevBig)

    # Finding next largest element
    makeNext(arr, n, nextBig)

    for i in range(n):
        if (nextBig[i] != i):
            maxi[nextBig[i] - i] = max(
                maxi[nextBig[i] - i],
                    i - prevBig[i])

    for i in range(n):
        ans += maxi[i]

    return ans

# Driver Code
if __name__ == "__main__":

    arr = [ 1, 3, 2, 4 ]
    n = len(arr)

    print(wrapper(arr, n))

# This code is contributed by sanjeev2552
```

## C#

```
// C# program to count number of distinct instance
// where second highest number lie
// before highest number in all subarrays.
using System;
using System.Collections.Generic;

class GFG
{

static int MAXN = 100005;
public class pair
{
    public int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Finding the next greater element of the array.
static void makeNext(int []arr, int n, int []nextBig)
{
    Stack<pair> s = new Stack<pair>();

    for (int i = n - 1; i >= 0; i--)
    {

        nextBig[i] = i;
        while (s.Count!=0 && s.Peek().first < arr[i])
            s.Pop();

        if (s.Count!=0)
            nextBig[i] = s.Peek().second;

        s.Push(new pair(arr[i], i));
    }
}

// Finding the previous greater element of the array.
static void makePrev(int []arr, int n, int[] prevBig)
{
    Stack<pair> s = new Stack<pair>();
    for (int i = 0; i < n; i++)
    {

        prevBig[i] = -1;
        while (s.Count!=0 && s.Peek().first < arr[i])
            s.Pop();

        if (s.Count!=0)
            prevBig[i] = s.Peek().second;

        s.Push(new pair(arr[i], i));
    }
}

// Wrapper Function
static int wrapper(int []arr, int n)
{
    int []nextBig = new int[MAXN];
    int []prevBig = new int[MAXN];
    int []maxi = new int[MAXN];
    int ans = 0;

    // Finding previous largest element
    makePrev(arr, n, prevBig);

    // Finding next largest element
    makeNext(arr, n, nextBig);

    for (int i = 0; i < n; i++)
        if (nextBig[i] != i)
            maxi[nextBig[i] - i] = Math.Max(maxi[nextBig[i] - i],
                                    i - prevBig[i]);

    for (int i = 0; i < n; i++)
        ans += maxi[i];

    return ans;
}

// Driver code
public static void Main(String[] args)
{

    int[] arr = { 1, 3, 2, 4 };
    int n = arr.Length;

    Console.WriteLine(wrapper(arr, n));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to count number of distinct instance
// where second highest number lie
// before highest number in all subarrays.
var MAXN = 100005;

// Finding the next greater element of the array.
function makeNext(arr, n, nextBig)
{
    var s = [];

    for (var i = n - 1; i >= 0; i--) {

        nextBig[i] = i;
        while (s.length!=0 && s[s.length-1][0] < arr[i])
            s.pop();

        if (s.length!=0)
            nextBig[i] = s[s.length-1][1];

        s.push([arr[i], i]);
    }
}

// Finding the previous greater element of the array.
function makePrev(arr, n, prevBig)
{
    var s = [];
    for (var i = 0; i < n; i++) {

        prevBig[i] = -1;
        while (s.length!=0 && s[s.length-1][0] < arr[i])
            s.pop();

        if (s.length!=0)
            prevBig[i] = s[s.length-1][1];

        s.push([arr[i], i]);
    }
}

// Wrapper Function
function wrapper( arr, n)
{
    var nextBig = Array(MAXN).fill(0);
    var prevBig= Array(MAXN).fill(0);
    var maxi= Array(MAXN).fill(0);
    var ans = 0;

    // Finding previous largest element
    makePrev(arr, n, prevBig);

    // Finding next largest element
    makeNext(arr, n, nextBig);

    for (var i = 0; i < n; i++)
        if (nextBig[i] != i)
            maxi[nextBig[i] - i] = Math.max(maxi[nextBig[i] - i],
                                       i - prevBig[i]);

    for (var i = 0; i < n; i++)
        ans += maxi[i];

    return ans;
}

// Driven Program

var arr = [1, 3, 2, 4];
var n = arr.length;
document.write( wrapper(arr, n));

</script>
```

**输出:**

```
3
```

**时间复杂度:** O(n)

本文由 **anuj0503** 供稿。如果你喜欢极客博客并想投稿，你也可以用 contribute.geekforgeeks.org 写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。