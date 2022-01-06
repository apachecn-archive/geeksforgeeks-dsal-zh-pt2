# 二进制数组中要替换的最小 1 个数

> 原文:[https://www . geeksforgeeks . org/二进制数组中要替换的最小 1 个数/](https://www.geeksforgeeks.org/minimum-number-of-1s-to-be-replaced-in-a-binary-array/)

给定一个只有 0 和 1 的二进制数组 arr[]。任务是找到要被改变为零的最小数，如果数组中存在任何索引![i  ](img/da3a035c66100e6c313a80f2aa178eb3.png "Rendered by QuickLaTeX.com")，arr[i] = 0，那么 arr[i-1]和 arr[i+1]不应同时等于![1  ](img/2a68dc4b37180a096b26d1b1d3429eef.png "Rendered by QuickLaTeX.com")。
也就是说，对于任何指数![i  ](img/da3a035c66100e6c313a80f2aa178eb3.png "Rendered by QuickLaTeX.com")而言，以下条件都应该失败:

```
if (arr[i]== 0):
    (arr[i-1] == 1) && (arr[i+1] == 1)
```

**注**:数组考虑基于 1 的索引。
**示例** :

> **输入** : arr[] = { 1，1，0，1，1，0，1，0，1，0 }
> **输出** : 2
> **解释**:指数 2 和 7 或 4 和 7 可以变为零。
> **输入** : arr[] = { 1，1，0，0，0 }
> **输出** : 0

**方法:**想法是，每当我们发现像![arr[i-1] = 1 \;and\; arr[i] = 0 \;and \;arr[i+1] = 1  ](img/a0bd545d87605871480b52f754fe68fc.png "Rendered by QuickLaTeX.com")这样的情况时，我们简单地将第(i+1)个指数的值改为零(0)。所以第(i-1)和第(i+1)个指数之间的指数是安全的。
以下是上述办法的实施:

## C++

```
// C++ program to find minimum number
// of 1's  to be replaced to 0's
#include <bits/stdc++.h>
using namespace std;

// Function to find minimum number
// of 1's  to be replaced to 0's
int minChanges(int A[], int n)
{
    int cnt = 0;

    for (int i = 0; i < n - 2; ++i) {

        if ((i - 1 >= 0) && A[i - 1] == 1
            && A[i + 1] == 1 && A[i] == 0) {
            A[i + 1] = 0;
            cnt++;
        }

    }

    // return final answer
    return cnt;
}

// Driver program
int main()
{
    int A[] = { 1, 1, 0, 1, 1, 0, 1, 0, 1, 0 };
    int n = sizeof(A) / sizeof(A[0]);

    cout << minChanges(A, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum number
// of 1's to be replaced to 0's
import java.lang.*;
import java.util.*;

class GFG
{
// Function to find minimum number
// of 1's to be replaced to 0's
static int minChanges(int[] A, int n)
{
    int cnt = 0;

    for (int i = 0; i < n - 2; ++i)
    {

        if ((i - 1 >= 0) && A[i - 1] == 1 &&
                            A[i + 1] == 1 &&
                            A[i] == 0)
        {
            A[i + 1] = 0;
            cnt++;
        }

    }

    // return final answer
    return cnt;
}

// Driver Code
public static void main(String args[])
{
    int[] A = { 1, 1, 0, 1, 1, 0, 1, 0, 1, 0 };
    int n = A.length;

    System.out.print(minChanges(A, n));
}
}

// This code is contributed
// by Akanksha Rai
```

## 蟒蛇 3

```
# Python 3 program to find minimum
# number of 1's to be replaced to 0's

# Function to find minimum number
# of 1's to be replaced to 0's
def minChanges(A, n):
    cnt = 0
    for i in range(n - 2):
        if ((i - 1 >= 0) and A[i - 1] == 1 and
           A[i + 1] == 1 and A[i] == 0):
            A[i + 1] = 0
            cnt = cnt + 1

    # return final answer
    return cnt

# Driver Code
A = [1, 1, 0, 1, 1, 0, 1, 0, 1, 0]
n = len(A)
print(minChanges(A, n))

# This code is contributed
# by Shashank_Sharma
```

## C#

```
// C# program to find minimum number
// of 1's to be replaced to 0's
using System;

class GFG
{
// Function to find minimum number
// of 1's to be replaced to 0's
static int minChanges(int[] A, int n)
{
    int cnt = 0;

    for (int i = 0; i < n - 2; ++i)
    {

        if ((i - 1 >= 0) && A[i - 1] == 1 &&
                            A[i + 1] == 1 && A[i] == 0)
        {
            A[i + 1] = 0;
            cnt++;
        }

    }

    // return final answer
    return cnt;
}

// Driver Code
public static void Main()
{
    int[] A = { 1, 1, 0, 1, 1, 0, 1, 0, 1, 0 };
    int n = A.Length;

    Console.Write(minChanges(A, n));
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find minimum number
// of 1's to be replaced to 0's

// Function to find minimum number
// of 1's to be replaced to 0's
function minChanges($A, $n)
{
    $cnt = 0;

    for ($i = 0; $i < $n - 2; ++$i)
    {
        if (($i - 1 >= 0) && $A[$i - 1] == 1 &&
          $A[$i + 1] == 1 && $A[$i] == 0)
        {
            $A[$i + 1] = 0;
            $cnt++;
        }

    }

    // return final answer
    return $cnt;
}

// Driver Code
$A = array(1, 1, 0, 1, 1,
           0, 1, 0, 1, 0);
$n = sizeof($A);

echo minChanges($A, $n);

// This code is contributed
// by Ankita_Saini
?>
```

## java 描述语言

```
<script>

// Javascript program to find minimum number
// of 1's  to be replaced to 0's

// Function to find minimum number
// of 1's  to be replaced to 0's
function minChanges(A, n)
{
    var cnt = 0;

    for (var i = 0; i < n - 2; ++i) {

        if ((i - 1 >= 0) && A[i - 1] == 1
            && A[i + 1] == 1 && A[i] == 0) {
            A[i + 1] = 0;
            cnt++;
        }

    }

    // return final answer
    return cnt;
}

var A = [ 1, 1, 0, 1, 1, 0, 1, 0, 1, 0 ];
var n = A.length;
document.write(  minChanges(A, n));

// This code is contributed by SoumikMondal

</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(N)