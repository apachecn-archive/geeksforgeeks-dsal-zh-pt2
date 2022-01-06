# 重复去除任意 3 个连续元素的中值后，找到最后两个剩余元素

> 原文:[https://www . geesforgeks . org/find-最后两个剩余元素-移除后-任意 3 个连续元素的中值-重复/](https://www.geeksforgeeks.org/find-last-two-remaining-elements-after-removing-median-of-any-3-consecutive-elements-repeatedly/)

给定不同整数的序列 **A <sub>1</sub> ，A <sub>2</sub> ，A <sub>3</sub> ，…A<sub>n</sub>T9】。任务是在从序列中重复移除任意 3 个连续元素的中间值后，找到最后 2 个剩余元素。
**举例:**** 

> **输入:** A[] = {2，5，3}
> **输出:** 2 5
> 的{2，5，3}的中位数为 3，去掉
> 后它剩下的元素为{2，5}。
> **输入:** A[] = {38，9，102，10，96，7，46，28，88，13}
> **输出:** 7 102

**逼近:**对于每一次运算，中值元素都是既不是最大值也不是最小值的元素。因此，应用该操作后，最小值和最大值元素都不会受到影响。概括之后，可以看到最终数组应该只包含来自初始数组的最小和最大元素。
以下是上述办法的实施情况:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the last
// two remaining elements
void lastTwoElement(int A[], int n)
{

    // Find the minimum and the maximum
    // element from the array
    int minn = *min_element(A, A + n);
    int maxx = *max_element(A, A + n);

    cout << minn << " " << maxx;
}

// Driver code
int main()
{
    int A[] = { 38, 9, 102, 10, 96,
                7, 46, 28, 88, 13 };
    int n = sizeof(A) / sizeof(int);

    lastTwoElement(A, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    static int min_element(int A[], int n)
    {
        int min = A[0];
        for(int i = 0; i < n; i++)
            if (A[i] < min )
                min = A[i];

        return min;

    }

    static int max_element(int A[], int n)
    {
        int max = A[0];
        for(int i = 0; i < n; i++)
            if (A[i] > max )
                max = A[i];

        return max;
    }

    // Function to find the last
    // two remaining elements
    static void lastTwoElement(int A[], int n)
    {

        // Find the minimum and the maximum
        // element from the array
        int minn = min_element(A, n);
        int maxx = max_element(A, n);

        System.out.println(minn + " " + maxx);
    }

    // Driver code
    public static void main (String[] args)
    {
        int A[] = { 38, 9, 102, 10, 96,
                    7, 46, 28, 88, 13 };

        int n = A.length;

        lastTwoElement(A, n);
    }
}

// This code is contributed by AnkitRai01
```

## 计算机编程语言

```
# Python3 implementation of the approach

# Function to find the last
# two remaining elements
def lastTwoElement(A, n):

    # Find the minimum and the maximum
    # element from the array
    minn = min(A)
    maxx = max(A)

    print(minn, maxx)

# Driver code
A = [38, 9, 102, 10, 96,7, 46, 28, 88, 13]
n = len(A)

lastTwoElement(A, n)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    static int min_element(int []A, int n)
    {
        int min = A[0];
        for(int i = 0; i < n; i++)
            if (A[i] < min )
                min = A[i];

        return min;
    }

    static int max_element(int []A, int n)
    {
        int max = A[0];
        for(int i = 0; i < n; i++)
            if (A[i] > max )
                max = A[i];

        return max;
    }

    // Function to find the last
    // two remaining elements
    static void lastTwoElement(int []A, int n)
    {

        // Find the minimum and the maximum
        // element from the array
        int minn = min_element(A, n);
        int maxx = max_element(A, n);

        Console.WriteLine(minn + " " + maxx);
    }

    // Driver code
    public static void Main ()
    {
        int []A = { 38, 9, 102, 10, 96,
                    7, 46, 28, 88, 13 };

        int n = A.Length;

        lastTwoElement(A, n);
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Java Script implementation of the approach
function min_element(A,n)
    {
        let min = A[0];
        for(let i = 0; i < n; i++)
            if (A[i] < min )
                min = A[i];

        return min;

    }

    function max_element(A,n)
    {
        let max = A[0];
        for(let i = 0; i < n; i++)
            if (A[i] > max )
                max = A[i];

        return max;
    }

    // Function to find the last
    // two remaining elements
    function lastTwoElement(A,n)
    {

        // Find the minimum and the maximum
        // element from the array
        let minn = min_element(A, n);
        let maxx = max_element(A, n);

        document.write(minn + " " + maxx);
    }

    // Driver code

        let A = [ 38, 9, 102, 10, 96,
                    7, 46, 28, 88, 13 ];

        let n = A.length;

        lastTwoElement(A, n);

// This code is contributed by sravan kumar Gottumukkala
</script>
```

**Output:** 

```
7 102
```

**时间复杂度:** O(n)