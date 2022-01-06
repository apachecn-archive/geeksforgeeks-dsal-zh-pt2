# 通过给定的运算

找出是否有可能使数组的所有元素相等

> 原文:[https://www . geeksforgeeks . org/find-如果可能的话-通过给定的操作使数组的所有元素相等/](https://www.geeksforgeeks.org/find-if-it-is-possible-to-make-all-elements-of-an-array-equal-by-the-given-operations/)

给定一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是使所有[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)元素与给定操作相等。
在单次操作中，[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)的任意元素可以乘以 **3** 或乘以 **5** 任意次数。如果有可能使所有[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)元素与给定操作相等，则打印是否则打印号
**示例:**

> **输入:** arr[] = {18，30，54，90，162}
> **输出:**是
> **解释:**
> 我们可以执行以下操作:
> 162 X 5 = 810
> 90 X 3 X 3 = 810
> 54 X 5 X 3 = 810
> 30 X 3 X 3 X 3 = 810
> 18 X 5 X 3 X 3

**观察** :

*   如果在一些运算之后，所有的数变得相等，那么它们将具有相同的[素因子分解](https://www.geeksforgeeks.org/prime-factorization-using-sieve-olog-n-multiple-queries/)，即每个数将具有相同的 **2，3，5…** 的幂，以此类推。
*   由于我们只是将数字乘以[质数](https://www.geeksforgeeks.org/prime-numbers/)的 **3** 和 **5** ，所以经过一些运算后，我们可以使所有数字的质因数分解中 **3 和 5** 的幂相等。
*   因此，要使所有的数相等，除了 **3** 和 **5** 之外，素数因式分解中[的幂](https://www.geeksforgeeks.org/prime-numbers/)必须相等。
*   解决办法是取每个数字，去掉 **3** 和 **5** 的所有幂。如果所有的数字都相等，那么就有可能通过给定的运算使[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)元素相等，否则是不可能的。

**步骤**:T2

1.  将[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**的每个元素除以 3 和 5，使得每个元素的[素分解](https://www.geeksforgeeks.org/prime-factorization-using-sieve-olog-n-multiple-queries/)中 **3** 和 **5** 的所有幂都为零。
2.  检查[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)的所有元素是否相等。如果是，则打印是。
3.  否则打印号。

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation to find if it's
// possible to make all elements of an
// array equal by using two operations.
#include <bits/stdc++.h>
using namespace std;

// Function to find if it's possible
// to make all array elements equal
bool canMakeEqual(int a[], int n)
{
    // Iterate over all numbers
    for (int i = 0; i < n; i++) {

        // If a number has a power of 5
        // remove it
        while (a[i] % 5 == 0) {
            a[i] /= 5;
        }

        // If a number has a power of 3
        // remove it
        while (a[i] % 3 == 0) {
            a[i] /= 3;
        }
    }

    int last = a[0];

    // Check if all elements are equal
    // in the final array
    for (int i = 1; i < n; i++) {
        if (a[i] != last) {
            return false;
        }
    }

    return true;
}

// Driver's Code
int main()
{
    int arr[] = { 18, 30, 54, 90, 162 };

    int n = sizeof(arr) / sizeof(arr[0]);

    // Function call to check if all
    // element in the array can be equal
    // or not.
    if (canMakeEqual(arr, n)) {
        cout << "YES" << endl;
    }
    else {
        cout << "NO" << endl;
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find if it's
// possible to make all elements of an
// array equal by using two operations.
class GFG{

// Function to find if it's possible
// to make all array elements equal
static boolean canMakeEqual(int a[], int n)
{
    // Iterate over all numbers
    for (int i = 0; i < n; i++) {

        // If a number has a power of 5
        // remove it
        while (a[i] % 5 == 0) {
            a[i] /= 5;
        }

        // If a number has a power of 3
        // remove it
        while (a[i] % 3 == 0) {
            a[i] /= 3;
        }
    }

    int last = a[0];

    // Check if all elements are equal
    // in the final array
    for (int i = 1; i < n; i++) {
        if (a[i] != last) {
            return false;
        }
    }

    return true;
}

// Driver's Code
public static void main(String[] args)
{
    int arr[] = { 18, 30, 54, 90, 162 };

    int n = arr.length;

    // Function call to check if all
    // element in the array can be equal
    // or not.
    if (canMakeEqual(arr, n)) {
        System.out.print("YES" +"\n");
    }
    else {
        System.out.print("NO" +"\n");
    }
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation to find if it's
# possible to make all elements of an
# array equal by using two operations.

# Function to find if it's possible
# to make all array elements equal
def canMakeEqual( a, n) :

    # Iterate over all numbers
    for i in range(n) :

        # If a number has a power of 5
        # remove it
        while (a[i] % 5 == 0) :
            a[i] //= 5;

        # If a number has a power of 3
        # remove it
        while (a[i] % 3 == 0) :
            a[i] //= 3;

    last = a[0];

    # Check if all elements are equal
    # in the final array
    for i in range(1,n) :
        if (a[i] != last) :
            return False;

    return True;

# Driver's Code
if __name__ == "__main__" :

    arr = [ 18, 30, 54, 90, 162 ];

    n = len(arr);

    # Function call to check if all
    # element in the array can be equal
    # or not.
    if (canMakeEqual(arr, n)) :
        print("YES");

    else :
        print("NO");

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation to find if it's
// possible to make all elements of an
// array equal by using two operations.
using System;

class GFG{

// Function to find if it's possible
// to make all array elements equal
static bool canMakeEqual(int []a, int n)
{
    // Iterate over all numbers
    for (int i = 0; i < n; i++) {

        // If a number has a power of 5
        // remove it
        while (a[i] % 5 == 0) {
            a[i] /= 5;
        }

        // If a number has a power of 3
        // remove it
        while (a[i] % 3 == 0) {
            a[i] /= 3;
        }
    }

    int last = a[0];

    // Check if all elements are equal
    // in the final array
    for (int i = 1; i < n; i++) {
        if (a[i] != last) {
            return false;
        }
    }

    return true;
}

// Driver's Code
public static void Main(string[] args)
{
    int []arr = { 18, 30, 54, 90, 162 };

    int n = arr.Length;

    // Function call to check if all
    // element in the array can be equal
    // or not.
    if (canMakeEqual(arr, n)) {
        Console.WriteLine("YES");
    }
    else {
        Console.WriteLine("NO");
    }
}
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// javascript implementation to find if it's
// possible to make all elements of an
// array equal by using two operations.   
// Function to find if it's possible
    // to make all array elements equal
    function canMakeEqual(a , n) {
        // Iterate over all numbers
        for (i = 0; i < n; i++) {

            // If a number has a power of 5
            // remove it
            while (a[i] % 5 == 0) {
                a[i] /= 5;
            }

            // If a number has a power of 3
            // remove it
            while (a[i] % 3 == 0) {
                a[i] /= 3;
            }
        }

        var last = a[0];

        // Check if all elements are equal
        // in the final array
        for (i = 1; i < n; i++) {
            if (a[i] != last) {
                return false;
            }
        }

        return true;
    }

    // Driver's Code

        var arr = [ 18, 30, 54, 90, 162 ];

        var n = arr.length;

        // Function call to check if all
        // element in the array can be equal
        // or not.
        if (canMakeEqual(arr, n)) {
            document.write("YES" + "\n");
        } else {
            document.write("NO" + "\n");
        }

// This code contributed by umadevi9616
</script>
```

**Output:** 

```
YES
```

**时间复杂度:** O(N)，其中 N 是数组的大小。