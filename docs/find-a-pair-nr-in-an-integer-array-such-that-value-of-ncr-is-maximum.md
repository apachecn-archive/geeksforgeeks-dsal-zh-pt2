# 在整数数组中找到一对(n，r)，使得 nCr 的值最大

> 原文:[https://www . geesforgeks . org/find-a-pair-NR-in-a-integer-array-so-value-NCR-is-maximum/](https://www.geeksforgeeks.org/find-a-pair-nr-in-an-integer-array-such-that-value-of-ncr-is-maximum/)

给定一个非负整数数组 **arr[]** 。任务是找到一对 **(n，r)** ，使得**T5】nC<sub>r</sub>T9】的值最大可能 **r < n** 。** 

> **<sup>n</sup> C <sub>r</sub> = n！/ (r！*(n–r)！)**

**例:**

> **输入:** arr[] = {5，2，3，4，1}
> **输出:** n = 5 和 r = 2
> T6】5C<sub>3</sub>= 5！/ (3!* (5 – 3)!)= 10
> **输入:** arr[] = {0，2，3，4，1，6，8，9}
> **输出:** n = 9 且 r = 4

**天真法:**一个简单的方法是考虑每个 **(n，r)** 对，找到 **<sup>n</sup> C <sub>r</sub>** 的最大可能值。
**有效途径:**从组合学中可知:

> **当 n 是怪客时:**
> **<sup>【c】<sub><<sup>【c】-什么<<sup>n</sup>【C14】(n-1)/2=<sup><sub>(n+1)/2</sub>>，-什么><sup>【n】</sup>【c】<sub>【n-1】</sub>><sup>【n25】【c】</sup></sup></sup></sub></sup>**
> **即使不在:**-什么<<sup>【n】</sup>【c】<sub>【n/2】<sub>>-什么><sup>【n】</sup>【c】<sub>【n-1】</sub>><sup>【n】</sup>【c】</sub></sub>****

可以观察到**<sup>n</sup>C<sub>r</sub>T5】最大时 **n** 最大，**ABS(r–中)**最小。现在的问题归结为在 **arr[]** 和 **r** 中找到最大的元素，使得**ABS(r–中间)**最小。
以下是上述方法的实施:** 

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the pair (n, r)
// such that nCr is maximum possible
void findPair(int arr[], int n)
{
    // Array should contain atleast 2 elements
    if (n < 2) {
        cout << "-1";
        return;
    }

    // Maximum element from the array
    int maximum = *max_element(arr, arr + n);

    // temp stores abs(middle - arr[i])
    int temp = 10000001, r = 0, middle = maximum / 2;

    // Finding r with minimum abs(middle - arr[i])
    for (int i = 0; i < n; i++) {

        // When n is even then middle is (maximum / 2)
        if (abs(middle - arr[i]) < temp && n % 2 == 0) {
            temp = abs(middle - arr[i]);
            r = arr[i];
        }

        // When n is odd then middle elements are
        // (maximum / 2) and ((maximum / 2) + 1)
        else if (min(abs(middle - arr[i]), abs(middle + 1 - arr[i])) < temp
                 && n % 2 == 1) {
            temp = min(abs(middle - arr[i]), abs(middle + 1 - arr[i]));
            r = arr[i];
        }
    }

    cout << "n = " << maximum
         << " and r = " << r;
}

// Driver code
int main()
{
    int arr[] = { 0, 2, 3, 4, 1, 6, 8, 9 };
    int n = sizeof(arr) / sizeof(arr[0]);

    findPair(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
class GFG
{

// Function to print the pair (n, r)
// such that nCr is maximum possible
static void findPair(int arr[], int n)
{
    // Array should contain atleast 2 elements
    if (n < 2)
    {
        System.out.print("-1");
        return;
    }

    // Maximum element from the array
    int maximum = arr[0];
    for(int i = 1; i < n; i++)
    maximum = Math.max(maximum, arr[i]);

    // temp stores abs(middle - arr[i])
    int temp = 10000001, r = 0, middle = maximum / 2;

    // Finding r with minimum abs(middle - arr[i])
    for (int i = 0; i < n; i++)
    {

        // When n is even then middle is (maximum / 2)
        if (Math.abs(middle - arr[i]) < temp && n % 2 == 0)
        {
            temp = Math.abs(middle - arr[i]);
            r = arr[i];
        }

        // When n is odd then middle elements are
        // (maximum / 2) and ((maximum / 2) + 1)
        else if (Math.min(Math.abs(middle - arr[i]),
                          Math.abs(middle + 1 - arr[i])) <
                                     temp && n % 2 == 1)
        {
            temp = Math.min(Math.abs(middle - arr[i]),
                            Math.abs(middle + 1 - arr[i]));
            r = arr[i];
        }
    }
    System.out.print( "n = " + maximum + " and r = " + r);
}

// Driver code
public static void main(String args[])
{
    int arr[] = { 0, 2, 3, 4, 1, 6, 8, 9 };
    int n = arr.length;

    findPair(arr, n);
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to print the pair (n, r)
# such that nCr is maximum possible

def find_pair(arr):

    current_min_diff = float('inf')
    n = max(arr)
    middle = n / 2

    for elem in arr:
        diff = abs(elem - middle)
        if diff < current_min_diff:
            current_min_diff = diff
            r = elem

    print("n =", n, "and r =", r)
    return r

# Driver code
if __name__ == "__main__":
    arr = [0, 2, 3, 4, 1, 6, 8, 9]
    # arr = [3,2,1.5]
    find_pair(arr)

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to print the pair (n, r)
// such that nCr is maximum possible
static void findPair(int []arr, int n)
{
    // Array should contain atleast 2 elements
    if (n < 2)
    {
        Console.Write("-1");
        return;
    }

    // Maximum element from the array
    int maximum = arr[0];
    for(int i = 1; i < n; i++)
    maximum = Math.Max(maximum, arr[i]);

    // temp stores abs(middle - arr[i])
    int temp = 10000001, r = 0, middle = maximum / 2;

    // Finding r with minimum abs(middle - arr[i])
    for (int i = 0; i < n; i++)
    {

        // When n is even then middle is (maximum / 2)
        if (Math.Abs(middle - arr[i]) < temp && n % 2 == 0)
        {
            temp = Math.Abs(middle - arr[i]);
            r = arr[i];
        }

        // When n is odd then middle elements are
        // (maximum / 2) and ((maximum / 2) + 1)
        else if (Math.Min(Math.Abs(middle - arr[i]),
                          Math.Abs(middle + 1 - arr[i])) <
                                   temp && n % 2 == 1)
        {
            temp = Math.Min(Math.Abs(middle - arr[i]),
                            Math.Abs(middle + 1 - arr[i]));
            r = arr[i];
        }
    }
    Console.Write( "n = " + maximum +
                   " and r = " + r);
}

// Driver code
public static void Main(String []args)
{
    int []arr = { 0, 2, 3, 4, 1, 6, 8, 9 };
    int n = arr.Length;

    findPair(arr, n);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Java  scriptimplementation of above approach

// Function to print the pair (n, r)
// such that nCr is maximum possible
function findPair(arr,n)
{
    // Array should contain atleast 2 elements
    if (n < 2)
    {
       document.write("-1");
        return;
    }

    // Maximum element from the array
    let maximum = arr[0];
    for(let i = 1; i < n; i++)
    maximum = Math.max(maximum, arr[i]);

    // temp stores abs(middle - arr[i])
    let temp = 10000001, r = 0, middle = maximum / 2;

    // Finding r with minimum abs(middle - arr[i])
    for (let i = 0; i < n; i++)
    {

        // When n is even then middle is (maximum / 2)
        if (Math.abs(middle - arr[i]) < temp && n % 2 == 0)
        {
            temp = Math.abs(middle - arr[i]);
            r = arr[i];
        }

        // When n is odd then middle elements are
        // (maximum / 2) and ((maximum / 2) + 1)
        else if (Math.min(Math.abs(middle - arr[i]),
                          Math.abs(middle + 1 - arr[i])) <
                                     temp && n % 2 == 1)
        {
            temp = Math.min(Math.abs(middle - arr[i]),
                            Math.abs(middle + 1 - arr[i]));
            r = arr[i];
        }
    }
    document.write( "n = " + maximum + " and r = " + r);
}

// Driver code

    let arr = [0, 2, 3, 4, 1, 6, 8, 9 ];
    let n = arr.length;

    findPair(arr, n);

// This code is contributed by sravan kumar
</script>
```

**Output:** 

```
n = 9 and r = 4
```