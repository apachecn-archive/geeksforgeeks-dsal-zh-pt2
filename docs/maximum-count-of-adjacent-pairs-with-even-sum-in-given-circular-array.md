# 给定圆形阵列中具有偶数和的相邻对的最大计数

> 原文:[https://www . geeksforgeeks . org/给定循环数组中相邻对的最大计数/](https://www.geeksforgeeks.org/maximum-count-of-adjacent-pairs-with-even-sum-in-given-circular-array/)

给定一个由 **N** 个整数组成的[圆形二进制数组](https://www.geeksforgeeks.org/circular-array/) **arr[]** ，任务是找到相邻元素对的最大计数，这些元素的和是偶数，其中每个元素最多只能属于一对。

**示例:**

> **输入:** arr[] = {1，1，1，0，1}
> **输出:** 2
> **说明:**可以形成如下两对:
> 
> 1.  arr[0]和 arr[4]构成第一对，因为给定的数组是循环的，arr[0] + arr[4] = 2。
> 2.  arr[1]和 arr[2]形成第二对。
> 
> **输入:** arr[] = {1，1，1，0，1，1，0，0}
> **输出:** 3

**方法:**给定的问题可以用[贪婪的方法](https://www.geeksforgeeks.org/greedy-algorithms/)来解决。可以观察到，所需的对只能由相同的元素形成，即 **(0，0)** 或 **(1，1)** 。另外，从 **X** 连续 **1 的**或 **0 的**可以形成的对的数量是[地板](https://www.geeksforgeeks.org/ceil-floor-functions-cpp/) (X / 2)。因此遍历给定的数组，计算所有可能的[组连续整数](https://www.geeksforgeeks.org/maximum-consecutive-ones-or-zeros-in-a-binary-array/)，并将每个组的 **X / 2** 加到答案中。
此外，检查 1 <sup>st</sup> 集合和最后一组连续整数是否具有相同的值，并且两组中的元素数量是奇数，然后将答案增加 1。

下面是上述方法的实现:

## C++

```
//C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find maximum count of
// pairs of adjacent elements with even
// sum in the given circular array
void findMaximumPairs(vector<int> arr)
{

    // Stores the value of current
    // integer during traversal
    int currentElement = arr[0], count = 1;

    // First chain's count and total number
    // of pairs is initially 0
    int firstChainCount = 0, totalPairs = 0;

    // flag is used to check if the current
    // chain is the first chain in array
    bool flag = true;

    for (int i = 1; i < arr.size(); i++)
    {

        // Count the number of
        // consecutive elements
        if (arr[i] == currentElement) {
            count++;
        }
        else {

            if (flag == true) {

                // Stores the count of
                // elements in 1st set
                firstChainCount = count;
                flag = false;
            }

            // Update answer
            totalPairs = totalPairs + count / 2;

            // Update current integer
            currentElement = arr[i];
            count = 1;
        }
    }

    totalPairs = totalPairs + count / 2;
    int lastChainCount = count;

    if (arr[0] == arr[arr.size() - 1]
        && firstChainCount % 2 == 1
        && lastChainCount % 2 == 1)
        totalPairs++;

    // Print Answer
    cout << (totalPairs);
}

// Driver Code
int main()
{
    vector<int> arr = { 1, 1, 1, 0, 1, 1, 0, 0 };
    findMaximumPairs(arr);
    return 0;
}

// This code is contributed by Potta Lokesh
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG {
    // Function to find maximum count of
    // pairs of adjacent elements with even
    // sum in the given circular array
    public static void findMaximumPairs(int[] arr)
    {
        // Stores the value of current
        // integer during traversal
        int currentElement = arr[0], count = 1;

        // First chain's count and total number
        // of pairs is initially 0
        int firstChainCount = 0, totalPairs = 0;

        // flag is used to check if the current
        // chain is the first chain in array
        boolean flag = true;

        for (int i = 1; i < arr.length; i++) {
            // Count the number of
            // consecutive elements
            if (arr[i] == currentElement) {
                count++;
            }
            else {

                if (flag == true) {

                    // Stores the count of
                    // elements in 1st set
                    firstChainCount = count;
                    flag = false;
                }

                // Update answer
                totalPairs = totalPairs + count / 2;

                // Update current integer
                currentElement = arr[i];
                count = 1;
            }
        }

        totalPairs = totalPairs + count / 2;
        int lastChainCount = count;

        if (arr[0] == arr[arr.length - 1]
            && firstChainCount % 2 == 1
            && lastChainCount % 2 == 1)
            totalPairs++;

        // Print Answer
        System.out.println(totalPairs);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 1, 1, 1, 0, 1, 1, 0, 0 };
        findMaximumPairs(arr);
    }
}
```

## 计算机编程语言

```
# Python program for the above approach
import math

# Function to find maximum count of
# pairs of adjacent elements with even
# sum in the given circular array
def findMaximumPairs(arr):

    # Stores the value of current
    # integer during traversal
    currentElement = arr[0]
    count = 1

    # First chain's count and total number
    # of pairs is initially 0
    firstChainCount = 0
    totalPairs = 0

    # flag is used to check if the current
    # chain is the first chain in array
    flag = True;

    for i in range(1, len(arr)):

        # Count the number of
        # consecutive elements
        if (arr[i] == currentElement):
            count = count + 1

        else:
            if (flag == True):

                # Stores the count of
                # elements in 1st set
                firstChainCount = count
                flag = False

            # Update answer
            totalPairs = totalPairs + math.floor(count / 2)

            # Update current integer
            currentElement = arr[i]
            count = 1

    totalPairs = totalPairs + math.floor(count / 2)
    lastChainCount = count

    if (arr[0] == arr[len(arr) - 1]
        and firstChainCount % 2 == 1
        and lastChainCount % 2 == 1):
        totalPairs = totalPairs + 1

    # Print Answer
    print(totalPairs)

# Driver Code
arr = [ 1, 1, 1, 0, 1, 1, 0, 0 ]
findMaximumPairs(arr)

# This code is contributed by Samim Hossain Mondal.
```

## C#

```
// C# code to implement above approach
using System;
class GFG {

    // Function to find maximum count of
    // pairs of adjacent elements with even
    // sum in the given circular array
    static void findMaximumPairs(int[] arr)
    {
        // Stores the value of current
        // integer during traversal
        int currentElement = arr[0], count = 1;

        // First chain's count and total number
        // of pairs is initially 0
        int firstChainCount = 0, totalPairs = 0;

        // flag is used to check if the current
        // chain is the first chain in array
        bool flag = true;

        for (int i = 1; i < arr.Length; i++) {
            // Count the number of
            // consecutive elements
            if (arr[i] == currentElement) {
                count++;
            }
            else {

                if (flag == true) {

                    // Stores the count of
                    // elements in 1st set
                    firstChainCount = count;
                    flag = false;
                }

                // Update answer
                totalPairs = totalPairs + count / 2;

                // Update current integer
                currentElement = arr[i];
                count = 1;
            }
        }

        totalPairs = totalPairs + count / 2;
        int lastChainCount = count;

        if (arr[0] == arr[arr.Length - 1]
            && firstChainCount % 2 == 1
            && lastChainCount % 2 == 1)
            totalPairs++;

        // Print Answer
        Console.Write(totalPairs);
    }

    // Driver Code
    public static void Main()
    {
        int []arr = { 1, 1, 1, 0, 1, 1, 0, 0 };
        findMaximumPairs(arr);
    }
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find maximum count of
// pairs of adjacent elements with even
// sum in the given circular array
const findMaximumPairs = (arr) => {

    // Stores the value of current
    // integer during traversal
    let currentElement = arr[0], count = 1;

    // First chain's count and total number
    // of pairs is initially 0
    let firstChainCount = 0, totalPairs = 0;

    // flag is used to check if the current
    // chain is the first chain in array
    let flag = true;

    for(let i = 1; i < arr.length; i++)
    {

        // Count the number of
        // consecutive elements
        if (arr[i] == currentElement)
        {
            count++;
        }
        else
        {
            if (flag == true)
            {

                // Stores the count of
                // elements in 1st set
                firstChainCount = count;
                flag = false;
            }

            // Update answer
            totalPairs = totalPairs + parseInt(count / 2);

            // Update current integer
            currentElement = arr[i];
            count = 1;
        }
    }

    totalPairs = totalPairs + parseInt(count / 2);
    let lastChainCount = count;

    if (arr[0] == arr[arr.length - 1] &&
            firstChainCount % 2 == 1 &&
             lastChainCount % 2 == 1)
        totalPairs++;

    // Print Answer
    document.write(totalPairs);
}

// Driver Code
let arr = [ 1, 1, 1, 0, 1, 1, 0, 0 ];

findMaximumPairs(arr);

// This code is contributed by rakeshsahni

</script>
```

**Output**

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)