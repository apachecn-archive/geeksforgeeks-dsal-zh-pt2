# 最长公共扩展/ LCE |集合 1(引入和朴素方法)

> 原文:[https://www . geesforgeks . org/long-common-extension-lce-set-1-introduction-and-naive-method/](https://www.geeksforgeeks.org/longest-common-extension-lce-set-1-introduction-and-naive-method/)

最长公共扩展(LCE)问题考虑一个字符串 **s** ，并为每对(L，R)计算从 L 和 R 开始的 **s** 的最长子字符串。在 LCE，在每个查询中，我们必须回答从索引 L 和 R 开始的最长公共前缀的长度。
**示例:**
**字符串**:【阿巴巴巴】
**查询:** LCE(1，2)，LCE(1，6) 5)
找出从给定索引开始的最长公共前缀的长度， **(1，2)、(1，6)和(0，5)** 。
突出显示的字符串“绿色”是从相应查询的索引- L 和 R 开始的最长公共前缀。我们必须找到从索引- **(1，2)、(1，6)和(0，5)** 开始的最长公共前缀的长度。

![Longest Common Extension](img/939034d902777406075a4f62c0af1883.png)

**算法(天真法)**

1.  对于表格中的每个 LCE 查询，LCE(左，右)执行以下操作:
    *   将 LCE“长度”初始化为 0
    *   开始逐个字符地比较从索引- L 和 R 开始的前缀。
    *   如果字符匹配，那么这个字符在我们的最长公共扩展名中。所以递增‘长度’(length++)。
    *   否则，如果字符不匹配，则返回此“长度”。
2.  返回的“长度”将是所需的 LCE(左，右)。

**实现:**
下面是上面 Naive 算法的 C++实现。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// A C++ Program to find the length of longest
// common extension using Naive Method
#include<bits/stdc++.h>
using namespace std;

// Structure to represent a query of form (L,R)
struct Query
{
    int L, R;
};

// A utility function to find longest common
// extension from index - L and index - R
int LCE(string str, int n, int L, int R)
{
    int length = 0;

    while (str[L+length] == str[R+length] &&
            R+length < n)
        length++;

    return(length);
}

// A function to answer queries of longest
// common extension
void LCEQueries(string str, int n, Query q[],
                                       int m)
{
    for (int i=0; i<m; i++)
    {
        int L = q[i].L;
        int R = q[i].R;

        printf("LCE (%d, %d) = %d\n", L, R,
                         LCE(str, n, L, R));
    }
    return;
}

// Driver Program to test above functions
int main()
{
    string str = "abbababba";
    int n = str.length();

    // LCA Queries to answer
    Query q[] = {{1, 2}, {1, 6}, {0, 5}};
    int m = sizeof(q)/sizeof(q[0]);

    LCEQueries(str, n, q, m);

    return (0);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Java Program to find the length of longest
// common extension using Naive Method
import java.util.*;
class GFG
{

// Structure to represent a query of form (L,R)
static class Query
{
    int L, R;
    Query(int L, int R)
    {
        this.L = L;
        this.R = R;
    }
};

// A utility function to find longest common
// extension from index - L and index - R
static int LCE(String str, int n, int L, int R)
{
    int length = 0;
    while ( R + length < n && str.charAt(L + length) == str.charAt(R + length))
        length++;
    return(length);
}

// A function to answer queries of longest
// common extension
static void LCEQueries(String str, int n, Query q[],
                                       int m)
{
    for (int i = 0; i < m; i++)
    {
        int L = q[i].L;
        int R = q[i].R;
        System.out.printf("LCE (%d, %d) = %d\n", L, R,
                         LCE(str, n, L, R));
    }
    return;
}

// Driver code
public static void main(String[] args)
{
    String str = "abbababba";
    int n = str.length();

    // LCA Queries to answer
    Query q[] = new Query[3];
    q[0] = new Query(1, 2);
    q[1] = new Query(1, 6);
    q[2] = new Query (0, 5);
    int m = q.length;
    LCEQueries(str, n, q, m);
}
}

// This code is contributed by gauravrajput1
```

## C#

```
// A C# Program to find the length of longest
// common extension using Naive Method
using System;
public class GFG
{

  // Structure to represent a query of form (L,R)
  public
    class Query
    {
      public
        int L, R;
      public
        Query(int L, int R)
      {
        this.L = L;
        this.R = R;
      }
    };

  // A utility function to find longest common
  // extension from index - L and index - R
  static int LCE(String str, int n, int L, int R)
  {
    int length = 0;
    while ( R + length < n && str[L + length] == str[R + length])
      length++;
    return(length);
  }

  // A function to answer queries of longest
  // common extension
  static void LCEQueries(String str, int n, Query []q,
                         int m)
  {
    for (int i = 0; i < m; i++)
    {
      int L = q[i].L;
      int R = q[i].R;
      Console.WriteLine("LCE (" + L + ", " + R +
                        ") = " + LCE(str, n, L, R));
    }
    return;
  }

  // Driver code
  public static void Main(String[] args)
  {
    String str = "abbababba";
    int n = str.Length;

    // LCA Queries to answer
    Query []q = new Query[3];
    q[0] = new Query(1, 2);
    q[1] = new Query(1, 6);
    q[2] = new Query (0, 5);
    int m = q.Length;
    LCEQueries(str, n, q, m);
  }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// A Javascript Program to find the length of longest
// common extension using Naive Method

// Structure to represent a query of form (L,R)
class Query
{
    constructor(L,R)
    {
        this.L = L;
        this.R = R;
    }
}

// A utility function to find longest common
// extension from index - L and index - R
function LCE(str,n,L,R)
{
    let length = 0;
    while ( R + length < n && str[L + length] == str[R + length])
        length++;
    return(length);
}

// A function to answer queries of longest
// common extension
function LCEQueries(str,n,q,m)
{
    for (let i = 0; i < m; i++)
    {
        let L = q[i].L;
        let R = q[i].R;
        document.write("LCE ("+L+", "+R+") = "+LCE(str, n, L, R)+"<br>");
    }
    return;
}

// Driver code
let  str = "abbababba";
let n = str.length;

// LCA Queries to answer
let q = new Array(3);
q[0] = new Query(1, 2);
q[1] = new Query(1, 6);
q[2] = new Query (0, 5);
let m = q.length;
LCEQueries(str, n, q, m);

// This code is contributed by unknown2108
</script>
```

输出:

```
LCE(1, 2) = 1
LCE(1, 6) = 3
LCE(0, 5) = 4
```

**朴素方法的分析**
时间复杂度:时间复杂度为 O(Q.N)，其中
**Q**= LCE 查询数
**N** =输入字符串长度
人们可能会惊讶，虽然具有更大的渐近时间复杂度，但朴素方法在实际应用中优于其他高效方法(渐近)。我们将在接下来的几集里讨论这个话题。
辅助空间:O(1)，原地算法。
**应用:**

1.  k-错配问题->朗道-维什金用 LCE 作为子程序解决 k-错配问题
2.  近似字符串搜索。
3.  带通配符的回文匹配。
4.  差分全球比对。

在接下来的内容中，我们将讨论如何将 LCE(最长公共扩展)问题简化为 RMQ(范围最小查询)。我们还将讨论寻找最长公共扩展的更有效的方法。
**参考:**

*   [http://www . science direct . com/science/article/pii/s 1570866710000377](http://www.sciencedirect.com/science/article/pii/S1570866710000377)

本文由**拉希特·贝尔瓦亚尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。