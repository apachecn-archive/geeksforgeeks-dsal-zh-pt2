# 使所有数组元素相等所需的最小增量或减量 D

> 原文:[https://www . geesforgeks . org/最小-递增-或递减-d-要求使所有数组元素相等/](https://www.geeksforgeeks.org/minimum-increments-or-decrements-by-d-required-to-make-all-array-elements-equal/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** 和一个整数 **D** ，任务是通过将数组元素的最小数量增加或减少 **D** 来使所有数组元素相等。如果无法使所有数组元素相等，则打印 **-1** 。

**示例:**

> **输入:** N = 4，d = 2，arr[ ] = {2，4，6，8}
> **输出:** 4
> **解释:**
> 将 arr[0]递增 D(=2)将 arr[ ]修改为{ 4，4，6，8}。
> 将 arr[2]减 D(=2)将 arr[]修改为{ 4，4，4，8 }。
> 将 arr[3]减 D(=2)将 arr[]修改为{ 4，4，4，6 }。
> 将 arr[3]减 D(=2)会将 arr[]修改为{ 4，4，4，4 }。
> 
> **输入:** N = 4，K = 3，arr[ ] = {2，4，5，6 }
> T3】输出: -1

**进场:**思路是用[贪婪进场](https://www.geeksforgeeks.org/greedy-algorithms/)解决这个问题。以下是步骤:

1.  [按升序排序](https://www.geeksforgeeks.org/sorting-algorithms/)给定的数组。
2.  请注意，只有那些数组元素可以相等，它们与相邻索引元素的差完全可以被 **D** 整除，即**(a[I+1]–a[I])% D = = 0**。
3.  如果任何差异不能被 **D** 整除，则打印 **-1** ，因为不能使所有数组元素相等。
4.  现在，在这里使用[贪婪的方法](https://www.geeksforgeeks.org/greedy-algorithms/)。对于最小操作，考虑**中间元素**，并尝试将所有其他元素更改为**中间**。找出一个数字转换所需的操作数，即**ABS(mid–a[I])/D**。
5.  最后，打印所需的最小操作数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find minimum count of operations
// required to make all array elements equal by
// incrementing or decrementing array elements by d
void numOperation(int arr[], int N, int D)
{

    // Sort the array
    sort(arr, arr + N);

    // Traverse the array
    for (int i = 0; i < N - 1; i++) {

        // If difference between two consecutive
        // elements are not divisible by D
        if ((arr[i + 1] - arr[i]) % D != 0) {
            cout << "-1";
            return;
        }
    }

    // Store minimum count of operations required to
    // make all array elements equal by incrementing
    // or decrementing array elements by d
    int count = 0;

    // Stores middle element
    // of the array
    int mid = arr[N / 2];

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Update count
        count += abs(mid - arr[i]) / D;
    }

    cout << count;
}

// Driver Code
int main()
{

    // Given N & D
    int N = 4, D = 2;

    // Given array arr[]
    int arr[] = { 2, 4, 6, 8 };

    // Function Call
    numOperation(arr, N, D);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find minimum count of operations
// required to make all array elements equal by
// incrementing or decrementing array elements by d
static void numOperation(int arr[], int N, int D)
{

    // Sort the array
    Arrays.sort(arr);

    // Traverse the array
    for (int i = 0; i < N - 1; i++) {

        // If difference between two consecutive
        // elements are not divisible by D
        if ((arr[i + 1] - arr[i]) % D != 0) {
            System.out.println("-1");
            return;
        }
    }

    // Store minimum count of operations required to
    // make all array elements equal by incrementing
    // or decrementing array elements by d
    int count = 0;

    // Stores middle element
    // of the array
    int mid = arr[N / 2];

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Update count
        count += Math.abs(mid - arr[i]) / D;
    }
    System.out.println(count);
}

// Driver code
public static void main(String[] args)
{

    // Given N & D
    int N = 4, D = 2;

    // Given array arr[]
    int arr[] = { 2, 4, 6, 8 };

    // Function Call
    numOperation(arr, N, D);
}
}

// This code is contributed by code_hunt.
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find minimum count of operations
# required to make all array elements equal by
# incrementing or decrementing array elements by d
def numOperation(arr,  N, D):

    # Sort the array
    arr.sort()

    # Traverse the array
    for i in range(N - 1):

        # If difference between two consecutive
        # elements are not divisible by D
        if ((arr[i + 1] - arr[i]) % D != 0):
            print("-1")
            return

    # Store minimum count of operations required to
    # make all array elements equal by incrementing
    # or decrementing array elements by d
    count = 0

    # Stores middle element
    # of the array
    mid = arr[N // 2]

    # Traverse the array
    for i in range(N):

        # Update count
        count += abs(mid - arr[i]) // D
    print(count)

# Driver Code
if __name__ == "__main__":

    # Given N & D
    N = 4
    D = 2

    # Given array arr[]
    arr = [2, 4, 6, 8]

    # Function Call
    numOperation(arr, N, D)

    # This code is contributed by chitranayal
```

## C#

```
// C# program for the above approach
using System;

class GFG
{

    // Function to find minimum count of operations
    // required to make all array elements equal by
    // incrementing or decrementing array elements by d
    static void numOperation(int[] arr, int N, int D)
    {

        // Sort the array
        Array.Sort(arr);

        // Traverse the array
        for (int i = 0; i < N - 1; i++)
        {

            // If difference between two consecutive
            // elements are not divisible by D
            if ((arr[i + 1] - arr[i]) % D != 0)
            {
                Console.WriteLine("-1");
                return;
            }
        }

        // Store minimum count of operations required to
        // make all array elements equal by incrementing
        // or decrementing array elements by d
        int count = 0;

        // Stores middle element
        // of the array
        int mid = arr[N / 2];

        // Traverse the array
        for (int i = 0; i < N; i++)
        {

            // Update count
            count += Math.Abs(mid - arr[i]) / D;
        }
        Console.WriteLine(count);
    }

    // Driver code
    static public void Main()
    {

        // Given N & D
        int N = 4, D = 2;

        // Given array arr[]
        int[] arr = new int[] { 2, 4, 6, 8 };

        // Function Call
        numOperation(arr, N, D);
    }
}

// This code is contributed by Dharanendra L V
```

## java 描述语言

```
<script>

// Javascript program of the above approach

// Function to find minimum count of
// operations required to make all
// array elements equal by incrementing
// or decrementing array elements by d
function numOperation(arr, N, D)
{

    // Sort the array
    arr.sort();

    // Traverse the array
    for(let i = 0; i < N - 1; i++)
    {

        // If difference between two consecutive
        // elements are not divisible by D
        if ((arr[i + 1] - arr[i]) % D != 0)
        {
            document.write("-1");
            return;
        }
    }

    // Store minimum count of operations
    // required to make all array elements
    // equal by incrementing or decrementing
    // array elements by d
    let count = 0;

    // Stores middle element
    // of the array
    let mid = arr[N / 2];

    // Traverse the array
    for(let i = 0; i < N; i++)
    {

        // Update count
        count += Math.abs(mid - arr[i]) / D;
    }
    document.write(count);
}

// Driver Code

// Given N & D
let N = 4, D = 2;

// Given array arr[]
let arr = [ 2, 4, 6, 8 ];

// Function Call
numOperation(arr, N, D);

// This code is contributed by chinmoy1997pal

</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(N * Log(N))*
***辅助空间:** O(1)*