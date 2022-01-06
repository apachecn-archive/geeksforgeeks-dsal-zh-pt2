# 最大化数组中(a[i]+i)*(a[j]+j)的值

> 原文:[https://www.geeksforgeeks.org/maximize-value-aiiajj-array/](https://www.geeksforgeeks.org/maximize-value-aiiajj-array/)

给定一个输入大小为 n 的数组，求(a[i] + i) * (a[j] + j)的最大值，其中 i **不等于**到 j.
注意 I 和 j 从 **0** 到 **n-1** 不等。
**示例:**

```
Input : a[] = [4,5,3,1,10]
Output : 84
Explanation:
We get the maximum value for i = 4 and j = 1
(10 + 4) * (5 + 1) = 84

Input : a[] = [10,0,0,0,-1]
Output : 30
Explanation:
We get the maximum value for i = 0 and j = 3
(10 + 0) * (0 + 3) = 30
```

**天真的方法:***最简单的*方法是运行两个循环来考虑所有可能的对，并跟踪表达式(a[i]+i)*(a[j]+j)的最大值。下面是这个想法的 Python 实现。**时间复杂度为 O(n*n)** 其中 n 为输入大小。

## C++

```
// C++ program to find maximum value (a[i]+i)*
// (a[j]+j) in an array of integers. maxval()
// returns maximum value of (a[i]+i)*(a[j]+j)
// where i is not equal to j
#include<bits/stdc++.h>
using namespace std;

int maxval(int a[], int n) {

        // at-least there must be two elements
        // in array
        if (n < 2) {
            return -99999;
        }

        // calculate maximum value
        int max = 0;
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                int x = (a[i] + i) * (a[j] + j);
                if (max < x) {
                    max = x;
                }
            }
        }

        return max;
    }

        // test the function
    int main()
    {
        int arr[] = {4, 5, 3, 1, 10};
        int len = sizeof(arr)/sizeof(arr[0]);
        cout<<(maxval(arr, len));
    }

// This code is contributed by
// Shashank_Sharma
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum value (a[i]+i)*
// (a[j]+j) in an array of integers. maxval()
// returns maximum value of (a[i]+i)*(a[j]+j)
// where i is not equal to j

public class GFG {
// Python

    static int maxval(int a[], int n) {

        // at-least there must be two elements
        // in array
        if (n < 2) {
            return -99999;
        }

        // calculate maximum value
        int max = 0;
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                int x = (a[i] + i) * (a[j] + j);
                if (max < x) {
                    max = x;
                }
            }
        }

        return max;
    }
// test the function

    public static void main(String args[]) {
        int arr[] = {4, 5, 3, 1, 10};
        int len = arr.length;
        System.out.println(maxval(arr, len));

    }
}

/*This code is contributed by 29AjayKumar*/
```

## 蟒蛇 3

```
# Python program to find maximum value (a[i]+i)*
# (a[j]+j) in an array of integers. maxval()
# returns maximum value of (a[i]+i)*(a[j]+j)
# where i is not equal to j
def maxval(a,n):

    # at-least there must be two elements
    # in array
    if (n < 2):
        return -99999

    # calculate maximum value
    max = 0
    for i in range(n):
        for j in range(i+1,n):
                x = (a[i]+i)*(a[j]+j)
                if max < x:
                    max = x
    return max

# test the function
print(maxval([4,5,3,1,10],5))
```

## C#

```

// C# program to find maximum value (a[i]+i)*
// (a[j]+j) in an array of integers. maxval()
// returns maximum value of (a[i]+i)*(a[j]+j)
// where i is not equal to j
using System;
public class GFG {
// Python

    static int maxval(int []a, int n) {

        // at-least there must be two elements
        // in array
        if (n < 2) {
            return -99999;
        }

        // calculate maximum value
        int max = 0;
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                int x = (a[i] + i) * (a[j] + j);
                if (max < x) {
                    max = x;
                }
            }
        }

        return max;
    }
// test the function

    public static void Main() {
        int []arr = {4, 5, 3, 1, 10};
        int len = arr.Length;
        Console.Write(maxval(arr, len));

    }
}

/*This code is contributed by 29AjayKumar*/
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find maximum value (a[i]+i)*
// (a[j]+j) in an array of integers. maxval()
// returns maximum value of (a[i]+i)*(a[j]+j)
// where i is not equal to on

function maxval($a, $n)
{

    // at-least there must be two
    // elements in array
    if ($n < 2)
    {
        return -99999;
    }

    // calculate maximum value
    $max = 0;
    for ($i = 0; $i < $n; $i++)
    {
        for ($j = $i + 1; $j < $n; $j++)
        {
            $x = ($a[$i] + $i) * ($a[$j] + $j);
            if ($max < $x)
            {
                $max = $x;
            }
        }
    }

    return $max;
}

// Driver Code
$arr = array(4, 5, 3, 1, 10);
$len = count($arr);
echo (maxval($arr, $len));

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
    // Javascript program to find maximum value (a[i]+i)*
    // (a[j]+j) in an array of integers. maxval()
    // returns maximum value of (a[i]+i)*(a[j]+j)
    // where i is not equal to j

    function maxval(a, n) {

        // at-least there must be two elements
        // in array
        if (n < 2) {
            return -99999;
        }

        // calculate maximum value
        let max = 0;
        for (let i = 0; i < n; i++) {
            for (let j = i + 1; j < n; j++) {
                let x = (a[i] + i) * (a[j] + j);
                if (max < x) {
                    max = x;
                }
            }
        }

        return max;
    }

    let arr = [4, 5, 3, 1, 10];
    let len = arr.length;
    document.write(maxval(arr, len));

</script>
```

**输出:**

```
84
```

**高效的方法:**一个高效的方法是在数组中找到 a[i] + i 的 ***最大值*** 以及 a[i] + i 的 ***次最大值*** 值。返回两个值的乘积。
寻找最大值和第二个最大值可以在数组的单次遍历中完成。
所以，**时间复杂度将为 O(n)** 。
下面是这个思路的实现。

## C++

```
// C++ program to find maximum value (a[i]+i)*
// (a[j]+j) in an array of integers
// maxval() returns maximum value of (a[i]+i)*(a[j]+j)
// where i is not equal to j
#include<bits/stdc++.h>
using namespace std;
#define MAX 5

int maxval(int a[MAX], int n)
{

    // there must be at-least two
    // elements in the array
    if (n < 2)
    {
        cout << "Invalid Input";
        return -9999;
    }

    // max1 will store the maximum value of
    // (a[i]+i)
    // max2 will store the second maximum value
    // of (a[i]+i)
    int max1 = 0, max2 = 0;
    for (int i = 0; i < n; i++)
    {
        int x = a[i] + i;

        // If current element x is greater than
        // first then update first and second
        if (x > max1)
        {
            max2 = max1;
            max1 = x;
        }

        // if x is in between max1 and
        // max2 then update max2
        else if (x > max2 & x != max1)
        {
            max2 = x;
        }
    }
    return (max1 * max2);
}

// Driver Code
int main()
{
    int arr[] = {4, 5, 3, 1, 10};
    int len = sizeof(arr)/arr[0];
    cout << maxval(arr, len);
}

// This code is contributed
// by Akanksha Rai
```

## C

```
// C program to find maximum value (a[i]+i)*
// (a[j]+j) in an array of integers
// maxval() returns maximum value of (a[i]+i)*(a[j]+j)
// where i is not equal to j
#include<stdio.h>
#include<string.h>
#define MAX 5

int maxval(int a[MAX], int n) {

    // there must be at-least two elements in
    // the array
    if (n < 2) {
        printf("Invalid Input");
        return -9999;
    }
    // max1 will store the maximum value of
    //      (a[i]+i)
    // max2 will store the second maximum value
    //      of (a[i]+i)
    int max1 = 0, max2 = 0;
    for (int i = 0; i < n; i++) {
        int x = a[i] + i;

        // If current element x is greater than
        // first then update first and second
        if (x > max1) {
            max2 = max1;
            max1 = x;
        }// if x is in between max1 and
            // max2 then update max2
        else if (x > max2 & x != max1) {
            max2 = x;
        }
    }
    return (max1 * max2);

    // test the function
}

int main() {
    int arr[] = {4, 5, 3, 1, 10};
    int len = sizeof(arr)/arr[0];
    printf("%d",maxval(arr, len));
}
// This code is contributed by 29AjayKumar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum value (a[i]+i)*
// (a[j]+j) in an array of integers
// maxval() returns maximum value of (a[i]+i)*(a[j]+j)
// where i is not equal to j

class GFG {

    static int maxval(int[] a, int n) {

        // there must be at-least two elements in
        // the array
        if (n < 2) {
            System.out.print("Invalid Input");
            return -9999;
        }
        // max1 will store the maximum value of
        //      (a[i]+i)
        // max2 will store the second maximum value
        //      of (a[i]+i)
        int max1 = 0, max2 = 0;
        for (int i = 0; i < n; i++) {
            int x = a[i] + i;

            // If current element x is greater than
            // first then update first and second
            if (x > max1) {
                max2 = max1;
                max1 = x;
            } // if x is in between max1 and
            // max2 then update max2
            else if (x > max2 & x != max1) {
                max2 = x;
            }
        }
        return (max1 * max2);

// test the function
    }

    public static void main(String[] args) {
        int arr[] = {4, 5, 3, 1, 10};
        int len = arr.length;
        System.out.println(maxval(arr, len));
    }
}
// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python program to find maximum value (a[i]+i)*
# (a[j]+j) in an array of integers
# maxval() returns maximum value of (a[i]+i)*(a[j]+j)
# where i is not equal to j
def maxval(a,n):

    # there must be at-least two elements in
    # the array
    if (n < 2):
        print("Invalid Input")
        return -9999

    # max1 will store the maximum value of
    #      (a[i]+i)
    # max2 will store the second maximum value
    #      of (a[i]+i)
    (max1, max2) = (0, 0)
    for i in range(n):
        x = a[i] + i

        # If current element x is greater than
        # first then update first and second
        if (x > max1):
            max2 = max1
            max1 = x

        # if x is in between max1 and
        # max2 then update max2
        elif (x > max2 and x != max1):
             max2 = x
    return(max1*max2)

# test the function
print(maxval([4,5,3,1,10],5))
```

## C#

```

// C# program to find maximum value (a[i]+i)*
// (a[j]+j) in an array of integers
// maxval() returns maximum value of (a[i]+i)*(a[j]+j)
// where i is not equal to j
using System;   
public class GFG {

    static int maxval(int[] a, int n) {

        // there must be at-least two elements in
        // the array
        if (n < 2) {
            Console.WriteLine("Invalid Input");
            return -9999;
        }
        // max1 will store the maximum value of
        //      (a[i]+i)
        // max2 will store the second maximum value
        //      of (a[i]+i)
        int max1 = 0, max2 = 0;
        for (int i = 0; i < n; i++) {
            int x = a[i] + i;

            // If current element x is greater than
            // first then update first and second
            if (x > max1) {
                max2 = max1;
                max1 = x;
            } // if x is in between max1 and
            // max2 then update max2
            else if (x > max2 & x != max1) {
                max2 = x;
            }
        }
        return (max1 * max2);

// test the function
    }

    public static void Main() {
        int []arr = {4, 5, 3, 1, 10};
        int len = arr.Length;
        Console.WriteLine(maxval(arr, len));
    }
}
// This code is contributed by PrinciRaj1992
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find maximum value (a[i]+i)*
// (a[j]+j) in an array of integers
// maxval() returns maximum value of (a[i]+i)*(a[j]+j)
// where i is not equal to j
// $MAX = 5;
function maxval($a, $n)
{

    // there must be at-least two elements in
    // the array
    if ($n < 2)
    {
        echo ("Invalid Input");
        return -9999;
    }

    // max1 will store the maximum value of
    // (a[i]+i)
    // max2 will store the second maximum value
    // of (a[i]+i)
    $max1 = 0;
    $max2 = 0;
    for ($i = 0; $i < $n; $i++)
    {
        $x = $a[$i] + $i;

        // If current element x is greater than
        // first then update first and second
        if ($x > $max1)
        {
            $max2 = $max1;
            $max1 = $x;
        } 

        // if x is in between max1 and
        // max2 then update max2
        else if (($x > $max2) & ($x != $max1))
        {
            $max2 = $x;
        }
    }
    return ($max1 * $max2);
}

// Driver Code
$arr = array(4, 5, 3, 1, 10);
$len = count($arr);
echo maxval($arr, $len);

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>

    // Javascript program to find maximum value (a[i]+i)*
    // (a[j]+j) in an array of integers
    // maxval() returns maximum value of (a[i]+i)*(a[j]+j)
    // where i is not equal to j

    function maxval(a, n)
    {

        // there must be at-least two elements in
        // the array
        if (n < 2) {
            document.write("Invalid Input");
            return -9999;
        }
        // max1 will store the maximum value of
        //      (a[i]+i)
        // max2 will store the second maximum value
        //      of (a[i]+i)
        let max1 = 0, max2 = 0;
        for (let i = 0; i < n; i++) {
            let x = a[i] + i;

            // If current element x is greater than
            // first then update first and second
            if (x > max1)
            {
                max2 = max1;
                max1 = x;
            }
            // if x is in between max1 and
            // max2 then update max2
            else if (x > max2 & x != max1) {
                max2 = x;
            }
        }
        return (max1 * max2);

        // test the function
    }

    let arr = [4, 5, 3, 1, 10];
    let len = arr.length;
    document.write(maxval(arr, len));

</script>
```

**输出:**

```
84
```

本文由 [**Sruti Rai**](https://auth.geeksforgeeks.org/profile.php?user=Sruti Rai&list=practice) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。