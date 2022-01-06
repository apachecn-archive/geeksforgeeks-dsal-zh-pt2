# 最小化为使所有数组元素等于 1 而需要执行的给定操作的数量

> 原文:[https://www . geesforgeks . org/minimum-给定操作的计数-需要执行-使所有数组元素等于 1/](https://www.geeksforgeeks.org/minimize-count-of-given-operations-required-to-be-performed-to-make-all-array-elements-equal-to-1/)

给定一个由 **N** 正整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)、 **arr[]** ，任务是通过执行以下操作最少次数使所有数组元素等于 **1** :

*   将子数组中所有元素的值增加任意正整数。
*   如果所有数组元素都是偶数，则将所有数组元素除以 **2** 。

打印所需的最小操作数。

**示例:**

> **输入:** arr[] = { 3，1，2，4 }
> **输出:** 3
> **解释:**
> arr[0]递增 1，arr[1]递增 3，arr[2]递增 2 将 arr[]修改为{ 4，4，4，4 }。
> 将所有数组元素除以 2 将 arr[]修改为{ 2，2，2，2 }。
> 将所有数组元素除以 2 将 arr[]修改为{ 1，1，1，1 }。
> 因此，要求输出为 3。
> 
> **输入:** arr[] = { 2，4 }
> **输出:** 3
> **解释:**
> 将所有数组元素除以 2 将 arr[]修改为{ 1，2 }。
> 将 arr[0]的值增加 1 会将 arr[]修改为{ 2，2 }。
> 将所有数组元素除以 2 将 arr[]修改为{ 1，2 }。
> 因此，要求输出为 3。

**方法:**使用[贪婪手法](https://www.geeksforgeeks.org/greedy-algorithms/)可以解决问题。按照以下步骤解决问题:

*   [找到阵中最大的元素](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)说， **Max** 。
*   如果所有数组元素相等，并且也是 **2** 的幂，那么打印**日志 <sub>2</sub> (最大)**。
*   否则，使所有数组元素等于大于或等于 **Max** 的 **2** 的最近幂，并打印 **log <sub>2</sub> (Max)** + 1。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if all array
// elements are equal or not
bool CheckAllEqual(int arr[], int N)
{

    // Traverse the array
    for (int i = 1; i < N; i++) {

        // If all array elements
        // are not equal
        if (arr[0] != arr[i]) {

            return false;
        }
    }

    return true;
}

// Function to find minimum count of operation
// to make all the array elements equal to 1
int minCntOperations(int arr[], int N)
{

    // Stores largest element of the array
    int Max = *max_element(arr, arr + N);

    // Check if a number is a power of 2 or not
    bool isPower2 = !(Max && (Max & (Max - 1)));

    // If Max is a power of 2 and all
    // array elements are equal
    if (isPower2 && CheckAllEqual(arr, N)) {

        return log2(Max);
    }
    else {

        return ceil(log2(Max)) + 1;
    }
}

// Driver Code
int main()
{

    int arr[] = { 2, 4 };

    int N = sizeof(arr) / sizeof(arr[0]);

    cout << minCntOperations(arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;
import java.util.*;
class GFG
{

    // Function to check if all array
    // elements are equal or not
    static boolean CheckAllEqual(int arr[], int N)
    {

        // Traverse the array
        for (int i = 1; i < N; i++)
        {

            // If all array elements
            // are not equal
            if (arr[0] != arr[i])
            {
                return false;
            }
        }
        return true;
    }

    // Function to find minimum count of operation
    // to make all the array elements equal to 1
    static int minCntOperations(int arr[], int N)
    {

        // Stores largest element of the array
        int Max = Arrays.stream(arr).max().getAsInt();

        // Check if a number is a power of 2 or not
        boolean isPower2;
        if ((int)(Math.ceil((Math.log(N) / Math.log(N))))
            == (int)(Math.floor(((Math.log(N) / Math.log(2))))))
        {
            isPower2 = true;
        }
        else
        {
            isPower2 = false;
        }

        // If Max is a power of 2 and all
        // array elements are equal
        if (isPower2 && CheckAllEqual(arr, N))
        {
            return (int)(Math.log(Max) / Math.log(2));
        }
        else
        {
            return (int)Math.ceil(Math.log(Max)
                                  / Math.log(2)) + 1;
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = new int[] { 2, 4 };
        int N = arr.length;
        System.out.println(minCntOperations(arr, N));
    }
}

// This code is contributed by Dharanendra L V
```

## 蟒蛇 3

```
# Python 3 program to implement
# the above approach
import math

# Function to check if all array
# elements are equal or not
def CheckAllEqual(arr, N):

    # Traverse the array
    for i in range(1, N):

        # If all array elements
        # are not equal
        if (arr[0] != arr[i]):
            return False
    return True

# Function to find minimum count of operation
# to make all the array elements equal to 1
def minCntOperations(arr, N):

    # Stores largest element of the array
    Max = max(arr)

    # Check if a number is a power of 2 or not
    isPower2 = not (Max and (Max & (Max - 1)))

    # If Max is a power of 2 and all
    # array elements are equal
    if (isPower2 and CheckAllEqual(arr, N)):
        return log2(Max)
    else:
        return math.ceil(math.log2(Max)) + 1

# Driver Code
if __name__ == "__main__":
    arr = [2, 4]
    N = len(arr)
    print(minCntOperations(arr, N))

    # This code is contributed by chitranayal.
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Linq;
class GFG {

  // Function to check if all array
  // elements are equal or not
  static bool CheckAllEqual(int[] arr, int N)
  {

    // Traverse the array
    for (int i = 1; i < N; i++)
    {

      // If all array elements
      // are not equal
      if (arr[0] != arr[i])
      {
        return false;
      }
    }
    return true;
  }

  // Function to find minimum count of operation
  // to make all the array elements equal to 1
  static int minCntOperations(int[] arr, int N)
  {

    // Stores largest element of the array
    int Max = arr.Max();

    // Check if a number is a power of 2 or not
    bool isPower2;
    if ((int)(Math.Ceiling((Math.Log(N) / Math.Log(N))))
        == (int)(Math.Floor(((Math.Log(N) / Math.Log(2))))))
    {
      isPower2 = true;
    }
    else
    {
      isPower2 = false;
    }

    // If Max is a power of 2 and all
    // array elements are equal
    if (isPower2 && CheckAllEqual(arr, N))
    {
      return (int)(Math.Log(Max) / Math.Log(2));
    }
    else
    {
      return (int)Math.Ceiling(Math.Log(Max)
                               / Math.Log(2)) + 1;
    }
  }

  // Driver Code
  static public void Main()
  {
    int[] arr = new int[] { 2, 4 };
    int N = arr.Length;
    Console.WriteLine(minCntOperations(arr, N));
  }
}

// This code is contributed by Dharanendra L V
```

## java 描述语言

```
<script>
// javascript program to implement
// the above approach   

// Function to check if all array
    // elements are equal or not
    function CheckAllEqual(arr, N)
    {

        // Traverse the array
        for (i = 1; i < N; i++)
        {

            // If all array elements
            // are not equal
            if (arr[0] != arr[i])
            {
                return false;
            }
        }
        return true;
    }

    // Function to find minimum count of operation
    // to make all the array elements equal to 1
    function minCntOperations(arr, N)
    {

        // Stores largest element of the array
        var Max =Math.max.apply(Math,arr);

        // Check if a number is a power of 2 or not
        var isPower2;
        if (parseInt( (Math.ceil((Math.log(N) / Math.log(N))))) == parseInt( (Math.floor(((Math.log(N) / Math.log(2))))))) {
            isPower2 = true;
        } else {
            isPower2 = false;
        }

        // If Max is a power of 2 and all
        // array elements are equal
        if (isPower2 && CheckAllEqual(arr, N))
        {
            return parseInt( (Math.log(Max) / Math.log(2)));
        }
        else
        {
            return parseInt( Math.ceil(Math.log(Max) / Math.log(2))) + 1;
        }
    }

    // Driver Code
        var arr = [ 2, 4 ];
        var N = arr.length;
        document.write(minCntOperations(arr, N));

// This code is contributed by Rajput-Ji
</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)