# 通过移除数组元素来计算奇数和偶数索引元素之和的方法

> 原文:[https://www . geeksforgeeks . org/count-way-通过移除数组元素使奇数和偶数索引元素之和相等/](https://www.geeksforgeeks.org/count-ways-to-make-sum-of-odd-and-even-indexed-elements-equal-by-removing-an-array-element/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)、 **arr[]** ，任务是找到数组索引的计数，使得从这些索引中移除一个元素使得偶数索引和奇数索引数组元素的总和相等。

**示例:**

> **输入:** arr[] = { 2，1，6，4 }
> **输出:** 1
> **解释:**
> 从数组中移除 arr[1]会将 arr[]修改为{ 2，6，4 }，这样，arr[0] + arr[2] = arr[1]。
> 因此，要求的输出为 1。
> 
> **输入:** arr[] = { 1，1，1 }
> **输出:** 3
> **解释:**
> 从给定数组中移除 arr[0]将 arr[]修改为{ 1，1 }，从而 arr[0] = arr[1]
> 从给定数组中移除 arr[1]将 arr[]修改为{ 1，1 }，从而 arr[0] = arr[1]
> 从给定数组中移除 arr[2]将 arr[]修改为{ 1，1 }

**天真方法:**解决这个问题最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个数组元素，检查从数组中移除元素是否使偶索引数组元素和奇索引数组元素的和相等。如果发现为真，则增加计数。最后，打印计数。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**有效方法:**上述方法可以基于以下观察进行优化，即从给定阵列中移除任何元素使得后续元素的偶数索引为奇数，后续元素的奇数索引为偶数。按照以下步骤解决问题:

*   初始化两个变量，比如 **evenSum** 和 **oddSum** ，分别存储给定数组的奇数索引和偶数索引元素的和。
*   [使用变量 **i** 遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)。
*   移除数组中的每一个**I**元素，并根据上述观察结果更新剩余的偶数索引元素和奇数索引元素的总和。检查总和是否相等。如果发现为真，则增加计数。
*   最后，打印获得的计数。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count array indices
// whose removal makes sum of odd and
// even indexed elements equal
int cntIndexesToMakeBalance(int arr[], int n)
{

    // If size of the array is 1
    if (n == 1) {
        return 1;
    }

    // If size of the array is 2
    if (n == 2)
        return 0;

    // Stores sum of even-indexed
    // elements of the given array
    int sumEven = 0;

    // Stores sum of odd-indexed
    // elements of the given array
    int sumOdd = 0;

    // Traverse the array
    for (int i = 0; i < n; i++) {

        // If i is an even number
        if (i % 2 == 0) {

            // Update sumEven
            sumEven += arr[i];
        }

        // If i is an odd number
        else {

            // Update sumOdd
            sumOdd += arr[i];
        }
    }

    // Stores sum of even-indexed
    // array elements till i-th index
    int currOdd = 0;

    // Stores sum of odd-indexed
    // array elements till i-th index
    int currEven = arr[0];

    // Stores count of indices whose
    // removal makes sum of odd and
    // even indexed elements equal
    int res = 0;

    // Stores sum of even-indexed elements
    // after removing the i-th element
    int newEvenSum = 0;

    // Stores sum of odd-indexed elements
    // after removing the i-th element
    int newOddSum = 0;

    // Traverse the array
    for (int i = 1; i < n - 1; i++) {

        // If i is an odd number
        if (i % 2) {

            // Update currOdd
            currOdd += arr[i];

            // Update newEvenSum
            newEvenSum = currEven + sumOdd
                         - currOdd;

            // Update newOddSum
            newOddSum = currOdd + sumEven
                        - currEven - arr[i];
        }

        // If i is an even number
        else {

            // Update currEven
            currEven += arr[i];

            // Update newOddSum
            newOddSum = currOdd + sumEven
                        - currEven;

            // Update newEvenSum
            newEvenSum = currEven + sumOdd
                         - currOdd - arr[i];
        }

        // If newEvenSum is equal to newOddSum
        if (newEvenSum == newOddSum) {

            // Increase the count
            res++;
        }
    }

    // If sum of even-indexed and odd-indexed
    // elements is equal by removing the first element
    if (sumOdd == sumEven - arr[0]) {

        // Increase the count
        res++;
    }

    // If length of the array
    // is an odd number
    if (n % 2 == 1) {

        // If sum of even-indexed and odd-indexed
        // elements is equal by removing the last element
        if (sumOdd == sumEven - arr[n - 1]) {

            // Increase the count
            res++;
        }
    }

    // If length of the array
    // is an even number
    else {

        // If sum of even-indexed and odd-indexed
        // elements is equal by removing the last element
        if (sumEven == sumOdd - arr[n - 1]) {

            // Increase the count
            res++;
        }
    }

    return res;
}

// Driver Code
int main()
{

    int arr[] = { 1, 1, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << cntIndexesToMakeBalance(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
class GFG {

    // Function to count array indices
    // whose removal makes sum of odd and
    // even indexed elements equal
    static int cntIndexesToMakeBalance(int arr[], int n)
    {

        // If size of the array is 1
        if (n == 1)
        {
            return 1;
        }

        // If size of the array is 2
        if (n == 2)
            return 0;

        // Stores sum of even-indexed
        // elements of the given array
        int sumEven = 0;

        // Stores sum of odd-indexed
        // elements of the given array
        int sumOdd = 0;

        // Traverse the array
        for (int i = 0; i < n; i++)
        {

            // If i is an even number
            if (i % 2 == 0)
            {

                // Update sumEven
                sumEven += arr[i];
            }

            // If i is an odd number
            else
            {

                // Update sumOdd
                sumOdd += arr[i];
            }
        }

        // Stores sum of even-indexed
        // array elements till i-th index
        int currOdd = 0;

        // Stores sum of odd-indexed
        // array elements till i-th index
        int currEven = arr[0];

        // Stores count of indices whose
        // removal makes sum of odd and
        // even indexed elements equal
        int res = 0;

        // Stores sum of even-indexed elements
        // after removing the i-th element
        int newEvenSum = 0;

        // Stores sum of odd-indexed elements
        // after removing the i-th element
        int newOddSum = 0;

        // Traverse the array
        for (int i = 1; i < n - 1; i++)
        {

            // If i is an odd number
            if (i % 2 != 0)
            {

                // Update currOdd
                currOdd += arr[i];

                // Update newEvenSum
                newEvenSum = currEven + sumOdd
                             - currOdd;

                // Update newOddSum
                newOddSum = currOdd + sumEven
                            - currEven - arr[i];
            }

            // If i is an even number
            else
            {

                // Update currEven
                currEven += arr[i];

                // Update newOddSum
                newOddSum = currOdd + sumEven
                            - currEven;

                // Update newEvenSum
                newEvenSum = currEven + sumOdd
                             - currOdd - arr[i];
            }

            // If newEvenSum is equal to newOddSum
            if (newEvenSum == newOddSum)
            {

                // Increase the count
                res++;
            }
        }

        // If sum of even-indexed and odd-indexed
        // elements is equal by removing the first element
        if (sumOdd == sumEven - arr[0])
        {

            // Increase the count
            res++;
        }

        // If length of the array
        // is an odd number
        if (n % 2 == 1)
        {

            // If sum of even-indexed and odd-indexed
            // elements is equal by removing the last element
            if (sumOdd == sumEven - arr[n - 1])
            {

                // Increase the count
                res++;
            }
        }

        // If length of the array
        // is an even number
        else
        {

            // If sum of even-indexed and odd-indexed
            // elements is equal by removing the last element
            if (sumEven == sumOdd - arr[n - 1])
            {

                // Increase the count
                res++;
            }
        }

        return res;
    }

    // Driver Code
   public static void main (String[] args)
    {  
        int arr[] = { 1, 1, 1 };
        int n = arr.length;
        System.out.println(cntIndexesToMakeBalance(arr, n));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to count array indices
# whose removal makes sum of odd and
# even indexed elements equal
def cntIndexesToMakeBalance(arr, n):

    # If size of the array is 1
    if (n == 1):
        return 1

    # If size of the array is 2
    if (n == 2):
        return 0

    # Stores sum of even-indexed
    # elements of the given array
    sumEven = 0

    # Stores sum of odd-indexed
    # elements of the given array
    sumOdd = 0

    # Traverse the array
    for i in range(n):

        # If i is an even number
        if (i % 2 == 0):

            # Update sumEven
            sumEven += arr[i]

        # If i is an odd number
        else:

            # Update sumOdd
            sumOdd += arr[i]

    # Stores sum of even-indexed
    # array elements till i-th index
    currOdd = 0

    # Stores sum of odd-indexed
    # array elements till i-th index
    currEven = arr[0]

    # Stores count of indices whose
    # removal makes sum of odd and
    # even indexed elements equal
    res = 0

    # Stores sum of even-indexed elements
    # after removing the i-th element
    newEvenSum = 0

    # Stores sum of odd-indexed elements
    # after removing the i-th element
    newOddSum = 0

    # Traverse the array
    for i in range(1, n - 1):

        # If i is an odd number
        if (i % 2):

            # Update currOdd
            currOdd += arr[i]

            # Update newEvenSum
            newEvenSum = (currEven + sumOdd -
                          currOdd)

            # Update newOddSum
            newOddSum = (currOdd + sumEven -
                        currEven - arr[i])

        # If i is an even number
        else:

            # Update currEven
            currEven += arr[i]

            # Update newOddSum
            newOddSum = (currOdd + sumEven -
                         currEven)

            # Update newEvenSum
            newEvenSum = (currEven + sumOdd -
                           currOdd - arr[i])

        # If newEvenSum is equal to newOddSum
        if (newEvenSum == newOddSum):

            # Increase the count
            res += 1

    # If sum of even-indexed and odd-indexed
    # elements is equal by removing the first
    # element
    if (sumOdd == sumEven - arr[0]):

        # Increase the count
        res += 1

    # If length of the array
    # is an odd number
    if (n % 2 == 1):

        # If sum of even-indexed and odd-indexed
        # elements is equal by removing the last
        # element
        if (sumOdd == sumEven - arr[n - 1]):

            # Increase the count
            res += 1

    # If length of the array
    # is an even number
    else:

        # If sum of even-indexed and odd-indexed
        # elements is equal by removing the last
        # element
        if (sumEven == sumOdd - arr[n - 1]):

            # Increase the count
            res += 1

    return res

# Driver Code
if __name__ == "__main__" :

    arr = [ 1, 1, 1 ]
    n = len(arr)

    print(cntIndexesToMakeBalance(arr, n))

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to implement
// the above approach 
using System;

class GFG {

    // Function to count array indices
    // whose removal makes sum of odd and
    // even indexed elements equal
    static int cntIndexesToMakeBalance(int[] arr, int n)
    {

        // If size of the array is 1
        if (n == 1)
        {
            return 1;
        }

        // If size of the array is 2
        if (n == 2)
            return 0;

        // Stores sum of even-indexed
        // elements of the given array
        int sumEven = 0;

        // Stores sum of odd-indexed
        // elements of the given array
        int sumOdd = 0;

        // Traverse the array
        for (int i = 0; i < n; i++)
        {

            // If i is an even number
            if (i % 2 == 0)
            {

                // Update sumEven
                sumEven += arr[i];
            }

            // If i is an odd number
            else
            {

                // Update sumOdd
                sumOdd += arr[i];
            }
        }

        // Stores sum of even-indexed
        // array elements till i-th index
        int currOdd = 0;

        // Stores sum of odd-indexed
        // array elements till i-th index
        int currEven = arr[0];

        // Stores count of indices whose
        // removal makes sum of odd and
        // even indexed elements equal
        int res = 0;

        // Stores sum of even-indexed elements
        // after removing the i-th element
        int newEvenSum = 0;

        // Stores sum of odd-indexed elements
        // after removing the i-th element
        int newOddSum = 0;

        // Traverse the array
        for (int i = 1; i < n - 1; i++)
        {

            // If i is an odd number
            if (i % 2 != 0)
            {

                // Update currOdd
                currOdd += arr[i];

                // Update newEvenSum
                newEvenSum = currEven + sumOdd
                             - currOdd;

                // Update newOddSum
                newOddSum = currOdd + sumEven
                            - currEven - arr[i];
            }

            // If i is an even number
            else
            {

                // Update currEven
                currEven += arr[i];

                // Update newOddSum
                newOddSum = currOdd + sumEven
                            - currEven;

                // Update newEvenSum
                newEvenSum = currEven + sumOdd
                             - currOdd - arr[i];
            }

            // If newEvenSum is equal to newOddSum
            if (newEvenSum == newOddSum)
            {

                // Increase the count
                res++;
            }
        }

        // If sum of even-indexed and odd-indexed
        // elements is equal by removing the first element
        if (sumOdd == sumEven - arr[0])
        {

            // Increase the count
            res++;
        }

        // If length of the array
        // is an odd number
        if (n % 2 == 1)
        {

            // If sum of even-indexed and odd-indexed
            // elements is equal by removing the last element
            if (sumOdd == sumEven - arr[n - 1])
            {

                // Increase the count
                res++;
            }
        }

        // If length of the array
        // is an even number
        else
        {

            // If sum of even-indexed and odd-indexed
            // elements is equal by removing the last element
            if (sumEven == sumOdd - arr[n - 1])
            {

                // Increase the count
                res++;
            }
        }

        return res;
    }

    // Drivers Code
    public static void Main ()
    {
        int[] arr = { 1, 1, 1 };
        int n = arr.Length;
        Console.WriteLine(cntIndexesToMakeBalance(arr, n));   
    }

}

// This code is contributed by susmitakundugoaldanga
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to count array indices
// whose removal makes sum of odd and
// even indexed elements equal
function cntIndexesToMakeBalance(arr, n)
{

    // If size of the array is 1
    if (n == 1) {
        return 1;
    }

    // If size of the array is 2
    if (n == 2)
        return 0;

    // Stores sum of even-indexed
    // elements of the given array
    let sumEven = 0;

    // Stores sum of odd-indexed
    // elements of the given array
    let sumOdd = 0;

    // Traverse the array
    for (let i = 0; i < n; i++) {

        // If i is an even number
        if (i % 2 == 0) {

            // Update sumEven
            sumEven += arr[i];
        }

        // If i is an odd number
        else {

            // Update sumOdd
            sumOdd += arr[i];
        }
    }

    // Stores sum of even-indexed
    // array elements till i-th index
    let currOdd = 0;

    // Stores sum of odd-indexed
    // array elements till i-th index
    let currEven = arr[0];

    // Stores count of indices whose
    // removal makes sum of odd and
    // even indexed elements equal
    let res = 0;

    // Stores sum of even-indexed elements
    // after removing the i-th element
    let newEvenSum = 0;

    // Stores sum of odd-indexed elements
    // after removing the i-th element
    let newOddSum = 0;

    // Traverse the array
    for (let i = 1; i < n - 1; i++) {

        // If i is an odd number
        if (i % 2) {

            // Update currOdd
            currOdd += arr[i];

            // Update newEvenSum
            newEvenSum = currEven + sumOdd
                        - currOdd;

            // Update newOddSum
            newOddSum = currOdd + sumEven
                        - currEven - arr[i];
        }

        // If i is an even number
        else {

            // Update currEven
            currEven += arr[i];

            // Update newOddSum
            newOddSum = currOdd + sumEven
                        - currEven;

            // Update newEvenSum
            newEvenSum = currEven + sumOdd
                        - currOdd - arr[i];
        }

        // If newEvenSum is equal to newOddSum
        if (newEvenSum == newOddSum) {

            // Increase the count
            res++;
        }
    }

    // If sum of even-indexed and odd-indexed
    // elements is equal by removing the first element
    if (sumOdd == sumEven - arr[0]) {

        // Increase the count
        res++;
    }

    // If length of the array
    // is an odd number
    if (n % 2 == 1) {

        // If sum of even-indexed and odd-indexed
        // elements is equal by removing the last element
        if (sumOdd == sumEven - arr[n - 1]) {

            // Increase the count
            res++;
        }
    }

    // If length of the array
    // is an even number
    else {

        // If sum of even-indexed and odd-indexed
        // elements is equal by removing the last element
        if (sumEven == sumOdd - arr[n - 1]) {

            // Increase the count
            res++;
        }
    }

    return res;
}

// Driver Code

    let arr = [ 1, 1, 1 ];
    let n = arr.length;
    document.write(cntIndexesToMakeBalance(arr, n));

// This code is contributed by Mayank Tyagi
</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)