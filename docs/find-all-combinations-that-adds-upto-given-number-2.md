# 找出所有加起来等于给定数字的组合

> 原文:[https://www . geesforgeks . org/find-all-combinations-add-up-给定数字-2/](https://www.geeksforgeeks.org/find-all-combinations-that-adds-upto-given-number-2/)

给定一个正数，找出所有与该数相加的正数组合。程序应该只打印组合，而不是排列。例如，对于输入 3，应该打印 1、2 或 2、1。
**例:**

```
Input: N = 3
Output:
1 1 1
1 2
3

Input: N = 5
Output:
1 1 1 1 1
1 1 1 2
1 1 3
1 2 2
1 4
2 3
5 
```

**我们强烈建议你尽量减少浏览器，先自己试试这个。**
想法是用递归。我们使用一个数组来存储组合，我们递归地填充数组，并用减少的数字递归。解决方案中使用的不变量是，每个组合将总是以所涉及元素的递增顺序存储。这样我们就可以避免打印排列。
以下是上述想法的实现:

## C++

```
// C++ program to find out all combinations of
// positive numbers that add upto given number
#include <iostream>
using namespace std;

/*    arr - array to store the combination
    index - next location in array
    num - given number
    reducedNum - reduced number */
void findCombinationsUtil(int arr[], int index,
                       int num, int reducedNum)
{
    // Base condition
    if (reducedNum < 0)
        return;

    // If combination is found, print it
    if (reducedNum == 0)
    {
        for (int i = 0; i < index; i++)
            cout << arr[i] << " ";
        cout << endl;
        return;
    }

    // Find the previous number stored in arr[]
    // It helps in maintaining increasing order
    int prev = (index == 0)? 1 : arr[index-1];

    // note loop starts from previous number
    // i.e. at array location index - 1
    for (int k = prev; k <= num ; k++)
    {
        // next element of array is k
        arr[index] = k;

        // call recursively with reduced number
        findCombinationsUtil(arr, index + 1, num,
                                 reducedNum - k);
    }
}

/* Function to find out all combinations of
   positive numbers that add upto given number.
   It uses findCombinationsUtil() */
void findCombinations(int n)
{
    // array to store the combinations
    // It can contain max n elements
    int arr[n];

    //find all combinations
    findCombinationsUtil(arr, 0, n, n);
}

// Driver code
int main()
{
    int n = 5;
    findCombinations(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find out
// all combinations of positive
// numbers that add upto given
// number
import java.io.*;

class GFG
{
    /* arr - array to store the
    combination
    index - next location in array
    num - given number
    reducedNum - reduced number */
static void findCombinationsUtil(int arr[], int index,
                                 int num, int reducedNum)
{
    // Base condition
    if (reducedNum < 0)
        return;

    // If combination is
    // found, print it
    if (reducedNum == 0)
    {
        for (int i = 0; i < index; i++)
                System.out.print (arr[i] + " ");
            System.out.println();
        return;
    }

    // Find the previous number
    // stored in arr[]. It helps
    // in maintaining increasing
    // order
    int prev = (index == 0) ?
                          1 : arr[index - 1];

    // note loop starts from
    // previous number i.e. at
    // array location index - 1
    for (int k = prev; k <= num ; k++)
    {
        // next element of
        // array is k
        arr[index] = k;

        // call recursively with
        // reduced number
        findCombinationsUtil(arr, index + 1, num,
                                 reducedNum - k);
    }
}

/* Function to find out all
combinations of positive
numbers that add upto given
number. It uses findCombinationsUtil() */
static void findCombinations(int n)
{
    // array to store the combinations
    // It can contain max n elements
    int arr[] = new int [n];

    // find all combinations
    findCombinationsUtil(arr, 0, n, n);
}

// Driver code
public static void main (String[] args)
{
    int n = 5;
    findCombinations(n);
}
}

// This code is contributed
// by akt_mit
```

## 蟒蛇 3

```
# Python3 program to find out all
# combinations of positive
# numbers that add upto given number

# arr - array to store the combination
# index - next location in array
# num - given number
# reducedNum - reduced number
def findCombinationsUtil(arr, index, num,
                              reducedNum):

    # Base condition
    if (reducedNum < 0):
        return

    # If combination is
    # found, print it
    if (reducedNum == 0):

        for i in range(index):
            print(arr[i], end = " ")
        print("")
        return

    # Find the previous number stored in arr[].
    # It helps in maintaining increasing order
    prev = 1 if(index == 0) else arr[index - 1]

    # note loop starts from previous
    # number i.e. at array location
    # index - 1
    for k in range(prev, num + 1):

        # next element of array is k
        arr[index] = k

        # call recursively with
        # reduced number
        findCombinationsUtil(arr, index + 1, num,
                                 reducedNum - k)

# Function to find out all
# combinations of positive numbers
# that add upto given number.
# It uses findCombinationsUtil()
def findCombinations(n):

    # array to store the combinations
    # It can contain max n elements
    arr = [0] * n

    # find all combinations
    findCombinationsUtil(arr, 0, n, n)

# Driver code
n = 5;
findCombinations(n);

# This code is contributed by mits
```

## C#

```
// C# program to find out all
// combinations of positive numbers
// that add upto given number
using System;

class GFG
{

/* arr - array to store the
combination
index - next location in array
num - given number
reducedNum - reduced number */
static void findCombinationsUtil(int []arr, int index,
                                 int num, int reducedNum)
{
    // Base condition
    if (reducedNum < 0)
        return;

    // If combination is
    // found, print it
    if (reducedNum == 0)
    {
        for (int i = 0; i < index; i++)
            Console.Write (arr[i] + " ");
            Console.WriteLine();
        return;
    }

    // Find the previous number
    // stored in arr[]. It helps
    // in maintaining increasing
    // order
    int prev = (index == 0) ?
                          1 : arr[index - 1];

    // note loop starts from
    // previous number i.e. at
    // array location index - 1
    for (int k = prev; k <= num ; k++)
    {
        // next element of
        // array is k
        arr[index] = k;

        // call recursively with
        // reduced number
        findCombinationsUtil(arr, index + 1, num,
                                 reducedNum - k);
    }
}

/* Function to find out all
combinations of positive
numbers that add upto given
number. It uses findCombinationsUtil() */
static void findCombinations(int n)
{
    // array to store the combinations
    // It can contain max n elements
    int []arr = new int [n];

    // find all combinations
    findCombinationsUtil(arr, 0, n, n);
}

// Driver code
static public void Main ()
{
    int n = 5;
    findCombinations(n);
}
}

// This code is contributed
// by akt_mit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find out all
// combinations of positive
// numbers that add upto given number

/* arr - array to store the combination
    index - next location in array
    num - given number
    reducedNum - reduced number */
function findCombinationsUtil($arr, $index,
                              $num, $reducedNum)
{
    // Base condition
    if ($reducedNum < 0)
        return;

    // If combination is
    // found, print it
    if ($reducedNum == 0)
    {
        for ($i = 0; $i < $index; $i++)
            echo $arr[$i] , " ";
        echo "\n";
        return;
    }

    // Find the previous number
    // stored in arr[] It helps
    // in maintaining increasing order
    $prev = ($index == 0) ? 1 : $arr[$index - 1];

    // note loop starts from previous
    // number i.e. at array location
    // index - 1
    for ($k = $prev; $k <= $num ; $k++)
    {
        // next element of array is k
        $arr[$index] = $k;

        // call recursively with
        // reduced number
        findCombinationsUtil($arr, $index + 1,
                             $num, $reducedNum - $k);
    }
}

/* Function to find out all
combinations of positive numbers
that add upto given number.
It uses findCombinationsUtil() */
function findCombinations($n)
{
    // array to store the combinations
    // It can contain max n elements
    $arr = array();

    //find all combinations
    findCombinationsUtil($arr, 0, $n, $n);
}

// Driver code
$n = 5;
findCombinations($n);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Javascript program to find out
// all combinations of positive
// numbers that add upto given
// number

    /* arr - array to store the
    combination
    index - next location in array
    num - given number
    reducedNum - reduced number */
function findCombinationsUtil(arr, index,
                                 num, reducedNum)
{
    // Base condition
    if (reducedNum < 0)
        return;

    // If combination is
    // found, print it
    if (reducedNum == 0)
    {
        for (let i = 0; i < index; i++)
               document.write (arr[i] + " ");
           document.write("<br/>");
        return;
    }

    // Find the previous number
    // stored in arr[]. It helps
    // in maintaining increasing
    // order
    let prev = (index == 0) ?
                          1 : arr[index - 1];

    // note loop starts from
    // previous number i.e. at
    // array location index - 1
    for (let k = prev; k <= num ; k++)
    {
        // next element of
        // array is k
        arr[index] = k;

        // call recursively with
        // reduced number
        findCombinationsUtil(arr, index + 1, num,
                                 reducedNum - k);
    }
}

/* Function to find out all
combinations of positive
numbers that add upto given
number. It uses findCombinationsUtil() */
function findCombinations(n)
{
    // array to store the combinations
    // It can contain max n elements
    let arr = [];

    // find all combinations
    findCombinationsUtil(arr, 0, n, n);
}

// Driver Code

    let n = 5;
    findCombinations(n);      

</script>
```

**输出:**

```
1 1 1 1 1 
1 1 1 2 
1 1 3 
1 2 2 
1 4 
2 3 
5 
```

**练习:**修改上述解决方案，只考虑组合中不同的元素。
本文由**阿迪蒂亚·戈尔**供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如发现任何不正确的地方，或想分享更多关于上述话题的信息，请写评论