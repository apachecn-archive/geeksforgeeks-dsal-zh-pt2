# 链对最大长度| DP-20

> 原文:[https://www . geesforgeks . org/最大长度成对链-dp-20/](https://www.geeksforgeeks.org/maximum-length-chain-of-pairs-dp-20/)

给你 n 对数字。在每对中，第一个数字总是小于第二个数字。一对(c，d)可以跟在另一对(a，b)之后如果 b < c. Chain of pairs can be formed in this fashion. Find the longest chain which can be formed from a given set of pairs. 
来源: [Amazon Interview | Set 2](https://www.geeksforgeeks.org/amazon-interview-set-2/)
例如，如果给定的对是{{5，24}、{39，60}、{15，28}、{27，40}、{50，90} }，那么可以形成的最长的链是长度 3，链是{{5，24}、{27，40}、{50，90}

这个问题是标准[最长递增子序列](https://www.geeksforgeeks.org/longest-increasing-subsequence-dp-3/)问题的变种。下面是一个简单的两步过程。
1)按照第一个(或更小的)元素的升序排列给定的对。为什么不需要排序？考虑示例{{6，8}，{3，4}}以了解排序的需要。如果我们继续第二步而不排序，我们得到的输出为 1。但是正确的输出是 2。
2)现在运行一个修改后的 LIS 流程，将已经完成的 LIS 的第二个元素与正在构建的新 LIS 的第一个元素进行比较。
以下代码是对本帖方法二的轻微修改。

## C++

```
// CPP program for above approach
#include <bits/stdc++.h>
using namespace std;

// Structure for a Pair
class Pair
{
    public:
    int a;
    int b;
};

// This function assumes that arr[]
// is sorted in increasing order
// according the first
// (or smaller) values in Pairs.
int maxChainLength( Pair arr[], int n)
{
    int i, j, max = 0;
    int *mcl = new int[sizeof( int ) * n ];

    /* Initialize MCL (max chain length)
    values for all indexes */
    for ( i = 0; i < n; i++ )
        mcl[i] = 1;

    /* Compute optimized chain
    length values in bottom up manner */
    for ( i = 1; i < n; i++ )
        for ( j = 0; j < i; j++ )
            if ( arr[i].a > arr[j].b &&
                    mcl[i] < mcl[j] + 1)
                mcl[i] = mcl[j] + 1;

    // mcl[i] now stores the maximum
    // chain length ending with Pair i

    /* Pick maximum of all MCL values */
    for ( i = 0; i < n; i++ )
        if ( max < mcl[i] )
            max = mcl[i];

    /* Free memory to avoid memory leak */

    return max;
}

/* Driver code */
int main()
{
    Pair arr[] = { {5, 24}, {15, 25},
                        {27, 40}, {50, 60} };
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << "Length of maximum size chain is "
                  << maxChainLength( arr, n );
    return 0;
}

// This code is contributed by rathbhupendra
```

## C

```
#include<stdio.h>
#include<stdlib.h>

// Structure for a pair
struct pair
{
  int a;
  int b;
};

// This function assumes that
// arr[] is sorted in increasing order
// according the first
// (or smaller) values in pairs.
int maxChainLength( struct pair arr[], int n)
{
   int i, j, max = 0;
   int *mcl = (int*) malloc ( sizeof( int ) * n );

   /* Initialize MCL (max chain
     length) values for all indexes */
   for ( i = 0; i < n; i++ )
      mcl[i] = 1;

   /* Compute optimized chain length
   values in bottom up manner */
   for ( i = 1; i < n; i++ )
      for ( j = 0; j < i; j++ )
         if ( arr[i].a > arr[j].b &&
                mcl[i] < mcl[j] + 1)
            mcl[i] = mcl[j] + 1;

   // mcl[i] now stores the maximum
   // chain length ending with pair i

   /* Pick maximum of all MCL values */
   for ( i = 0; i < n; i++ )
      if ( max < mcl[i] )
         max = mcl[i];

   /* Free memory to avoid memory leak */
   free( mcl );

   return max;
}

/* Driver program to test above function */
int main()
{
    struct pair arr[] = { {5, 24}, {15, 25},
                          {27, 40}, {50, 60} };
    int n = sizeof(arr)/sizeof(arr[0]);
    printf("Length of maximum size chain is %d\n",
           maxChainLength( arr, n ));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
class Pair
{
    int a;
    int b;

    public Pair(int a, int b)
    {
        this.a = a;
        this.b = b;
    }

    // This function assumes that
    // arr[] is sorted in increasing order
    // according the first (or smaller)
    // values in pairs.
    static int maxChainLength(Pair arr[], int n)
    {
       int i, j, max = 0;
       int mcl[] = new int[n];

       /* Initialize MCL (max chain length)
        values for all indexes */
       for ( i = 0; i < n; i++ )
          mcl[i] = 1;

       /* Compute optimized chain length
        values in bottom up manner */
       for ( i = 1; i < n; i++ )
          for ( j = 0; j < i; j++ )
             if ( arr[i].a > arr[j].b &&
                    mcl[i] < mcl[j] + 1)
                mcl[i] = mcl[j] + 1;

       // mcl[i] now stores the maximum
       // chain length ending with pair i

       /* Pick maximum of all MCL values */
       for ( i = 0; i < n; i++ )
          if ( max < mcl[i] )
             max = mcl[i];

       return max;
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        Pair arr[] = new Pair[]
        {
          new Pair(5,24),
          new Pair(15, 25),                     
          new Pair (27, 40),
          new Pair(50, 60)};
         System.out.println("Length of maximum
                               size chain is " +
                 maxChainLength(arr, arr.length));
    }
}
```

## 蟒蛇 3

```
# Python program for above approach
class Pair(object):
    def __init__(self, a, b):
        self.a = a
        self.b = b

# This function assumes
# that arr[] is sorted in increasing
# order according the
# first (or smaller) values in pairs.
def maxChainLength(arr, n):

    max = 0

    # Initialize MCL(max chain
    # length) values for all indices
    mcl = [1 for i in range(n)]

    # Compute optimized chain
    # length values in bottom up manner
    for i in range(1, n):
        for j in range(0, i):
            if (arr[i].a > arr[j].b and
                  mcl[i] < mcl[j] + 1):
                mcl[i] = mcl[j] + 1

    # mcl[i] now stores the maximum
    # chain length ending with pair i

    # Pick maximum of all MCL values
    for i in range(n):
        if (max < mcl[i]):
            max = mcl[i]

    return max

# Driver program to test above function
arr = [Pair(5, 24), Pair(15, 25),
       Pair(27, 40), Pair(50, 60)]

print('Length of maximum size chain is',
      maxChainLength(arr, len(arr)))

# This code is contributed by Soumen Ghosh
```

## C#

```
// Dynamic C# program to find
// Maximum Length Chain of Pairs
using System;

class Pair
{
    int a;
    int b;

    public Pair(int a, int b)
    {
        this.a = a;
        this.b = b;
    }

    // This function assumes that arr[]
    // is sorted in increasing order
    // according the first (or smaller)
    // values in pairs.
    static int maxChainLength(Pair []arr, int n)
    {
        int i, j, max = 0;
        int []mcl = new int[n];

        // Initialize MCL (max chain length)
        // values for all indexes
        for(i = 0; i < n; i++ )
            mcl[i] = 1;

        // Compute optimized chain length
        // values in bottom up manner
        for(i = 1; i < n; i++)
            for (j = 0; j < i; j++)
                if(arr[i].a > arr[j].b &&
                   mcl[i] < mcl[j] + 1)

          // mcl[i] now stores the maximum
          // chain length ending with pair i
          mcl[i] = mcl[j] + 1;

        // Pick maximum of all MCL values
        for ( i = 0; i < n; i++ )
            if (max < mcl[i] )
                max = mcl[i];

        return max;
    }

    // Driver Code
    public static void Main()
    {
        Pair []arr = new Pair[]
        {new Pair(5,24), new Pair(15, 25),
        new Pair (27, 40), new Pair(50, 60)};
        Console.Write("Length of maximum size
                                chain is " +
                 maxChainLength(arr, arr.Length));
    }
}

// This code is contributed by nitin mittal.
```

## java 描述语言

```
<script>

// Javascript program for above approach

class Pair
{
    constructor(a,b)
    {
        this.a=a;
        this.b=b;
    }
}

// This function assumes that
    // arr[] is sorted in increasing order
    // according the first (or smaller)
    // values in pairs.
function maxChainLength(arr,n)
{
    let i, j, max = 0;
       let mcl = new Array(n);

       /* Initialize MCL (max chain length)
        values for all indexes */
       for ( i = 0; i < n; i++ )
          mcl[i] = 1;

       /* Compute optimized chain length
        values in bottom up manner */
       for ( i = 1; i < n; i++ )
          for ( j = 0; j < i; j++ )
             if ( arr[i].a > arr[j].b &&
                    mcl[i] < mcl[j] + 1)
                mcl[i] = mcl[j] + 1;

       // mcl[i] now stores the maximum
       // chain length ending with pair i

       /* Pick maximum of all MCL values */
       for ( i = 0; i < n; i++ )
          if ( max < mcl[i] )
             max = mcl[i];

       return max;
}

/* Driver program to test above function */
let arr=[ new Pair(5,24),
          new Pair(15, 25),                    
          new Pair (27, 40),
          new Pair(50, 60)];

document.write("Length of maximum size chain is " +
                 maxChainLength(arr, arr.length));

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output**

```
Length of maximum size chain is 3
```

**时间复杂度:** O(n^2)其中 n 是对的数量。

给定的问题也是 [**活动选择问题**](https://www.geeksforgeeks.org/activity-selection-problem-greedy-algo-1/) 的变种，可以在(nLogn)时间内解决。要将其作为活动选择问题来解决，请将活动选择问题中的第一个元素视为开始时间，将第二个元素视为结束时间。

**另一种方法(自上而下的动态规划):**
现在我们将探索使用自上而下的动态规划方法 ***(*** 递归+记忆)来解决这个问题的方法。
既然我们要用自上而下的方法来解决上述问题，那么我们的第一步就是找出递归关系。获得递归关系的最好和最简单的方法是考虑我们在每个状态或位置的选择。
如果我们仔细看上面的问题，我们会发现每个位置/指数都有两个选择。两个选择是:
***选择 1:*** 选择特定位置的元素并探索其余部分，*(或)*
***选择 2:*** 将元素留在该位置并探索其余部分。
这里请注意，只有当特定位置的第一个元素大于我们之前选择的第二个元素时，我们才能选择该位置的元素(这是问题中给出的一个约束)。因此，在递归中，我们维护一个变量，它会告诉我们之前选择的元素。
同样，我们必须最大化我们的答案。因此，我们必须通过在每个位置探索上述两个选择来找出最大结果选项。
得到的递归关系为:

**T(n) = max( maxlenchain(p，n，p[pos])。第二，0)+1，maxlenchain(p，n，prev_choosen_ele，pos+1) )**
请注意函数签名如下:
int cal(struct val p[]，int n，int prev_choosen_ele，int pos)；

然而，我们不应该忘记递归中的基本条件。如果没有，我们的代码将享受一个假期，永远执行而不停止。
所以，我们这个问题的基础条件相当简单。如果我们到达探索的终点，我们只返回 0，因为不可能有更多的链。

**如果(位置> = n)返回 0；**

为了避免重复的任务，我们做了动态编程魔术(这是一个降低时间复杂度的魔术)。我们将位置和先前的元素存储在地图中。如果我们碰巧遇到相同的位置和相同的前一个元素，我们不再重新计算。我们只是从地图上返回答案。
下面是上述方法的实现:

## C++14

```
// CPP program for above approach
#include <bits/stdc++.h>
using namespace std;

// Structure val
struct val
{
    int first;
    int second;
};

map<pair<int, int>, int> m;

// Memoisation function
int findMaxChainLen(struct val p[], int n,
                        int prev, int pos)
{

    // Check if pair { pos, prev } exists
    // in m
    if (m.find({ pos, prev }) != m.end())
    {
        return m[{ pos, prev }];
    }

    // Check if pos is >=n
    if (pos >= n)
        return 0;

    // Check if p[pos].first is
    // less than prev
    if (p[pos].first <= prev)
    {
        return findMaxChainLen(p, n, prev,
                                 pos + 1);
    }

    else
    {
        int ans = max(findMaxChainLen(p, n,
                             p[pos].second, 0) + 1,
                      findMaxChainLen(p, n,
                                   prev, pos + 1));
        m[{ pos, prev }] = ans;
        return ans;
    }
}

// Function to calculate maximum
// chain length
int maxChainLen(struct val p[], int n)
{
    m.clear();

    // Call memoisation function
    int ans = findMaxChainLen(p, n, 0, 0);
    return ans;
}

// Driver Code
int main()
{

    int n = 5;
    val p[n];
    p[0].first = 5;
    p[0].second = 24;

    p[1].first = 39;
    p[1].second = 60;

    p[2].first = 15;
    p[2].second = 28;

    p[3].first = 27;
    p[3].second = 40;

    p[4].first = 50;
    p[4].second = 90;

    // Function Call
    cout << maxChainLen(p, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
import java.util.*;

class GFG{

// Structure val
static class val
{
    int first;
    int second;
};

static class pair
{
    int first, second;

    public pair(int first, int second) 
    {
        this.first = first;
        this.second = second;
    }

    @Override
    public int hashCode()
    {
        final int prime = 31;
        int result = 1;
        result = prime * result + first;
        result = prime * result + second;
        return result;
    }

    @Override
    public boolean equals(Object obj)
    {
        if (this == obj)
            return true;
        if (obj == null)
            return false;
        if (getClass() != obj.getClass())
            return false;

        pair other = (pair) obj;
        if (first != other.first)
            return false;
        if (second != other.second)
            return false;

        return true;
    }   

}

static Map<pair, Integer> m = new HashMap<>();

// Memoisation function
static int findMaxChainLen(val p[], int n,
                           int prev, int pos)
{

    // Check if pair { pos, prev } exists
    // in m
    if (m.containsKey(new pair(pos, prev)))
    {
        return m.get(new pair(pos, prev));
    }

    // Check if pos is >=n
    if (pos >= n)
        return 0;

    // Check if p[pos].first is
    // less than prev
    if (p[pos].first <= prev)
    {
        return findMaxChainLen(p, n, prev,
                               pos + 1);
    }

    else
    {
        int ans = Math.max(findMaxChainLen(
                               p, n, p[pos].second, 0) + 1,
                           findMaxChainLen(
                               p, n, prev, pos + 1));

        m.put(new pair(pos, prev), ans);
        return ans;
    }
}

// Function to calculate maximum
// chain length
static int maxChainLen(val p[], int n)
{
    m.clear();

    // Call memoisation function
    int ans = findMaxChainLen(p, n, 0, 0);
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int n = 5;
    val []p = new val[n];
    for(int i = 0; i < n; i++)
        p[i] = new val();

    p[0].first = 5;
    p[0].second = 24;

    p[1].first = 39;
    p[1].second = 60;

    p[2].first = 15;
    p[2].second = 28;

    p[3].first = 27;
    p[3].second = 40;

    p[4].first = 50;
    p[4].second = 90;

    // Function Call
    System.out.print(maxChainLen(p, n) + "\n");
}
}

// This code is contributed by 29AjayKumar
```

**Output**

```
3
```

https://www.youtube.com/watch?v=v

-hyperxpectqm 3q

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。