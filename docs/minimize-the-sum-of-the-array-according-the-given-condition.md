# 根据给定条件

最小化数组的和

> 原文:[https://www . geeksforgeeks . org/根据给定条件最小化数组的总和/](https://www.geeksforgeeks.org/minimize-the-sum-of-the-array-according-the-given-condition/)

给定一组整数**和**。任务是使用以下规则最小化数组元素的总和:
选择两个索引 **i** 和 **j** 和一个任意整数 **x** ，使得 **x** 是 **A[i]** 的除数，并将它们更改如下 **A[i] = A[i]/x** 和 **A[j] = A[j]*x** 。
**举例:**

> **输入:** A = { 1，2，3，4，5 }
> **输出:** 14
> 将 A[3]除以 2 然后
> A[3] = 4/2 = 2，
> 将 A[0]乘以 2 然后
> A[0] = 1*2 = 2
> 更新数组 A = { 2，2，3，2，5 }
> 因此求和= 14
> **输入:**A = =

**方法:**如果任何数除以 **x** ，则最好将数组中最小的数乘以 **x** 。
想法是得到数组的最小值，找到特定元素的除数，并不断检查总和减少了多少。
以下是上述方法的实施:

## C++

```
// C++ implementation
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum sum
void findMin(int arr[], int n)
{
    int sum = 0;
    for (int i = 0; i < n; i++)
        sum += arr[i];

    // sort the array to find the
    // minimum element
    sort(arr, arr + n);

    int min = arr[0];
    int max = 0;

    for (int i = n - 1; i >= 1; i--) {
        int num = arr[i];
        int total = num + min;
        int j;

        // finding the number to
        // divide
        for (j = 2; j <= num; j++) {
            if (num % j == 0) {
                int d = j;
                int now = (num / d)
                          + (min * d);

                // Checking to what
                // instance the sum
                // has decreased
                int reduce = total - now;

                // getting the max
                // difference
                if (reduce > max)
                    max = reduce;
            }
        }
    }
    cout << (sum - max);
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);
    findMin(arr, n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG
{

    // Function to return the minimum sum
    static void findMin(int arr[], int n)
    {
        int sum = 0;
        for (int i = 0; i < n; i++)
            sum += arr[i];

        // sort the array to find the
        // minimum element
        Arrays.sort(arr);

        int min = arr[0];
        int max = 0;

        for (int i = n - 1; i >= 1; i--)
        {
            int num = arr[i];
            int total = num + min;
            int j;

            // finding the number to
            // divide
            for (j = 2; j <= num; j++)
            {
                if (num % j == 0)
                {
                    int d = j;
                    int now = (num / d) +
                              (min * d);

                    // Checking to what
                    // instance the sum
                    // has decreased
                    int reduce = total - now;

                    // getting the max
                    // difference
                    if (reduce > max)
                        max = reduce;
                }
            }
        }
        System.out.println(sum - max);
    }

    // Driver Code
    public static void main (String[] args)
    {
        int arr[] = { 1, 2, 3, 4, 5 };
        int n = arr.length;
        findMin(arr, n);
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Function to return the minimum sum
def findMin(arr, n):
    sum = 0
    for i in range(0, n):
        sum = sum + arr[i]

    # sort the array to find the
    # minimum element
    arr.sort()

    min = arr[0]
    max = 0

    for i in range(n - 1, 0, -1):
        num = arr[i]
        total = num + min

        # finding the number to
        # divide
        for j in range(2, num + 1):
            if(num % j == 0):
                d = j
                now = (num // d) + (min * d)

                # Checking to what
                # instance the sum
                # has decreased
                reduce = total - now

                # getting the max
                # difference
                if(reduce > max):
                    max = reduce

    print(sum - max)

# Driver Code
arr = [1, 2, 3, 4, 5 ]
n = len(arr)
findMin(arr, n)

# This code is contributed by Sanjit_Prasad
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    // Function to return the minimum sum
    static void findMin(int []arr, int n)
    {
        int sum = 0;
        for (int i = 0; i < n; i++)
            sum += arr[i];

        // sort the array to find the
        // minimum element
        Array.Sort(arr);

        int min = arr[0];
        int max = 0;

        for (int i = n - 1; i >= 1; i--)
        {
            int num = arr[i];
            int total = num + min;
            int j;

            // finding the number to
            // divide
            for (j = 2; j <= num; j++)
            {
                if (num % j == 0)
                {
                    int d = j;
                    int now = (num / d) +
                              (min * d);

                    // Checking to what
                    // instance the sum
                    // has decreased
                    int reduce = total - now;

                    // getting the max
                    // difference
                    if (reduce > max)
                        max = reduce;
                }
            }
        }
        Console.WriteLine(sum - max);
    }

    // Driver Code
    public static void Main (String[] args)
    {
        int []arr = { 1, 2, 3, 4, 5 };
        int n = arr.Length;
        findMin(arr, n);
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript implementation

// Function to return the minimum sum
function findMin(arr, n)
{
    let sum = 0;
    for (let i = 0; i < n; i++)
        sum += arr[i];

    // sort the array to find the
    // minimum element
    arr.sort();

    let min = arr[0];
    let max = 0;

    for (let i = n - 1; i >= 1; i--) {
        let num = arr[i];
        let total = num + min;
        let j;

        // finding the number to
        // divide
        for (j = 2; j <= num; j++) {
            if (num % j == 0) {
                let d = j;
                let now = parseInt(num / d)
                          + (min * d);

                // Checking to what
                // instance the sum
                // has decreased
                let reduce = total - now;

                // getting the max
                // difference
                if (reduce > max)
                    max = reduce;
            }
        }
    }
    document.write(sum - max);
}

// Driver Code
    let arr = [ 1, 2, 3, 4, 5 ];
    let n = arr.length;
    findMin(arr, n);

</script>
```

**Output:** 

```
14
```