# 通过给定操作改变位置所需的最小移动量

> 原文:[https://www . geeksforgeeks . org/通过给定操作改变位置所需的最小移动量/](https://www.geeksforgeeks.org/minimum-moves-required-to-change-position-with-the-given-operation/)

给定两个整数 **S** 和 **T** 以及一个数组 **arr** ，该数组包含从 **1** 到 **N** 的元素，这些元素以未排序的方式存在。任务是通过以下操作找到将 **Sth** 元素移动到数组中 **Tth** 位置的最小移动次数:
单次移动包括以下

```
// Initially b[] = {1, 2, 3, ..., N}
// arr[] is input array
for (i = 1..n)
   temp[arr[i]] = b[i]
b = temp
```

如果不可能，则打印 **-1** 。
**例:**

> **输入:** S = 2，T = 1，arr[] = {2，3，4，1}
> **输出:** 3
> N 为 4(arr[])
> 移动 1: b[] = {4，1，2，3}
> 移动 2: b[] = {3，4，1，2}
> 移动 3: b[] = {2，3，4，1}
> **输入:** S = 3，T = 4

**进场:**这里重要的观察是我们只关心单个元素的位置，而不是整个数组。因此，每次移动时，我们将位置 **S** 处的元素移动到位置**arr【S】**，直到我们到达 **Tth** 位置。
由于我们最多只能到达 **N** 个不同的地方，如果我们在 **N** 个动作中没有到达 **T** ，那就意味着我们永远无法到达。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the number of moves
int minimumMoves(int n, int a[], int s, int t)
{
    int i, x;
    x = s;
    for (i = 1; i <= n; i++) {
        if (x == t)
            break;
        x = a[x];
    }

    // Destination reached
    if (x == t)
        return i - 1;
    else
        return -1;
}

// Driver Code
int main()
{
    int s = 2, t = 1, i;
    int a[] = {-1, 2, 3, 4, 1};
    int n = sizeof(a) / sizeof(a[0]);
    cout << minimumMoves(n, a, s, t);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
public class GFG{

// Function to return the number of moves
static int minimumMoves(int n, int a[], int s, int t)
{
    int i, x;
    x = s;
    for (i = 1; i <= n; i++) {
        if (x == t)
            break;
        x = a[x];
    }

    // Destination reached
    if (x == t)
        return i - 1;
    else
        return -1;
}

    // Driver Code
    public static void main(String []args){
    int s = 2, t = 1, i;
    int a[] = {-1, 2, 3, 4, 1};
    int n = a.length ;
    System.out.println(minimumMoves(n, a, s, t)); 
    }
    // This code is contributed by Ryuga
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the number of moves
def minimumMoves(n, a, s, t):

    x = s
    for i in range(1, n+1): 
        # Destination reached
        if x == t:
            return i-1
        x = a[x]

    return -1

# Driver Code
if __name__ == "__main__":

    s, t = 2, 1
    a = [-1, 2, 3, 4, 1]
    n = len(a)
    print(minimumMoves(n, a, s, t))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the approach
using System;
public class GFG{

// Function to return the number of moves
static int minimumMoves(int n, int []a, int s, int t)
{
    int i, x;
    x = s;
    for (i = 1; i <= n; i++) {
        if (x == t)
            break;
        x = a[x];
    }

    // Destination reached
    if (x == t)
        return i - 1;
    else
        return -1;
}

    // Driver Code
    public static void Main(){
    int s = 2, t = 1;
    int []a = {-1, 2, 3, 4, 1};
    int n = a.Length ;
    Console.WriteLine(minimumMoves(n, a, s, t));
    }
    // This code is contributed by inder_verma.
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the number of moves
function minimumMoves($n, $a, $s, $t)
{
    $i; $x;
    $x = $s;
    for ($i = 1; $i <= $n; $i++) {
        if ($x == $t)
            break;
        $x = $a[$x];
    }

    // Destination reached
    if ($x == $t)
        return $i - 1;
    else
        return -1;
}

// Driver Code

    $s = 2; $t = 1; $i;
    $a = array(-1, 2, 3, 4, 1);
    $n = count($a);
    echo minimumMoves($n, $a, $s, $t);
     // This code is contributed by inder_verma.
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach  

    // Function to return the number of moves
    function minimumMoves(n, a, s, t)
    {
        let i, x;
        x = s;
        for (i = 1; i <= n; i++) {
            if (x == t)
                break;
            x = a[x];
        }

        // Destination reached
        if (x == t)
            return i - 1;
        else
            return -1;
    }

    let s = 2, t = 1;
    let a = [-1, 2, 3, 4, 1];
    let n = a.length ;
    document.write(minimumMoves(n, a, s, t));

     // This code is contributed by suresh07.
</script>
```

**Output:** 

```
3
```