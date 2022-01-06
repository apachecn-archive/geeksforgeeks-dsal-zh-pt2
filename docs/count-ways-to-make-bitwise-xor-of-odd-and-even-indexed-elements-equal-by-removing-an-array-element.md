# 计数通过移除数组元素使奇数和偶数索引元素的按位异或相等的方法

> 原文:[https://www . geeksforgeeks . org/count-way-to-make-by-by-way-to-by-to-by-count-way-to-by-to-by-to-to-to-to-to-to-to-to-to-to-to-to-to-to-to-to-to-to-to-to-to-to-to-to-to-](https://www.geeksforgeeks.org/count-ways-to-make-bitwise-xor-of-odd-and-even-indexed-elements-equal-by-removing-an-array-element/)

给定一个长度为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是找到数组索引的计数，以便从这些索引中移除一个元素使得奇数索引元素和偶数索引(基于 1 的索引)元素的[按位异或相等。](https://www.geeksforgeeks.org/find-xor-of-all-elements-in-an-array/)

**示例:**

> **输入:** arr[] = {1，0，1，0，1}，N = 5
> T3】输出:3
> T6】解释:
> 
> 1.  从索引 3 中删除元素会将 arr[]修改为{1，0，0，1}。因此，奇数和偶数索引元素的 xor 为 0。
> 2.  从索引 1 中删除元素会将 arr[]修改为{0，1，0，1}。因此，奇数和偶数索引元素的 xor 为 0。
> 3.  从索引 5 中删除元素会将 arr[]修改为{1，0，1，0}。因此，奇数和偶数索引元素的 xor 为 0。
> 
> **输入:** arr[] = {1，0，0，0，1}，N = 5
> T3】输出: 3
> 
> 1.  从索引 3 中删除元素会将 arr[]修改为{1，0，0，1}。因此，奇数和偶数索引元素的 xor 为 0。
> 2.  从索引 2 中删除元素会将 arr[]修改为{1，0，0，1}。因此，奇数和偶数索引元素的 xor 为 1。
> 3.  从索引 4 中删除元素会将 arr[]修改为{1，0，0，0}。因此，奇数和偶数索引元素的 xor 为 1。

**天真方法:**解决这个问题最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个数组元素，检查从数组中移除元素是否使偶索引和奇索引数组元素的**按位异或**相等。如果发现为真，则增加计数。最后，打印计数。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**有效方法:**上述方法可以基于以下观察进行优化，即从给定阵列中移除任何元素使得后续元素的偶数索引为奇数，后续元素的奇数索引为偶数。按照以下步骤解决问题:

1.  用 **0** 初始化变量**curr _ 奇数、curr _ 偶数、post _ 奇数、post _ 偶数、**和 **res** 。
2.  [反向遍历阵列](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，并执行以下操作:
    *   如果当前元素为奇数，则与**后 _ 奇数**异或。
    *   否则，将电流元件与**后偶**异或。
3.  现在，[遍历给定的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并执行以下操作:
    *   如果当前索引为奇数，则通过用 **post_odd** 和当前元素的**按位异或**更新 **post_odd** ，从 **post_odd** 中移除当前元素。
    *   否则，同样从 **post_even** 中移除当前元素。
    *   初始化变量 **X** 和 **Y** 。
    *   将 **X** 中的**curr _ 奇数**和**post _ 偶数**进行异或运算。因此， **X** 存储所有奇数索引元素的异或。
    *   将 **Y** 中的**curr _ 偶数**和**post _ 奇数**进行异或运算。因此， **Y** 存储所有偶数索引元素的异或。
    *   检查 **X** 是否等于 **Y** 。如果发现为真，将 **res** 增加 **1** 。
    *   如果当前索引为奇数，则用 **curr_odd** 异或当前元素。
    *   否则，将电流元件与**电流偶**进行异或运算。
4.  最后，打印 **res** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count ways to make Bitwise
// XOR of odd and even indexed elements
// equal by removing an array element
void Remove_one_element(int arr[], int n)
{
    // Stores xor of odd and even
    // indexed elements from the end
    int post_odd = 0, post_even = 0;

    // Stores xor of odd and even
    // indexed elements from the start
    int curr_odd = 0, curr_even = 0;

    // Stores the required count
    int res = 0;

    // Traverse the array in reverse
    for (int i = n - 1; i >= 0; i--) {

        // If i is odd
        if (i % 2)
            post_odd ^= arr[i];

        // If i is even
        else
            post_even ^= arr[i];
    }

    // Traverse the array
    for (int i = 0; i < n; i++) {

        // If i is odd
        if (i % 2)
            post_odd ^= arr[i];

        // If i is even
        else
            post_even ^= arr[i];

        // Removing arr[i], post_even stores
        // XOR of odd indexed elements
        int X = curr_odd ^ post_even;

        // Removing arr[i], post_odd stores
        // XOR of even indexed elements
        int Y = curr_even ^ post_odd;

        // Check if they are equal
        if (X == Y)
            res++;

        // If i is odd, xor it
        // with curr_odd
        if (i % 2)
            curr_odd ^= arr[i];

        // If i is even, xor it
        // with curr_even
        else
            curr_even ^= arr[i];
    }

    // Finally print res
    cout << res << endl;
}

// Drivers Code
int main()
{

    // Given array
    int arr[] = { 1, 0, 1, 0, 1 };

    // Given size
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call
    Remove_one_element(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG {

    // Function to count ways to make Bitwise
    // XOR of odd and even indexed elements
    // equal by removing an array element
    static void Remove_one_element(int arr[], int n)
    {
        // Stores xor of odd and even
        // indexed elements from the end
        int post_odd = 0, post_even = 0;

        // Stores xor of odd and even
        // indexed elements from the start
        int curr_odd = 0, curr_even = 0;

        // Stores the required count
        int res = 0;

        // Traverse the array in reverse
        for (int i = n - 1; i >= 0; i--)
        {

            // If i is odd
            if (i % 2 != 0)
                post_odd ^= arr[i];

            // If i is even
            else
                post_even ^= arr[i];
        }

        // Traverse the array
        for (int i = 0; i < n; i++)
        {

            // If i is odd
            if (i % 2 != 0)
                post_odd ^= arr[i];

            // If i is even
            else
                post_even ^= arr[i];

            // Removing arr[i], post_even stores
            // XOR of odd indexed elements
            int X = curr_odd ^ post_even;

            // Removing arr[i], post_odd stores
            // XOR of even indexed elements
            int Y = curr_even ^ post_odd;

            // Check if they are equal
            if (X == Y)
                res++;

            // If i is odd, xor it
            // with curr_odd
            if (i % 2 != 0)
                curr_odd ^= arr[i];

            // If i is even, xor it
            // with curr_even
            else
                curr_even ^= arr[i];
        }

        // Finally print res
        System.out.println(res);
    }

    // Drivers Code
    public static void main (String[] args)
    {

        // Given array
        int arr[] = { 1, 0, 1, 0, 1 };

        // Given size
        int N = arr.length;

        // Function call
        Remove_one_element(arr, N);   
    }

}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count ways to make Bitwise
# XOR of odd and even indexed elements
# equal by removing an array element
def Remove_one_element(arr, n):

    # Stores xor of odd and even
    # indexed elements from the end
    post_odd = 0
    post_even = 0

    # Stores xor of odd and even
    # indexed elements from the start
    curr_odd = 0
    curr_even = 0

    # Stores the required count
    res = 0

    # Traverse the array in reverse
    for i in range(n - 1, -1, -1):

        # If i is odd
        if (i % 2):
            post_odd ^= arr[i]

        # If i is even
        else:
            post_even ^= arr[i]

    # Traverse the array
    for i in range(n):

        # If i is odd
        if (i % 2):
            post_odd ^= arr[i]

        # If i is even
        else:
            post_even ^= arr[i]

        # Removing arr[i], post_even stores
        # XOR of odd indexed elements
        X = curr_odd ^ post_even

        # Removing arr[i], post_odd stores
        # XOR of even indexed elements
        Y = curr_even ^ post_odd

        # Check if they are equal
        if (X == Y):
            res += 1

        # If i is odd, xor it
        # with curr_odd
        if (i % 2):
            curr_odd ^= arr[i]

        # If i is even, xor it
        # with curr_even
        else:
            curr_even ^= arr[i]

    # Finally print res
    print(res)

# Drivers Code
if __name__ == "__main__" :

    # Given array
    arr = [ 1, 0, 1, 0, 1 ]

    # Given size
    N = len(arr)

    # Function call
    Remove_one_element(arr, N)

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to implement
// the above approach 
using System;

class GFG {

    // Function to count ways to make Bitwise
    // XOR of odd and even indexed elements
    // equal by removing an array element
    static void Remove_one_element(int[] arr, int n)
    {
        // Stores xor of odd and even
        // indexed elements from the end
        int post_odd = 0, post_even = 0;

        // Stores xor of odd and even
        // indexed elements from the start
        int curr_odd = 0, curr_even = 0;

        // Stores the required count
        int res = 0;

        // Traverse the array in reverse
        for (int i = n - 1; i >= 0; i--)
        {

            // If i is odd
            if (i % 2 != 0)
                post_odd ^= arr[i];

            // If i is even
            else
                post_even ^= arr[i];
        }

        // Traverse the array
        for (int i = 0; i < n; i++)
        {

            // If i is odd
            if (i % 2 != 0)
                post_odd ^= arr[i];

            // If i is even
            else
                post_even ^= arr[i];

            // Removing arr[i], post_even stores
            // XOR of odd indexed elements
            int X = curr_odd ^ post_even;

            // Removing arr[i], post_odd stores
            // XOR of even indexed elements
            int Y = curr_even ^ post_odd;

            // Check if they are equal
            if (X == Y)
                res++;

            // If i is odd, xor it
            // with curr_odd
            if (i % 2 != 0)
                curr_odd ^= arr[i];

            // If i is even, xor it
            // with curr_even
            else
                curr_even ^= arr[i];
        }

        // Finally print res
        Console.WriteLine(res);
    }

    // Drivers Code
    public static void Main ()
    {

        // Given array
        int[] arr = { 1, 0, 1, 0, 1 };

        // Given size
        int N = arr.Length;

        // Function call
        Remove_one_element(arr, N);   
    }

}

// This code is contributed by susmitakundugoaldanga
```

## java 描述语言

```
<script>
// JavaScript program to implement
// the above approach

    // Function to count ways to make Bitwise
    // XOR of odd and even indexed elements
    // equal by removing an array element
    function Remove_one_element(arr, n)
    {
        // Stores xor of odd and even
        // indexed elements from the end
        let post_odd = 0, post_even = 0;

        // Stores xor of odd and even
        // indexed elements from the start
        let curr_odd = 0, curr_even = 0;

        // Stores the required count
        let res = 0;

        // Traverse the array in reverse
        for (let i = n - 1; i >= 0; i--)
        {

            // If i is odd
            if (i % 2 != 0)
                post_odd ^= arr[i];

            // If i is even
            else
                post_even ^= arr[i];
        }

        // Traverse the array
        for (let i = 0; i < n; i++)
        {

            // If i is odd
            if (i % 2 != 0)
                post_odd ^= arr[i];

            // If i is even
            else
                post_even ^= arr[i];

            // Removing arr[i], post_even stores
            // XOR of odd indexed elements
            let X = curr_odd ^ post_even;

            // Removing arr[i], post_odd stores
            // XOR of even indexed elements
            let Y = curr_even ^ post_odd;

            // Check if they are equal
            if (X == Y)
                res++;

            // If i is odd, xor it
            // with curr_odd
            if (i % 2 != 0)
                curr_odd ^= arr[i];

            // If i is even, xor it
            // with curr_even
            else
                curr_even ^= arr[i];
        }

        // Finally print res
        document.write(res);
    }

// Driver Code

    // Given array
        let arr = [ 1, 0, 1, 0, 1 ];

        // Given size
        let N = arr.length;

        // Function call
        Remove_one_element(arr, N);

</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)