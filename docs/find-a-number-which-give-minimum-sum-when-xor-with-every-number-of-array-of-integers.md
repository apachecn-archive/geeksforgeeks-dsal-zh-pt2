# 求一个数，当与整数数组的每个数进行异或运算时，该数给出最小和

> 原文:[https://www . geeksforgeeks . org/find-a-number-给出整数数组的每一个数字异或时的最小和/](https://www.geeksforgeeks.org/find-a-number-which-give-minimum-sum-when-xor-with-every-number-of-array-of-integers/)

给定一个非负整数的数组 **arr[]** ，任务是找到一个整数 **X** ，使得 **(arr[0]异或 X) + (arr[1]异或 X)+…+arr[n–1]异或 X** 最小。
**举例:**

> **输入:** arr[] = {3，9，6，2，4}
> **输出:** X = 2，Sum = 22
> **输入:** arr[] = {6，56，78，34}
> **输出:** X = 2，Sum = 170

**方法:**我们将检查二进制表示的数组中每个数字的第**【I】**位，并对包含设置为**【1】**的第**【I】**位的那些数字进行计数，因为这些设置位将有助于最大化和而不是最小化。所以我们必须将第**“I”**位设置为**“0”**如果计数大于 N/2，并且如果计数小于 N/2，那么具有第**“I”**位设置的数字较少，因此不会影响答案。根据对两位的异或运算，我们知道当 A 异或 B 和 A 与 B 都相同时，那么它给出的结果为**‘0’**，所以我们将使我们的数(num)中的第**‘I’**位变为**‘1’**，这样(1 异或 1)将给出**‘0’**并最小化和。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
#include <cmath>
using namespace std;

// Function to find an integer X such that
// the sum of all the array elements after
// getting XORed with X is minimum
void findX(int arr[], int n)
{
    // Finding Maximum element of array
    int* itr = max_element(arr, arr + n);

    // Find Maximum number of bits required
    // in the binary representation
    // of maximum number
    // so log2 is calculated
    int p = log2(*itr) + 1;

    // Running loop from p times which is
    // the number of bits required to represent
    // all the elements of the array
    int X = 0;
    for (int i = 0; i < p; i++) {
        int count = 0;
        for (int j = 0; j < n; j++) {

            // If the bits in same position are set
            // then count
            if (arr[j] & (1 << i)) {
                count++;
            }
        }

        // If count becomes greater than half of
        // size of array then we need to make
        // that bit '0' by setting X bit to '1'
        if (count > (n / 2)) {

            // Again using shift operation to calculate
            // the required number
            X += 1 << i;
        }
    }

    // Calculate minimized sum
    long long int sum = 0;
    for (int i = 0; i < n; i++)
        sum += (X ^ arr[i]);

    // Print solution
    cout << "X = " << X << ", Sum = " << sum;
}

// Driver code
int main()
{
    int arr[] = { 2, 3, 4, 5, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);

    findX(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.lang.Math;
import java.util.*;

class GFG
{
    // Function to find an integer X such that
    // the sum of all the array elements after
    // getting XORed with X is minimum
    public static void findX(int[] a, int n)
    {

        // Finding Maximum element of array
        Collections.sort(Arrays.asList(a), null);
        int itr = a[n-1];

        // Find Maximum number of bits required
        // in the binary representation
        // of maximum number
        // so log2 is calculated
        int p = (int)(Math.log(itr)/Math.log(2)) + 1;

        // Running loop from p times which is
        // the number of bits required to represent
        // all the elements of the array
        int x = 0;
        for (int i = 0; i < p; i++)
        {
            int count = 0;
            for (int j = 0; j < n; j++)
            {

                // If the bits in same position are set
                // then count
                if ((a[j] & (1 << i)) != 0)
                    count++;
            }

            // If count becomes greater than half of
            // size of array then we need to make
            // that bit '0' by setting X bit to '1'
            if (count > (n / 2))
            {

                // Again using shift operation to calculate
                // the required number
                x += 1 << i;
            }
        }

        // Calculate minimized sum
        long sum = 0;
        for (int i = 0; i < n; i++)
            sum += (x ^ a[i]);

        // Print solution
        System.out.println("X = " + x + ", Sum = " + sum);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] a = {2, 3, 4, 5, 6};
        int n = a.length;

        findX(a, n);
    }

}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python 3 implementation of the approach
from math import log2

# Function to find an integer X such that
# the sum of all the array elements after
# getting XORed with X is minimum
def findX(arr, n):

    # Finding Maximum element of array
    itr = arr[0]
    for i in range(len(arr)):

        # Find Maximum number of bits required
        # in the binary representation
        # of maximum number
        # so log2 is calculated
        if(arr[i] > itr):
            itr = arr[i]

    p = int(log2(itr)) + 1

    # Running loop from p times which is
    # the number of bits required to represent
    # all the elements of the array
    X = 0
    for i in range(p):
        count = 0
        for j in range(n):

            # If the bits in same position are set
            # then increase count
            if (arr[j] & (1 << i)):
                count += 1

        # If count becomes greater than half of
        # size of array then we need to make
        # that bit '0' by setting X bit to '1'
        if (count > int(n / 2)):

            # Again using shift operation to calculate
            # the required number
            X += 1 << i

    # Calculate minimized sum
    sum = 0
    for i in range(n):
        sum += (X ^ arr[i])

    # Print solution
    print("X =", X, ", Sum =", sum)

# Driver code
if __name__=='__main__':
    arr = [2, 3, 4, 5, 6]
    n = len(arr)
    findX(arr, n)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of above approach
using System;
using System.Linq;

class GFG
{
    // Function to find an integer X such that
    // the sum of all the array elements after
    // getting XORed with X is minimum
    public static void findX(int[] a, int n)
    {

        // Finding Maximum element of array
        int itr = a.Max();

        // Find Maximum number of bits required
        // in the binary representation
        // of maximum number
        // so log2 is calculated
        int p = (int) Math.Log(itr, 2) + 1;

        // Running loop from p times which is
        // the number of bits required to represent
        // all the elements of the array
        int x = 0;
        for (int i = 0; i < p; i++)
        {
            int count = 0;
            for (int j = 0; j < n; j++)
            {

                // If the bits in same position are set
                // then count
                if ((a[j] & (1 << i)) != 0)
                    count++;
            }

            // If count becomes greater than half of
            // size of array then we need to make
            // that bit '0' by setting X bit to '1'
            if (count > (n / 2))
            {

                // Again using shift operation to calculate
                // the required number
                x += 1 << i;
            }
        }

        // Calculate minimized sum
        long sum = 0;
        for (int i = 0; i < n; i++)
            sum += (x ^ a[i]);

        // Print solution
        Console.Write("X = " + x + ", Sum = " + sum);
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int[] a = {2, 3, 4, 5, 6};
        int n = a.Length;

        findX(a, n);
    }

}

// This code is contributed by ravikishor
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to find an integer X such that
// the sum of all the array elements after
// getting XORed with X is minimum
function findX(arr, n)
{
    // Finding Maximum element of array
    let itr = Math.max(...arr);

    // Find Maximum number of bits required
    // in the binary representation
    // of maximum number
    // so log2 is calculated
    let p = parseInt(Math.log(itr) / Math.log(2)) + 1;

    // Running loop from p times which is
    // the number of bits required to represent
    // all the elements of the array
    let X = 0;
    for (let i = 0; i < p; i++) {
        let count = 0;
        for (let j = 0; j < n; j++) {

            // If the bits in same position are set
            // then count
            if (arr[j] & (1 << i)) {
                count++;
            }
        }

        // If count becomes greater than half of
        // size of array then we need to make
        // that bit '0' by setting X bit to '1'
        if (count > parseInt(n / 2)) {

            // Again using shift
            // operation to calculate
            // the required number
            X += 1 << i;
        }
    }

    // Calculate minimized sum
    let sum = 0;
    for (let i = 0; i < n; i++)
        sum += (X ^ arr[i]);

    // Print solution
    document.write("X = " + X + ", Sum = " + sum);
}

// Driver code

    let arr = [ 2, 3, 4, 5, 6 ];
    let n = arr.length;

    findX(arr, n);

</script>
```

**Output:** 

```
X = 6, Sum = 14
```

**时间复杂度:** O(N * log(A))
**辅助空间:** O(1)