# 使所有数组元素相等所需翻转的数组元素的最小位数

> 原文:[https://www . geesforgeks . org/最小数组元素位数-需要翻转才能使所有数组元素相等/](https://www.geeksforgeeks.org/minimum-number-of-bits-of-array-elements-required-to-be-flipped-to-make-all-array-elements-equal/)

给定一个由 **N** 个正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找到需要翻转的数组元素的最小位数，使[个数组元素相等](https://www.geeksforgeeks.org/all-elements-in-an-array-are-same-or-not/)。

**示例:**

> **输入:** arr[] = {3，5}
> **输出:** 2
> **解释:**
> 以下是所需数组元素位的翻转:
> 
> *   **对于元素 arr[0](= 3):** 从右侧翻转第三位将 arr[0]修改为(= 7(111) <sub>2</sub> 。现在，数组变成了{7，5}。
> *   **对于元素 arr[0](= 7):** 从右侧翻转第二位将 arr[0]修改为 5 (= (101) <sub>2</sub> )。现在，数组变成了{5，5}。
> 
> 执行上述操作后，所有数组元素都是相等的。因此，所需的位翻转总数为 2。
> 
> **输入:** arr[] = {4，6，3，4，5}
> **输出:** 5

**方法:**给定的问题可以通过修改数组元素来解决，修改方式是在所有数组元素之间的每个位置设置位和未设置位的数量。按照以下步骤解决问题:

*   初始化两个频率数组，大小为**32**[的**fre0【】**和**fre1【】**对数组元素的每一位](https://www.geeksforgeeks.org/count-frequencies-elements-array-o1-extra-space-time/)计数 0 和 1 的频率。
*   [遍历给定的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个数组元素， **arr[i]** 如果 **arr[i]** 的 **j <sup>第</sup>T7】位是[设置位](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)，那么将**fre1【j】**的频率增加 **1** 。否则，将 **fre0[j]** 的频率增加 **1** 。**
*   完成上述步骤后，打印范围**【0，32】**内每一位 **i** 的**fre0【I】**和**fre1【I】**的最小值之和。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count minimum number
// of bits required to be flipped
// to make all array elements equal
int makeEqual(int* arr, int n)
{
    // Stores the count of unset bits
    int fre0[33] = { 0 };

    // Stores the count of set bits
    int fre1[33] = { 0 };

    // Traverse the array
    for (int i = 0; i < n; i++) {

        int x = arr[i];

        // Traverse the bit of arr[i]
        for (int j = 0; j < 33; j++) {

            // If current bit is set
            if (x & 1) {

                // Increment fre1[j]
                fre1[j] += 1;
            }

            // Otherwise
            else {

                // Increment fre0[j]
                fre0[j] += 1;
            }

            // Right shift x by 1
            x = x >> 1;
        }
    }

    // Stores the count of total moves
    int ans = 0;

    // Traverse the range [0, 32]
    for (int i = 0; i < 33; i++) {

        // Update the value of ans
        ans += min(fre0[i], fre1[i]);
    }

    // Return the minimum number of
    // flips required
    return ans;
}

// Driver Code
int main()
{
    int arr[] = { 3, 5 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << makeEqual(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Function to count minimum number
// of bits required to be flipped
// to make all array elements equal
static int makeEqual(int arr[], int n)
{

    // Stores the count of unset bits
    int fre0[] = new int[33];

    // Stores the count of set bits
    int fre1[] = new int[33];

    // Traverse the array
    for(int i = 0; i < n; i++)
    {
        int x = arr[i];

        // Traverse the bit of arr[i]
        for(int j = 0; j < 33; j++)
        {

            // If current bit is set
            if ((x & 1) != 0)
            {

                // Increment fre1[j]
                fre1[j] += 1;
            }

            // Otherwise
            else
            {

                // Increment fre0[j]
                fre0[j] += 1;
            }

            // Right shift x by 1
            x = x >> 1;
        }
    }

    // Stores the count of total moves
    int ans = 0;

    // Traverse the range [0, 32]
    for(int i = 0; i < 33; i++)
    {

        // Update the value of ans
        ans += Math.min(fre0[i], fre1[i]);
    }

    // Return the minimum number of
    // flips required
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 3, 5 };
    int N = arr.length;

    System.out.print(makeEqual(arr, N));
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count minimum number
# of bits required to be flipped
# to make all array elements equal
def makeEqual(arr, n):

    # Stores the count of unset bits
    fre0 = [0]*33

    # Stores the count of set bits
    fre1 = [0]*33

    # Traverse the array
    for i in range(n):

        x = arr[i]

        # Traverse the bit of arr[i]
        for j in range(33):

            # If current bit is set
            if (x & 1):
                # Increment fre1[j]
                fre1[j] += 1
            # Otherwise
            else:
                # Increment fre0[j]
                fre0[j] += 1
            # Right shift x by 1
            x = x >> 1

    # Stores the count of total moves
    ans = 0

    # Traverse the range [0, 32]
    for i in range(33):

        # Update the value of ans
        ans += min(fre0[i], fre1[i])

    # Return the minimum number of
    # flips required
    return ans

# Driver Code
if __name__ == '__main__':
    arr= [3, 5]
    N = len(arr)
    print(makeEqual(arr, N))

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
class GFG {

    // Function to count minimum number
    // of bits required to be flipped
    // to make all array elements equal
    static int makeEqual(int[] arr, int n)
    {

        // Stores the count of unset bits
        int[] fre0 = new int[33];

        // Stores the count of set bits
        int[] fre1 = new int[33];

        // Traverse the array
        for (int i = 0; i < n; i++) {
            int x = arr[i];

            // Traverse the bit of arr[i]
            for (int j = 0; j < 33; j++) {

                // If current bit is set
                if ((x & 1) != 0) {

                    // Increment fre1[j]
                    fre1[j] += 1;
                }

                // Otherwise
                else {

                    // Increment fre0[j]
                    fre0[j] += 1;
                }

                // Right shift x by 1
                x = x >> 1;
            }
        }

        // Stores the count of total moves
        int ans = 0;

        // Traverse the range [0, 32]
        for (int i = 0; i < 33; i++) {

            // Update the value of ans
            ans += Math.Min(fre0[i], fre1[i]);
        }

        // Return the minimum number of
        // flips required
        return ans;
    }

    // Driver Code
    public static void Main()
    {
        int[] arr = { 3, 5 };
        int N = arr.Length;

        Console.WriteLine(makeEqual(arr, N));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
// javascript program for the above approach
    // Function to count minimum number
    // of bits required to be flipped
    // to make all array elements equal
    function makeEqual(arr , n)
    {

        // Stores the count of unset bits
        var fre0 = Array(33).fill(0);

        // Stores the count of set bits
        var fre1 = Array(33).fill(0);

        // Traverse the array
        for (i = 0; i < n; i++) {
            var x = arr[i];

            // Traverse the bit of arr[i]
            for (j = 0; j < 33; j++) {

                // If current bit is set
                if ((x & 1) != 0) {

                    // Increment fre1[j]
                    fre1[j] += 1;
                }

                // Otherwise
                else {

                    // Increment fre0[j]
                    fre0[j] += 1;
                }

                // Right shift x by 1
                x = x >> 1;
            }
        }

        // Stores the count of total moves
        var ans = 0;

        // Traverse the range [0, 32]
        for (i = 0; i < 33; i++) {

            // Update the value of ans
            ans += Math.min(fre0[i], fre1[i]);
        }

        // Return the minimum number of
        // flips required
        return ans;
    }

    // Driver Code
        var arr = [ 3, 5 ];
        var N = arr.length;

        document.write(makeEqual(arr, N));

// This code is contributed by aashish1995
</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N * log N)*
***辅助空间:** O(1)*