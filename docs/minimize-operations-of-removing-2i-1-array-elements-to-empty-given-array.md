# 最小化移除 2i -1 数组元素以清空给定数组的操作

> 原文:[https://www . geesforgeks . org/minimum-operations-of-remove-2i-1-array-elements-to-empty-given-array/](https://www.geeksforgeeks.org/minimize-operations-of-removing-2i-1-array-elements-to-empty-given-array/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是通过在每次操作中移除**2<sup>I</sup>–1**数组元素来清空给定数组( ***i** 为任意正整数*)。找到所需的最小操作数。

**示例:**

> **输入:** arr[] = { 2，3，4 }
> **输出:** 1
> **解释:**
> 移除(2<sup>2</sup>–1)元素即{ arr[0]，arr[1]，arr[2] }将 arr[]修改为{ }
> 由于数组中没有剩余元素，因此所需的输出为 1。
> 
> **输入:** arr[] = { 1，2，3，4 }
> **输出:** 2
> **解释:**
> 移除(2<sup>1</sup>–1)元素即{ arr[0] }将 arr[]修改为{ 2，3，4 }
> 移除(2<sup>2</sup>–1)元素即{ arr[0]，arr[1]，arr[2] }将 arr[]修改为{ }

**方法:**使用[贪婪手法](https://www.geeksforgeeks.org/greedy-algorithms/)可以解决问题。其思想是总是从数组中移除最大可能数量的元素**(2<sup>I</sup>–1**)。按照以下步骤解决问题:

*   初始化一个变量，比如 **cntSteps** ，以存储清空给定数组所需的最小操作数。
*   移除 **N** 数组元素将 **arr[]** 修改为 **0** 长度数组。因此，将 **N** 的值增加 **1** 。
*   使用变量 **i** 遍历 **N** 的每个位，对于每个 **i <sup>第</sup>** 位，[检查该位是否置位](https://www.geeksforgeeks.org/check-whether-k-th-bit-set-not/)。如果发现为真，则更新 **cntSteps += 1**
*   最后，打印 **cntSteps** 的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find minimum count of steps
// required to remove all the array elements
int minimumStepReqArr(int arr[], int N)
{

    // Stores minimum count of steps required
    // to remove all the array elements
    int cntStep = 0;

    // Update N
    N += 1;

    // Traverse each bit of N
    for (int i = 31; i >= 0; i--) {

        // If current bit is set
        if (N & (1 << i)) {

            // Update cntStep
            cntStep += 1;
        }
    }

    return cntStep;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3 };

    int N = sizeof(arr) / sizeof(arr[0]);
    cout << minimumStepReqArr(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG
{

  // Function to find minimum count of steps
  // required to remove all the array elements
  static int minimumStepReqArr(int[] arr, int N)
  {

    // Stores minimum count of steps required
    // to remove all the array elements
    int cntStep = 0;

    // Update N
    N += 1;

    // Traverse each bit of N
    for (int i = 31; i >= 0; i--)
    {

      // If current bit is set
      if ((N & (1 << i)) != 0)
      {

        // Update cntStep
        cntStep += 1;
      }
    }      
    return cntStep;
  }

  // Driver code
  public static void main(String[] args)
  {
    int[] arr = { 1, 2, 3 };

    int N = arr.length;
    System.out.println(minimumStepReqArr(arr, N));
  }
}

// This code is contributed by susmitakundugoaldanga
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find minimum count of steps
# required to remove all the array elements
def minimumStepReqArr(arr, N):

    # Stores minimum count of steps required
    # to remove all the array elements
    cntStep = 0

    # Update N
    N += 1

    i = 31

    while(i >= 0):

        # If current bit is set
        if (N & (1 << i)):

            # Update cntStep
            cntStep += 1

        i -= 1

    return cntStep

# Driver Code
if __name__ == '__main__':

    arr = [ 1, 2, 3 ]
    N = len(arr)

    print(minimumStepReqArr(arr, N))

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG
{

  // Function to find minimum count of steps
  // required to remove all the array elements
  static int minimumStepReqArr(int[] arr, int N)
  {

    // Stores minimum count of steps required
    // to remove all the array elements
    int cntStep = 0;

    // Update N
    N += 1;

    // Traverse each bit of N
    for (int i = 31; i >= 0; i--)
    {

      // If current bit is set
      if ((N & (1 << i)) != 0)
      {

        // Update cntStep
        cntStep += 1;
      }
    }      
    return cntStep;
  }

  // Driver code
  static void Main()
  {
    int[] arr = { 1, 2, 3 };

    int N = arr.Length;
    Console.WriteLine(minimumStepReqArr(arr, N));
  }
}

// This code is contributed by divyesh072019
```

## java 描述语言

```
<script>
    // Javascript program to implement the above approach

    // Function to find minimum count of steps
    // required to remove all the array elements
    function minimumStepReqArr(arr, N)
    {

      // Stores minimum count of steps required
      // to remove all the array elements
      let cntStep = 0;

      // Update N
      N += 1;

      // Traverse each bit of N
      for (let i = 31; i >= 0; i--)
      {

        // If current bit is set
        if ((N & (1 << i)) != 0)
        {

          // Update cntStep
          cntStep += 1;
        }
      }     
      return cntStep;
    }

    let arr = [ 1, 2, 3 ];

    let N = arr.length;
    document.write(minimumStepReqArr(arr, N));

// This code is contributed by suresh07.
</script>
```

**Output:** 

```
1
```

***时间复杂度:**O(31)*
T5**辅助空间:** O(1)