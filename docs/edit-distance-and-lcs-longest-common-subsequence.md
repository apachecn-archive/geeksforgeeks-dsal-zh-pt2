# 编辑距离和 LCS(最长公共子序列)

> 原文:[https://www . geesforgeks . org/edit-distance-and-LCS-最长-公共-子序列/](https://www.geeksforgeeks.org/edit-distance-and-lcs-longest-common-subsequence/)

在标准的编辑距离中，我们可以进行 3 个操作，插入、删除和替换。考虑一个编辑距离的变化，其中我们只允许两个操作插入和删除，在这个变化中找到编辑距离。

**示例:**

```
Input : str1 = "cat", st2 = "cut"
Output : 2
We are allowed to insert and delete. We delete 'a'
from "cat" and insert "u" to make it "cut".

Input : str1 = "acb", st2 = "ab"
Output : 1
We can convert "acb" to "ab" by removing 'c'. 
```

一种解决方案是通过进行两次递归调用而不是三次来简单修改[编辑距离](https://www.geeksforgeeks.org/dynamic-programming-set-5-edit-distance/)解决方案。一个有趣的解决方案基于 LCS。
1)找到两线 LCS。让 LCS 的长度为 **x** 。
2)让第一根弦的长度为 **m** ，第二根弦的长度为 **n** 。我们的结果是(m–x)+(n–x)。我们基本上需要做(m–x)个删除操作和(n–x)个插入操作。

## C++

```
// CPP program to find Edit Distance (when only two
// operations are allowed, insert and delete) using LCS.
#include<bits/stdc++.h>
using namespace std;

int editDistanceWith2Ops(string &X, string &Y)
{
    // Find LCS
    int m = X.length(), n = Y.length();
    int L[m+1][n+1];
    for (int i=0; i<=m; i++)
    {
        for (int j=0; j<=n; j++)
        {
            if (i == 0 || j == 0)
                L[i][j] = 0;
            else if (X[i-1] == Y[j-1])
                L[i][j] = L[i-1][j-1] + 1;
            else
                L[i][j] = max(L[i-1][j], L[i][j-1]);
        }
    }   
    int lcs  = L[m][n];

    // Edit distance is delete operations +
    // insert operations.
    return (m - lcs) + (n - lcs);
}

/* Driver program to test above function */
int main()
{
    string X = "abc", Y = "acd";
    cout << editDistanceWith2Ops(X, Y);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java program to find Edit Distance (when only two
// operations are allowed, insert and delete) using LCS.

class GFG {

    static int editDistanceWith2Ops(String X, String Y) {
        // Find LCS
        int m = X.length(), n = Y.length();
        int L[][] = new int[m + 1][n + 1];
        for (int i = 0; i <= m; i++) {
            for (int j = 0; j <= n; j++) {
                if (i == 0 || j == 0) {
                    L[i][j] = 0;
                } else if (X.charAt(i - 1) == Y.charAt(j - 1)) {
                    L[i][j] = L[i - 1][j - 1] + 1;
                } else {
                    L[i][j] = Math.max(L[i - 1][j], L[i][j - 1]);
                }
            }
        }
        int lcs = L[m][n];

        // Edit distance is delete operations +
        // insert operations.
        return (m - lcs) + (n - lcs);
    }

    /* Driver program to test above function */
    public static void main(String[] args) {
        String X = "abc", Y = "acd";
        System.out.println(editDistanceWith2Ops(X, Y));

    }
}
/* This Java code is contributed by 29AjayKumar*/
```

## 蟒蛇 3

```
# Python 3 program to find Edit Distance
# (when only two operations are allowed,
# insert and delete) using LCS.

def editDistanceWith2Ops(X, Y):

    # Find LCS
    m = len(X)
    n = len(Y)
    L = [[0 for x in range(n + 1)]
            for y in range(m + 1)]
    for i in range(m + 1):
        for j in range(n + 1):
            if (i == 0 or j == 0):
                L[i][j] = 0
            elif (X[i - 1] == Y[j - 1]):
                L[i][j] = L[i - 1][j - 1] + 1
            else:
                L[i][j] = max(L[i - 1][j],
                              L[i][j - 1])

    lcs = L[m][n]

    # Edit distance is delete operations +
    # insert operations.
    return (m - lcs) + (n - lcs)

# Driver Code
if __name__ == "__main__":

    X = "abc"
    Y = "acd"
    print(editDistanceWith2Ops(X, Y))

# This code is contributed by ita_c
```

## C#

```
// C# program to find Edit Distance
// (when only two operations are
// allowed, insert and delete) using LCS.
using System;

class GFG
{

static int editDistanceWith2Ops(String X,
                                String Y)
{
    // Find LCS
    int m = X.Length, n = Y.Length;
    int [ , ]L = new int[m + 1 , n + 1];
    for (int i = 0; i <= m; i++)
    {
        for (int j = 0; j <= n; j++)
        {
            if (i == 0 || j == 0)
            {
                L[i , j] = 0;
            }
            else if (X[i - 1] == Y[j - 1])
            {
                L[i , j] = L[i - 1 , j - 1] + 1;
            }
            else
            {
                L[i , j] = Math.Max(L[i - 1 , j],
                                    L[i , j - 1]);
            }
        }
    }
    int lcs = L[m , n];

    // Edit distance is delete operations +
    // insert operations.
    return (m - lcs) + (n - lcs);
}

// Driver Code
public static void Main()
{
    String X = "abc", Y = "acd";
    Console.Write(editDistanceWith2Ops(X, Y));
}
}

// This code is contributed
// by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find Edit Distance
// (when only two operations are allowed,
// insert and delete) using LCS.

function editDistanceWith2Ops($X, $Y)
{
    // Find LCS
    $m = strlen($X); $n = strlen($Y);
    $L[$m + 1][$n + 1];
    for ($i = 0; $i <= $m; $i++)
    {
        for ($j = 0; $j <= $n; $j++)
        {
            if ($i == 0 || $j == 0)
                $L[$i][$j] = 0;
            else if ($X[$i - 1] == $Y[$j - 1])
                $L[$i][$j] = $L[$i - 1][$j - 1] + 1;
            else
                $L[$i][$j] = max($L[$i - 1][$j],
                                 $L[$i][$j - 1]);
        }
    }
    $lcs = $L[$m][$n];

    // Edit distance is delete operations +
    // insert operations.
    return ($m - $lcs) + ($n - $lcs);
}

// Driver Code
$X = "abc"; $Y = "acd";
echo editDistanceWith2Ops($X, $Y);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>
//Javascript program to find Edit Distance (when only two
// operations are allowed, insert and delete) using LCS.

    function editDistanceWith2Ops(X,Y)
    {
        // Find LCS
        let m = X.length, n = Y.length;
        let L = new Array(m + 1);
        for(let i=0;i<L.length;i++)
        {
            L[i]=new Array(n+1);
            for(let j=0;j<L[i].length;j++)
            {
                L[i][j]=0;
            }
        }
        for (let i = 0; i <= m; i++) {
            for (let j = 0; j <= n; j++) {
                if (i == 0 || j == 0) {
                    L[i][j] = 0;
                } else if (X[i-1] == Y[j-1]) {
                    L[i][j] = L[i - 1][j - 1] + 1;
                } else {
                    L[i][j] = Math.max(L[i - 1][j], L[i][j - 1]);
                }
            }
        }
        let lcs = L[m][n];

        // Edit distance is delete operations +
        // insert operations.
        return (m - lcs) + (n - lcs);
    }

    /* Driver program to test above function */
    let X = "abc", Y = "acd";
    document.write(editDistanceWith2Ops(X, Y));

// This code is contributed by rag2127
</script>
```

**输出:**

```
2
```

**时间复杂度:**O(m * n)
T3】辅助空间: O(m * n)