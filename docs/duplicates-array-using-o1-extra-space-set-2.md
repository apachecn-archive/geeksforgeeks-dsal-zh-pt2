# 用 O(n)和使用 O(1)额外空间在数组中复制| Set-2

> 原文:[https://www . geesforgeks . org/duplicates-array-use-O1-extra-space-set-2/](https://www.geeksforgeeks.org/duplicates-array-using-o1-extra-space-set-2/)

给定包含从 0 到 n-1 的元素的 n 个元素的数组，这些数字中的任何一个出现任何次数，在 O(n)中找到这些重复的数字，并且只使用恒定的内存空间。

**示例:**

```
Input: n = 7 , array = {1, 2, 3, 1, 3, 6, 6}
Output: 1, 3 and 6.
Explanation: Duplicate element in the array are 1 , 3 and 6

Input: n = 6, array = {5, 3, 1, 3, 5, 5}
Output: 3 and 5.
Explanation: Duplicate element in  the array are 3 and 6
```

我们已经在下面的帖子中讨论了这个问题的解决方法:
[在数组中用 O(n)重复，并使用 O(1)额外的空间| Set-2](https://www.geeksforgeeks.org/find-duplicates-in-on-time-and-constant-extra-space/) 。
但是上面的做法有问题。它会多次打印重复的数字。

## [我们强烈建议您点击此处进行练习，然后再进入解决方案。](https://practice.geeksforgeeks.org/problems/find-duplicates-in-an-array/1)

**<u>逼近</u> :** 基本思路是用一个 HashMap 来解决问题。但是有一个问题，数组中的数字是从 0 到 n-1，输入数组的长度是 n。所以，输入数组可以用作哈希映射。遍历数组时，如果遇到元素 *a* ，则将第 *a%n* 个元素的值增加 n。频率可以通过将第 *a%n* 个元素除以 n 来获取。

**<u>算法</u> :**

1.  从头到尾遍历给定的数组。
2.  对于数组中的每个元素，将第*个元素递增 n*
3.  现在再次遍历数组并打印所有那些*arr[I]/n*大于 1 的索引 I。这保证了数字 *n* 已经被添加到该指数中。

**注意:**这种方法有效，因为所有元素都在 0 到 n-1 的范围内，只有当值“I”出现多次时，arr[I/n]才会大于 1。

下面是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to print all elements that
// appear more than once.
#include <iostream>
using namespace std;

// function to find repeating elements
void printRepeating(int arr[], int n)
{
    // First check all the values that are
    // present in an array then go to that
    // values as indexes and increment by
    // the size of array
    for (int i = 0; i < n; i++)
    {
        int index = arr[i] % n;
        arr[index] += n;
    }

    // Now check which value exists more
    // than once by dividing with the size
    // of array
    for (int i = 0; i < n; i++)
    {
        if ((arr[i] / n) >= 2)
            cout << i << " ";
    }
}

// Driver code
int main()
{
    int arr[] = { 1, 6, 3, 1, 3, 6, 6 };
    int arr_size = sizeof(arr) / sizeof(arr[0]);

    cout << "The repeating elements are: \n";

    // Function call
    printRepeating(arr, arr_size);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print all elements that
// appear more than once.
import java.util.*;
class GFG {

    // function to find repeating elements
    static void printRepeating(int arr[], int n)
    {
        // First check all the values that are
        // present in an array then go to that
        // values as indexes and increment by
        // the size of array
        for (int i = 0; i < n; i++)
        {
            int index = arr[i] % n;
            arr[index] += n;
        }

        // Now check which value exists more
        // than once by dividing with the size
        // of array
        for (int i = 0; i < n; i++)
        {
            if ((arr[i] / n) >= 2)
                System.out.print(i + " ");
        }
    }

    // Driver code
    public static void main(String args[])
    {
        int arr[] = { 1, 6, 3, 1, 3, 6, 6 };
        int arr_size = arr.length;

        System.out.println("The repeating elements are: ");

        // Function call
        printRepeating(arr, arr_size);
    }
}
```

## 蟒蛇 3

```
# Python3 program to
# print all elements that
# appear more than once.

# function to find
# repeating elements

def printRepeating(arr, n):

    # First check all the
        # values that are
    # present in an array
        # then go to that
    # values as indexes
        # and increment by
    # the size of array
    for i in range(0, n):
        index = arr[i] % n
        arr[index] += n

    # Now check which value
        # exists more
    # than once by dividing
        # with the size
    # of array
    for i in range(0, n):
        if (arr[i]/n) >= 2:
            print(i, end=" ")

# Driver code
arr = [1, 6, 3, 1, 3, 6, 6]
arr_size = len(arr)

print("The repeating elements are:")

# Function call
printRepeating(arr, arr_size)

# This code is contributed
# by Shreyanshi Arun.
```

## C#

```
// C# program to print all elements that
// appear more than once.

using System;
class GFG {

    // function to find repeating elements
    static void printRepeating(int[] arr, int n)
    {
        // First check all the values that are
        // present in an array then go to that
        // values as indexes and increment by
        // the size of array
        for (int i = 0; i < n; i++)
        {
            int index = arr[i] % n;
            arr[index] += n;
        }

        // Now check which value exists more
        // than once by dividing with the size
        // of array
        for (int i = 0; i < n; i++)
        {
            if ((arr[i] / n) >= 2)
                Console.Write(i + " ");
        }
    }

    // Driver code
    public static void Main()
    {
        int[] arr = { 1, 6, 3, 1, 3, 6, 6 };
        int arr_size = arr.Length;

        Console.Write("The repeating elements are: "
                      + "\n");

        // Function call
        printRepeating(arr, arr_size);
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print all
// elements that appear more
// than once.

// function to find
// repeating elements
function printRepeating( $arr, $n)
{
    // First check all the values
    // that are present in an array
    // then go to that values as indexes
    // and increment by the size of array
    for ($i = 0; $i < $n; $i++)
    {
        $index = $arr[$i] % $n;
        $arr[$index] += $n;
    }

    // Now check which value
    // exists more than once
    // by dividing with the
    // size of array
    for ($i = 0; $i < $n; $i++)
    {
        if (($arr[$i] / $n) >= 2)
            echo $i , " ";
    }
}

// Driver code
$arr = array(1, 6, 3, 1, 3, 6, 6);
$arr_size = sizeof($arr) /
            sizeof($arr[0]);

echo "The repeating elements are: \n";

// Function call
printRepeating( $arr, $arr_size);

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

// Javascript program to print all elements that
// appear more than once.   

    // function to find repeating elements
    function printRepeating(arr,n)
    {
        // First check all the values that are
        // present in an array then go to that
        // values as indexes and increment by
        // the size of array
        for (let i = 0; i < n; i++)
        {
            let index = arr[i] % n;
            arr[index] += n;
        }

        // Now check which value exists more
        // than once by dividing with the size
        // of array
        for (let i = 0; i < n; i++)
        {
            if ((arr[i] / n) >= 2)
                document.write(i + " ");
        }
    }

    // Driver code
    let arr=[1, 6, 3, 1, 3, 6, 6];
    let arr_size = arr.length;
    document.write("The repeating elements are: <br>");

    // Function call
    printRepeating(arr, arr_size);

    //  This code is contributed by avanitrachhadiya2155

</script>
```

**Output**

```
The repeating elements are: 
1 3 6 
```

**<u>复杂度分析</u> :**

*   **时间复杂度:** O(n)。
    只需要两次遍历。所以时间复杂度是 O(n)
*   **辅助空间:** O(1)。
    由于不需要额外的空间，所以空间复杂度是恒定的

本文由 [**萨希尔·查布拉(akku)**](https://www.facebook.com/sahil.chhabra.965) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现任何不正确的地方，或者你想分享更多关于上述话题的信息，请写评论