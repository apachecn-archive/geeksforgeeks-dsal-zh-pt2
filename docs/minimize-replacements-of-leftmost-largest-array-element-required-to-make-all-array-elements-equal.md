# 尽量减少替换最左边最大的数组元素，以使所有数组元素相等

> 原文:[https://www . geesforgeks . org/minimum-替换最左边最大的数组元素-需要使所有数组元素相等/](https://www.geeksforgeeks.org/minimize-replacements-of-leftmost-largest-array-element-required-to-make-all-array-elements-equal/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是通过用严格小于当前最大最小次数的最大元素替换数组最左边的最大元素来使所有数组元素相等。

**示例:**

> ***输入:** arr[] = { 1，1，2，2，3 < }*
> ***输出:** 4*
> **解释:**以下操作将所需的操作次数减少到最少:
> 
> 1.  最左边最大的数组元素是 arr[4]( = 3)。用小于当前最大元素 arr[3] (= 2)的最大元素替换它，数组将修改为{1，1，2，2，2}。
> 2.  数组最左边最大的元素是 arr[2]( = 2)。用小于当前最大元素 arr[1] (= 1)的最大元素替换它，数组将修改为{1，1，1，2，2}。
> 3.  数组最左边的最大元素是 arr[3]( = 2)，用比当前最大元素小的最大元素 arr[1] (= 1)替换它，数组修改为{1，1，1，1，2}。
> 4.  数组最左边最大的元素是 arr[4]( = 2)。用小于当前最大元素 arr[1] (=1)的最大元素替换它，数组将修改为{1，1，1，1，1}
> 
> 因此，至少需要 4 次移动。
> 
> ***输入:** arr[] = {* 5，1，3 *}*
> *输出: 3*

**方法:**这个问题可以通过[对数组进行降序排序](https://www.geeksforgeeks.org/how-to-sort-an-array-in-descending-order-using-stl-in-c/)来解决，根据观察，在每一步，一个数组元素将替换所有大于当前数组元素的元素。按照以下步骤解决问题:

*   [按降序排列数组](https://www.geeksforgeeks.org/how-to-sort-an-array-in-descending-order-using-stl-in-c/)。
*   初始化一个变量，说**把**算作 **0** ，来计算需要的移动总数。
*   使用变量 **i** 迭代范围**【1，N–1】**，并执行以下步骤:
    *   如果 **arr[i]！= arr[I–1]**，然后将**计数**增加 **i** 。
*   最后，完成上述步骤后，在**中获得的打印值计为**作为答案**。**

下面是上述方法的实现:

## C++

```
// C++ program for above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count minimum number of
// times the leftmost larger element is
// required to be replaced to make
// all array elements equal
int reductionOperations(int arr[], int N)
{
    // Sort the array in descending order
    sort(arr, arr + N, greater<int>());

    // Stores minimum number of moves required
    int count = 0;

    // Traverse the array
    for (int i = 1; i < N; i++) {

        // If arr[i - 1] is not equal to arr[i]
        if (arr[i - 1] != arr[i]) {

            // Update count
            count += i;
        }
    }

    // Return count
    return count;
}

// Driver code
int main()
{
    // Given input
    int arr[] = { 1, 1, 2, 2, 3 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << reductionOperations(arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for the above approach
import java.io.*;
import java.util.Arrays;
class GFG {
    public static int reductionOperations(int arr[], int N)
    {
        // Sort the array in descending order
        Arrays.sort(arr);
        reverse(arr);

        // Stores minimum number of moves required
        int count = 0;

        // Traverse the array
        for (int i = 1; i < N; i++) {

            // If arr[i - 1] is not equal to arr[i]
            if (arr[i - 1] != arr[i]) {

                // Update count
                count += i;
            }
        }

        // Return count
        return count;
    }

    public static void reverse(int[] array)
    {

        // Length of the array
        int n = array.length;

        // Swaping the first half elements with last half
        // elements
        for (int i = 0; i < n / 2; i++) {

            // Storing the first half elements temporarily
            int temp = array[i];

            // Assigning the first half to the last half
            array[i] = array[n - i - 1];

            // Assigning the last half to the first half
            array[n - i - 1] = temp;
        }
    }

    public static void main(String[] args)
    {
        // Given input
        int arr[] = { 1, 1, 2, 2, 3 };
        int N = arr.length;

        // Function Call
        System.out.println(reductionOperations(arr, N));
    }
}

  // This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# python 3 program for above approach

# Function to count minimum number of
# times the leftmost larger element is
# required to be replaced to make
# all array elements equal
def reductionOperations(arr, N):

    # Sort the array in descending order
    arr.sort(reverse=True)

    # Stores minimum number of moves required
    count = 0

    # Traverse the array
    for i in range(1, N, 1):

        # If arr[i - 1] is not equal to arr[i]
        if (arr[i - 1] != arr[i]):

            # Update count
            count += i

    # Return count
    return count

# Driver code
if __name__ == '__main__':

    # Given input
    arr = [1, 1, 2, 2, 3]
    N = len(arr)

    # Function Call
    print(reductionOperations(arr, N))

    # This code is contributed by ipg2016107.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

static int reductionOperations(int[] arr, int N)
{

    // Sort the array in descending order
    Array.Sort(arr);
    reverse(arr);

    // Stores minimum number of moves required
    int count = 0;

    // Traverse the array
    for(int i = 1; i < N; i++)
    {

        // If arr[i - 1] is not equal to arr[i]
        if (arr[i - 1] != arr[i])
        {

            // Update count
            count += i;
        }
    }

    // Return count
    return count;
}

static void reverse(int[] array)
{

    // Length of the array
    int n = array.Length;

    // Swaping the first half elements
    // with last half elements
    for(int i = 0; i < n / 2; i++)
    {

        // Storing the first half
        // elements temporarily
        int temp = array[i];

        // Assigning the first half
        // to the last half
        array[i] = array[n - i - 1];

        // Assigning the last half
        // to the first half
        array[n - i - 1] = temp;
    }
}

// Driver code
public static void Main()
{

    // Given input
    int[] arr = { 1, 1, 2, 2, 3 };
    int N = arr.Length;

    // Function Call
    Console.Write(reductionOperations(arr, N));
}
}

// This code is contributed by subham348
```

## java 描述语言

```
<script>
        // JavaScript program for the above approach

        // Function to count minimum number of
        // times the leftmost larger element is
        // required to be replaced to make
        // all array elements equal
        function reductionOperations(arr, N)
        {

            // Sort the array in descending order
            arr.sort(function (a, b) { return b - a });

            // Stores minimum number of moves required
            let count = 0;

            // Traverse the array
            for (let i = 1; i < N; i++) {

                // If arr[i - 1] is not equal to arr[i]
                if (arr[i - 1] != arr[i]) {

                    // Update count
                    count += i;
                }
            }

            // Return count
            return count;
        }

        // Driver code

        // Given input
        let arr = [1, 1, 2, 2, 3];
        let N = arr.length;

        // Function Call
        document.write(reductionOperations(arr, N));

  // This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
4
```

***时间复杂度:** O(N * log(N))*
***辅助空间:** O(1)*