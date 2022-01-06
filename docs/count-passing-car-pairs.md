# 统计过往车辆对

> 原文:[https://www.geeksforgeeks.org/count-passing-car-pairs/](https://www.geeksforgeeks.org/count-passing-car-pairs/)

给出了一个由大小为 N 的非空二进制数组 A，其中，

```
0 represents a car traveling east,
1 represents a car traveling west. 
```

目标是统计过往车辆。我们说一对车(P，Q)，其中 0 <= P < Q < N, is passing when P is traveling to the east and Q is traveling to the west.
**例:**

```
Input  : arr[] = {0, 1, 0, 1, 1}
Output : 5
The 5 pairs are (A[0], A[1]), (A[0], A[3]), (A[0], A[4]),   
(A[2], A[3]) and (A[2], A[4]). Note that in all pairs
first element is 0, second element is 1 and index of
first element is smaller than index of second element.

Input  : arr[] = {1, 0, 0, 0, 1}
Output : 3

Input : arr[] = {0, 0, 1, 0, 0}
Output : 2
```

一个**简单的解决方案**是使用两个嵌套循环。外部循环搜索 0，内部循环在 0 之后计数 1。最后，我们返回总计数。

## C++

```
// Simple C++ program to count passing cars
#include<bits/stdc++.h>
using namespace std;

// Returns count of passing cars
int getPassingCars(int A[], int n)
{
    int result = 0;
    for (int i=0; i<n-1; i++)
    {
       if (A[i] == 0)
       {
           for (int j=i+1; j<n; j++) 
              if (A[j])
                 result++;
       }
    }
    return result;
}

// Driver program
int main()
{
    int A[] = {0, 1, 0, 1, 1};
    int n = sizeof(A)/sizeof(A[0]);
    cout << getPassingCars(A, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Simple Java program to count passing cars
class GFG
{

// Returns count of passing cars
static int getPassingCars(int[] A, int n)
{
    int result = 0;
    for (int i = 0; i < n - 1; i++)
    {
    if (A[i] == 0)
    {
        for (int j = i + 1; j < n; j++)
            if (A[j] == 1)
                result++;
    }
    }
    return result;
}

// Driver Code
public static void main(String[] args)
{
    int[] A = {0, 1, 0, 1, 1};
    int n = A.length;
    System.out.println(getPassingCars(A, n));
}
}

// This code is contributed
// by Code_Mech
```

## 蟒蛇 3

```
# Simple Python 3 program to
# count passing cars

# Returns count of passing cars
def getPassingCars(A, n):
    result = 0
    for i in range(0, n - 1, 1):
        if (A[i] == 0):
            for j in range(i + 1, n, 1):
                if (A[j]):
                    result += 1

    return result

# Driver Code
if __name__ == '__main__':
    A = [0, 1, 0, 1, 1]
    n = len(A)
    print(getPassingCars(A, n))

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// Simple C# program to count passing cars
using System;

class GFG
{

// Returns count of passing cars
static int getPassingCars(int[] A, int n)
{
    int result = 0;
    for (int i = 0; i < n - 1; i++)
    {
    if (A[i] == 0)
    {
        for (int j = i + 1; j < n; j++)
            if (A[j] == 1)
                result++;
    }
    }
    return result;
}

// Driver Code
public static void Main()
{
    int[] A = {0, 1, 0, 1, 1};
    int n = A.Length;
    Console.WriteLine(getPassingCars(A, n));
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Simple PHP program to count passing cars

// Returns count of passing cars
function getPassingCars($A, $n)
{
    $result = 0;
    for ($i = 0; $i < $n - 1; $i++)
    {
        if ($A[$i] == 0)
        {
            for ($j = $i + 1; $j < $n; $j++)
                if ($A[$j])
                    $result++;
        }
    }
    return $result;
}

    // Driver Code
    $A = array(0, 1, 0, 1, 1);
    $n = sizeof($A);
    echo getPassingCars($A, $n);

// This code is contributed by m_kit
?>
```

## java 描述语言

```
<script>

    // Simple Javascript program
    // to count passing cars

    // Returns count of passing cars
    function getPassingCars(A, n)
    {
        let result = 0;
        for (let i = 0; i < n - 1; i++)
        {
          if (A[i] == 0)
          {
              for (let j = i + 1; j < n; j++)
                  if (A[j] == 1)
                      result++;
          }
        }
        return result;
    }

    let A = [0, 1, 0, 1, 1];
    let n = A.length;
    document.write(getPassingCars(A, n));

</script>
```

**输出:**

```
5
```

**时间复杂度:** O(n <sup>2</sup> )
**辅助空间:** O(1)

An **高效解**从右遍历数组，从右跟踪 1 的计数。每当我们看到一个 0，我们就把结果增加一个 1。

## C++

```
// Efficient C++ program to count passing cars
#include<bits/stdc++.h>
using namespace std;

// Returns count of passing cars
int getPassingCars(int A[], int n)
{
    // Initialize count of 1s from right
    // and result
    int countOne = 0, result = 0;
    while (n >= 1)
    {
        if (A[n-1] == 1)
            countOne++;
        else
            result += countOne;
        n--;
    }

    return result;
}

// Driver program
int main()
{
    int A[] = {0, 1, 0, 1, 1};
    int n = sizeof(A)/sizeof(A[0]);
    cout << getPassingCars(A, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Efficient Java program to count passing cars
class GFG
{

// Returns count of passing cars
static int getPassingCars(int A[], int n)
{
    // Initialize count of 1s from right
    // and result
    int countOne = 0, result = 0;
    while (n >= 1)
    {
        if (A[n-1] == 1)
            countOne++;
        else
            result += countOne;
        n--;
    }

    return result;
}

// Driver code
public static void main(String[] args)
{
    int A[] = {0, 1, 0, 1, 1};
    int n = A.length;
    System.out.println(getPassingCars(A, n));
}
}

// This code is contributed by Mukul Singh.
```

## 蟒蛇 3

```
# Efficient Python3 program to
# count passing cars

# Returns count of passing cars
def getPassingCars(A, n):

    # Initialize count of 1s
    # from right and result
    countOne = 0; result = 0
    while n >= 1:
        if A[n - 1] == 1:
            countOne += 1
        else:
            result += countOne
        n -= 1
    return result

# Driver code
A = [0, 1, 0, 1, 1]
n = len(A)
print(getPassingCars(A, n))

# This code is contributed
# by Shrikant13
```

## C#

```
// Efficient C# program to
// count passing cars
using System;

class GFG
{

// Returns count of passing cars
static int getPassingCars(int []A, int n)
{
    // Initialize count of 1s from right
    // and result
    int countOne = 0, result = 0;
    while (n >= 1)
    {
        if (A[n - 1] == 1)
            countOne++;
        else
            result += countOne;
        n--;
    }

    return result;
}

// Driver code
public static void Main()
{
    int []A = {0, 1, 0, 1, 1};
    int n = A.Length;
    Console.Write(getPassingCars(A, n));
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Efficient PHP program to count passing cars

// Returns count of passing cars
function getPassingCars($A, $n)
{
    // Initialize count of 1s from right
    // and result
    $countOne = 0; $result = 0;
    while ($n >= 1)
    {
        if ($A[$n-1] == 1)
            $countOne++;
        else
            $result += $countOne;
        $n--;
    }

    return $result;
}

// Driver Code
$A = array(0, 1, 0, 1, 1);
$n = sizeof($A);
echo getPassingCars($A, $n);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>
    // Efficient Javascript program to count passing cars

    // Returns count of passing cars
    function getPassingCars(A, n)
    {
        // Initialize count of 1s from right
        // and result
        let countOne = 0, result = 0;
        while (n >= 1)
        {
            if (A[n - 1] == 1)
                countOne++;
            else
                result += countOne;
            n--;
        }

        return result;
    }

    let A = [0, 1, 0, 1, 1];
    let n = A.length;
    document.write(getPassingCars(A, n));

</script>
```

**输出:**

```
5
```

**时间复杂度:** O(n)
**辅助空间:** O(1)
**参考:**
[http://stackoverflow . com/questions/23774985/coding-passing-car](http://stackoverflow.com/questions/23774985/codility-passing-car)
本文由 [**Rakesh Kumar**](https://www.facebook.com/Rakesh2raj) 投稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。