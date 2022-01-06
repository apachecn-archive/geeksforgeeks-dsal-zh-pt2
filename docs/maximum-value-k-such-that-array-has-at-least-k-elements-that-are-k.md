# 最大值 K，这样数组至少有 K 个元素是> = K

> 原文:[https://www . geesforgeks . org/maximum-value-k-so-so-array-至少有-k-elements-be-k/](https://www.geeksforgeeks.org/maximum-value-k-such-that-array-has-at-least-k-elements-that-are-k/)

给定一个由**个正整数**组成的数组，找到最大可能值 K，使得该数组至少有 K 个大于或等于 K 的元素。该数组没有排序，可能包含重复值。
**例:**

```
Input: [2, 3, 4, 5, 6, 7]
Output: 4
Explanation : 4 elements [4, 5, 6, 7] 
            are greater than equal to 4

Input: [1, 2, 3, 4]
Output: 2
Explanation : 3 elements [2, 3, 4] are 
               greater than equal to 2

Input: [4, 7, 2, 3, 8]
Output: 3 
Explanation : 4 elements [4, 7, 3, 8] 
          are greater than equal to 3

Input: [6, 7, 9, 8, 10]
Output: 5
Explanation : All 5 elements are greater
              than equal to 5 
```

预期时间复杂度:O(n)

**方法 1【简单:O(n <sup>2</sup> )时间】**
让输入数组的大小为 n，让我们考虑以下重要观察。

1.  结果的最大可能值可以是 n，当所有元素都大于或等于 n 时，我们得到最大可能值，例如，如果输入数组是{10，20，30}，n 就是 3。结果的值不能大于 3。
2.  最小可能值为 1。得到这个输出的一个例子是，当所有元素都是 1 时。

所以我们可以运行一个从 n 到 1 的循环，为每个值计算更多的元素。

## C++

```
// C++ program to find maximum possible value K
// such that array has at-least K elements that
// are greater than or equals to K.
#include <iostream>
using namespace std;

// Function to return maximum possible value K
// such that array has atleast K elements that
// are greater than or equals to K
int findMaximumNum(unsigned int arr[], int n)
{
    // output can contain any number from n to 0
    // where n is length of the array

    // We start a loop from n as we need to find
    // maximum possible value
    for (int i = n; i >= 1; i--)
    {
        // count contains total number of elements
        // in input array that are more than equal to i
        int count = 0;

        // traverse the input array and find count
        for (int j=0; j<n; j++)
            if (i <= arr[j])
                count++;

        if (count >= i)
          return i;
    }   
    return 1;
}

// Driver code
int main()
{
    unsigned int arr[] = {1, 2, 3, 8, 10 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << findMaximumNum(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum
// possible value K such that
// array has at-least K elements
// that are greater than or equals to K.
import java.io.*;

class GFG
{

// Function to return maximum
// possible value K such that
// array has atleast K elements
// that are greater than or equals to K
static int findMaximumNum(int arr[],
                          int n)
{
    // output can contain any
    // number from n to 0 where
    // n is length of the array

    // We start a loop from n
    // as we need to find
    // maximum possible value
    for (int i = n; i >= 1; i--)
    {
        // count contains total
        // number of elements
        // in input array that
        // are more than equal to i
        int count = 0;

        // traverse the input
        // array and find count
        for (int j = 0; j < n; j++)
            if (i <= arr[j])
                count++;

        if (count >= i)
        return i;
    }
    return 1;
}

// Driver code
public static void main (String[] args)
{
int arr[] = {1, 2, 3, 8, 10 };
int n = arr.length;
System.out.println(findMaximumNum(arr, n));
}
}

// This code is contributed by aj_36
```

## 蟒蛇 3

```
# python 3 program to find maximum possible value K
# such that array has at-least K elements that
# are greater than or equals to K.

# Function to return maximum possible value K
# such that array has atleast K elements that
# are greater than or equals to K
def findMaximumNum(arr, n):
    # output can contain any number from n to 0
    # where n is length of the array

    # We start a loop from n as we need to find
    # maximum possible value
    i = n
    while(i >= 1):
        # count contains total number of elements
        # in input array that are more than equal to i
        count = 0

        # traverse the input array and find count
        for j in range(0,n,1):
            if (i <= arr[j]):
                count += 1

        if (count >= i):
            return i

        i -= 1

    return 1

# Driver code
if __name__ == '__main__':
    arr = [1, 2, 3, 8, 10]
    n = len(arr)
    print(findMaximumNum(arr, n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find maximum
// possible value K such that
// array has at-least K elements
// that are greater than or equals to K.
using System;

class GFG
{

// Function to return maximum
// possible value K such that
// array has atleast K elements
// that are greater than or equals to K
static int findMaximumNum(int []arr,
                          int n)
{
    // output can contain any
    // number from n to 0 where
    // n is length of the array

    // We start a loop from n
    // as we need to find
    // maximum possible value
    for (int i = n; i >= 1; i--)
    {
        // count contains total
        // number of elements
        // in input array that
        // are more than equal to i
        int count = 0;

        // traverse the input
        // array and find count
        for (int j = 0; j < n; j++)
            if (i <= arr[j])
                count++;

        if (count >= i)
        return i;
    }
    return 1;
}

// Driver code
static public void Main ()
{
    int []arr = {1, 2, 3, 8, 10 };
    int n = arr.Length;
    Console.WriteLine(findMaximumNum(arr, n));
}
}

// This code is contributed by m_kit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find maximum
// possible value K such that
// array has at-least K elements
// that are greater than or
// equals to K.

// Function to return maximum
// possible value K such that
// array has atleast K elements
// that are greater than or
// equals to K
function findMaximumNum($arr, $n)
{
    // output can contain any
    // number from n to 0 where
    // n is length of the array

    // We start a loop from
    // n as we need to find
    // maximum possible value
    for ($i = $n; $i >= 1; $i--)
    {
        // count contains total
        // number of elements in
        // input array that are
        // more than equal to i
        $count = 0;

        // traverse the input
        // array and find count
        for ($j = 0; $j < $n; $j++)
            if ($i <= $arr[$j])
                $count++;

        if ($count >= $i)
        return $i;
    }
    return 1;
}

// Driver code
$arr = array (1, 2, 3, 8, 10);
$n = sizeof($arr);
echo findMaximumNum($arr, $n);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

    // Javascript program to find maximum
    // possible value K such that
    // array has at-least K elements
    // that are greater than or equals to K.

    // Function to return maximum
    // possible value K such that
    // array has atleast K elements
    // that are greater than or equals to K
    function findMaximumNum(arr, n)
    {
        // output can contain any
        // number from n to 0 where
        // n is length of the array

        // We start a loop from n
        // as we need to find
        // maximum possible value
        for (let i = n; i >= 1; i--)
        {
            // count contains total
            // number of elements
            // in input array that
            // are more than equal to i
            let count = 0;

            // traverse the input
            // array and find count
            for (let j = 0; j < n; j++)
                if (i <= arr[j])
                    count++;

            if (count >= i)
            return i;
        }
        return 1;
    }

    let arr = [1, 2, 3, 8, 10 ];
    let n = arr.length;
    document.write(findMaximumNum(arr, n));

</script>
```

**输出:**

```
3
```

**方法二【高效:O(n)时间和 O(n)额外空间】**
1)思路是构造 n + 1 大小的腋数组，利用该数组寻找输入数组中较大元素的个数。让辅助数组为 freq[]。我们将这个数组的所有元素初始化为 0。
2)我们处理所有输入元素。
a)如果一个元素 arr[i]小于 n，那么我们增加它的频率，即我们做 freq[arr[i]]++。
b)否则我们增加频率[n]。
3)第二步之后我们有两件事。
a)存储在 freq[0]中的小于 n 的元素的元素频率..n-1]。
b)存储在 freq[n]中的大于 n 的元素计数。
最后，我们向后处理 freq[]数组，通过保持到目前为止处理的值的总和来找到输出。
以下是上述思路的实现。

## C++

```
// C++ program to find maximum possible value K such
// that array has atleast K elements that are greater
// than or equals to K.
#include <bits/stdc++.h>
using namespace std;

// Function to return maximum possible value K such
// that array has at-least K elements that are greater
// than or equals to K.
int findMaximumNum(unsigned int arr[], int n)
{
    // construct axillary array of size n + 1 and
    // initialize the array with 0
    vector<int> freq(n+1, 0);

    // store the frequency of elements of
    // input array in the axillary array
    for (int i = 0; i < n; i++)
    {
        // If element is smaller than n, update its
        // frequency
        if (arr[i] < n)
            freq[arr[i]]++;

        // Else increment count of elements greater
        // than n.
        else
            freq[n]++;
    }

    // sum stores number of elements in input array
    // that are greater than or equal to current
    // index
    int sum = 0;

    // scan auxiliary array backwards
    for (int i = n; i > 0; i--)
    {
        sum += freq[i];

        // if sum is greater than current index,
        // current index is the answer
        if (sum >= i)
            return i;
    }
}

// Driver code
int main()
{
    unsigned int arr[] = {1, 2, 3, 8, 10 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << findMaximumNum(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum possible value K such
// that array has atleast K elements that are greater
// than or equals to K.

import java.util.Vector;

class GFG {

// Function to return maximum possible value K such
// that array has at-least K elements that are greater
// than or equals to K.
    static int findMaximumNum(int arr[], int n) {
        // construct axillary array of size n + 1 and
        // initialize the array with 0
        int[] freq=new int[n+1];
        for (int i = 0; i < n + 1; i++) {
            freq[i] = 0;
        }

        // store the frequency of elements of
        // input array in the axillary array
        for (int i = 0; i < n; i++) {
            // If element is smaller than n, update its
            // frequency
            if (arr[i] < n) //
            {
                freq[arr[i]]++;
            } // Else increment count of elements greater
            // than n.
            else {
                freq[n]++;
            }
        }

        // sum stores number of elements in input array
        // that are greater than or equal to current
        // index
        int sum = 0;

        // scan auxiliary array backwards
        for (int i = n; i > 0; i--) {
            sum += freq[i];

            // if sum is greater than current index,
            // current index is the answer
            if (sum >= i) {
                return i;
            }
        }
        return 0;
    }

// Driver code
    public static void main(String[] args) {
        int arr[] = {1, 2, 3, 8, 10};
        int n = arr.length;
        System.out.println(findMaximumNum(arr, n));
    }
}
/*This Java code is contributed by koulick_sadhu*/
```

## C#

```
// C# program to find maximum possible value K such
// that array has atleast K elements that are greater
// than or equals to K.
using System;
using System.Collections.Generic;

class GFG
{

    // Function to return maximum possible value K such
    // that array has at-least K elements that are greater
    // than or equals to K.
    static int findMaximumNum(int []arr, int n)
    {
        // construct axillary array of size n + 1 and
        // initialize the array with 0
        List<int> freq = new List<int>();
        for (int i = 0; i < n + 1; i++)
        {
            freq.Insert(i, 0);
        }

        // store the frequency of elements of
        // input array in the axillary array
        for (int i = 0; i < n; i++)
        {
            // If element is smaller than n, update its
            // frequency
            if (arr[i] < n) //freq[arr[i]]++;
            {
                freq.Insert(arr[i], freq[arr[i]] + 1);
            }
            // Else increment count of elements greater
            // than n.
            else
            {
                freq.Insert(n, freq[n] + 1);
            }
            //freq[n]++;
        }

        // sum stores number of elements in input array
        // that are greater than or equal to current
        // index
        int sum = 0;

        // scan auxiliary array backwards
        for (int i = n; i > 0; i--)
        {
            sum += freq[i];

            // if sum is greater than current index,
            // current index is the answer
            if (sum >= i)
            {
                return i;
            }
        }
        return 0;
    }

    // Driver code
    public static void Main()
    {
        int []arr = {1, 2, 3, 8, 10};
        int n = arr.Length;
        Console.WriteLine(findMaximumNum(arr, n));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>
// Javascript program to find maximum possible value K such
// that array has atleast K elements that are greater
// than or equals to K.

// Function to return maximum possible value K such
// that array has at-least K elements that are greater
// than or equals to K.
function findMaximumNum(arr, n)
{

    // construct axillary array of size n + 1 and
    // initialize the array with 0
    let freq = new Array(n + 1).fill(0);

    // store the frequency of elements of
    // input array in the axillary array
    for (let i = 0; i < n; i++) {
        // If element is smaller than n, update its
        // frequency
        if (arr[i] < n)
            freq[arr[i]]++;

        // Else increment count of elements greater
        // than n.
        else
            freq[n]++;
    }

    // sum stores number of elements in input array
    // that are greater than or equal to current
    // index
    let sum = 0;

    // scan auxiliary array backwards
    for (let i = n; i > 0; i--) {
        sum += freq[i];

        // if sum is greater than current index,
        // current index is the answer
        if (sum >= i)
            return i;
    }
}

// Driver code
let arr = [1, 2, 3, 8, 10];
let n = arr.length;
document.write(findMaximumNum(arr, n));

// This code is contributed by gfgking.
</script>
```

**输出:**

```
3
```

本文由**阿迪蒂亚·戈尔**供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如发现任何不正确的地方，请写评论，或者您想分享更多关于上述话题的信息