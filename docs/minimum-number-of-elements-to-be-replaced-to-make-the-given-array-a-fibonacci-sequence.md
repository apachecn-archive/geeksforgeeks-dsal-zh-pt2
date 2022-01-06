# 使给定数组成为斐波那契数列的最小替换元素数

> 原文:[https://www . geeksforgeeks . org/要替换的最小元素数以构成给定的斐波那契数列数组/](https://www.geeksforgeeks.org/minimum-number-of-elements-to-be-replaced-to-make-the-given-array-a-fibonacci-sequence/)

给定一个包含 *N* 整数元素的数组 *arr* ，任务是计算需要更改的元素的最小数量，以便所有元素(经过适当的重新排列)首先成为斐波那契数列的 *N* 项。
**举例:**

> **输入:** arr[] = {4，1，2，1，3，7}
> **输出:** 2
> 4 和 7 必须改为 5 和 8 才能构成斐波那契数列的前 N(6)项。
> **输入:** arr[] = {5，3，1，1，2，8，11}
> **输出:** 1
> 11 必须改为 13。

**进场:**

*   将斐波那契数列的前 N 个元素插入到多集合中。
*   然后，从左到右遍历数组，检查当前元素是否存在于多集合中。
*   如果元素存在于多重集合中，则将其移除。
*   最终答案将是最终多组的大小。

以下是上述方法的实现:

## C++

```
// C++ program to find the minimum number
// of elements the need to be changed
// to get first N numbers of Fibonacci series
#include <bits/stdc++.h>
using namespace std;

// Function that finds minimum changes required
int fibonacciArray(int arr[], int n)
{
    multiset<int> s;

    // a and b are first two
    // fibonacci numbers
    int a = 1, b = 1;
    int c;

    // insert first n fibonacci elements to set
    s.insert(a);
    if (n >= 2)
        s.insert(b);

    for (int i = 0; i < n - 2; i++) {
        c = a + b;
        s.insert(c);
        a = b;
        b = c;
    }

    multiset<int>::iterator it;
    for (int i = 0; i < n; i++) {

        // if fibonacci element is present
        // in the array then remove it from set
        it = s.find(arr[i]);
        if (it != s.end())
            s.erase(it);
    }

    // return the remaining number of
    // elements in the set
    return s.size();
}

// Driver code
int main()
{
    int arr[] = { 3, 1, 21, 4, 2, 1, 8, 9 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << fibonacciArray(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the minimum number
// of elements the need to be changed
// to get first N numbers of Fibonacci series
import java.util.*;

class geeks
{

    // Function that finds minimum changes required
    public static int fibonacciArray(int[] arr, int n)
    {
        Set<Integer> s = new HashSet<Integer>();

        // a and b are first two
        // fibonacci numbers
        int a = 1, b = 1;
        int c;

        // insert first n fibonacci elements to set
        s.add(a);
        if (n > 2)
            s.add(b);

        for (int i = 0; i < n - 2; i++)
        {
            c = a + b;
            s.add(c);
            a = b;
            b = c;
        }

        for (int i = 0; i < n; i++)
        {

            // if fibonacci element is present
            // in the array then remove it from set
            if (s.contains(arr[i]))
                s.remove(arr[i]);
        }

        // return the remaining number of
        // elements in the set
        return s.size();
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = { 3, 1, 21, 4, 2, 1, 8, 9 };
        int n = arr.length;

        System.out.print(fibonacciArray(arr, n));
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 program to find the minimum number
# of elements the need to be changed
# to get first N numbers of Fibonacci series

# Function that finds minimum changes required
def fibonacciArray(arr, n):

    s = set()

    # a and b are first two
    # fibonacci numbers
    a, b = 1, 1

    # insert first n fibonacci elements to set
    s.add(a)
    if n >= 2:
        s.add(b)

    for i in range(0, n - 2):
        c = a + b
        s.add(c)
        a, b = b, c

    for i in range(0, n):

        # if fibonacci element is present in
        # the array then remove it from set
        if arr[i] in s:
            s.remove(arr[i])

    # return the remaining number
    # of elements in the set
    return len(s)

# Driver code
if __name__ == "__main__":

    arr = [3, 1, 21, 4, 2, 1, 8, 9]
    n = len(arr)

    print(fibonacciArray(arr, n))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to find the minimum number
// of elements the need to be changed
// to get first N numbers of Fibonacci series
using System;
using System.Collections.Generic;

public class geeks
{

    // Function that finds minimum changes required
    public static int fibonacciArray(int[] arr, int n)
    {
        HashSet<int> s = new HashSet<int>();

        // a and b are first two
        // fibonacci numbers
        int a = 1, b = 1;
        int c;

        // insert first n fibonacci elements to set
        s.Add(a);
        if (n > 2)
            s.Add(b);

        for (int i = 0; i < n - 2; i++)
        {
            c = a + b;
            s.Add(c);
            a = b;
            b = c;
        }

        for (int i = 0; i < n; i++)
        {

            // if fibonacci element is present
            // in the array then remove it from set
            if (s.Contains(arr[i]))
                s.Remove(arr[i]);
        }

        // return the remaining number of
        // elements in the set
        return s.Count;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int[] arr = { 3, 1, 21, 4, 2, 1, 8, 9 };
        int n = arr.Length;

        Console.WriteLine(fibonacciArray(arr, n));
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript program to find the minimum number
// of elements the need to be changed
// to get first N numbers of Fibonacci series

// Function that finds minimum changes required
function fibonacciArray(arr, n) {
    let s = new Set();

    // a and b are first two
    // fibonacci numbers
    let a = 1, b = 1;
    let c;

    // insert first n fibonacci elements to set
    s.add(a);
    if (n > 2)
        s.add(b);

    for (let i = 0; i < n - 2; i++) {
        c = a + b;
        s.add(c);
        a = b;
        b = c;
    }

    for (let i = 0; i < n; i++) {

        // if fibonacci element is present
        // in the array then remove it from set
        if (s.has(arr[i]))
            s.delete(arr[i]);
    }

    // return the remaining number of
    // elements in the set
    return s.size;
}

// Driver Code

let arr = [3, 1, 21, 4, 2, 1, 8, 9];
let n = arr.length;

document.write(fibonacciArray(arr, n));

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
2
```