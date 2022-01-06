# 通过反转后缀子阵列

可能的数组的字典式最大排列

> 原文:[https://www . geeksforgeeks . org/按字典顺序排列的最大可能倒排后缀子数组/](https://www.geeksforgeeks.org/lexicographically-largest-permutation-of-array-possible-by-reversing-suffix-subarrays/)

给定一个大小为 **N、**的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是通过反转数组中的任何后缀[子数组](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)来找到[字典上最大的排列数组](https://www.geeksforgeeks.org/compare-two-strings-lexicographically-in-java/)。

**示例:**

> **输入:** arr[] = {3，5，4，1，2}
> **输出:** 3 5 4 2 1
> **解释:**反转后缀子数组{1，2}生成可能的数组元素的字典式最大排列。
> 
> **输入:** arr[] = {3，5，1，2，1}
> **输出:** 3 5 1 2 1
> **解释:**
> 给定的数组 arr[]，已经是该数组可能的最大字典排列了。

**天真方法:**最简单的方法是[反转](https://www.geeksforgeeks.org/write-a-program-to-reverse-an-array-or-string/)数组中所有可能的后缀子数组，打印出字典上最大可能的数组元素排列。
***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*

**高效法:**优化上述方法，思路是使用[贪婪法](https://www.geeksforgeeks.org/greedy-algorithms/)。给定的问题可以基于以下观察来解决:

> 可以观察到，通过在范围**【I，N–1】**中选择后缀数组作为子数组，使得**arr【I】<arr【N–1】**并将其反转，所获得的数组将是字典上最大的数组。

按照以下步骤解决问题:

*   初始化一个变量，比如说**标记**为 **-1** ，表示找到了一个值小于最后一个元素的索引。
*   [遍历给定数组](https://www.geeksforgeeks.org/iterating-arrays-java/) **arr[]** ，在每次迭代中，检查**arr[I]<arr[N–1]**是否存在。然后，将当前索引存储在变量**标志**和[中，断开循环](https://www.geeksforgeeks.org/break-statement-cc/)。
*   完成上述步骤后，检查**标志**的值是否为 **-1** 。如果发现为真，则反转后缀 subarray，即范围**【标志，N–1】**内的 subarray。
*   完成以上步骤后，[打印数组](https://www.geeksforgeeks.org/c-program-to-print-an-array-using-recursion/)**arr【】**作为结果。

下面是上述方法的实现:

## C++

```
// CPP program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function that
 void LLA(vector<int> A)
{

    // Stores the index that have
    // element less than the
    // element at last index
    int flg = -1;

    // Traverse the array
    for (int i = 0; i < A.size(); i++)
    {

        // Checks if value at the
        // current index is less
        // than value at last index
        if (A[i] < A[A.size() - 1])
        {

            // Assign the current
            // index value to index
            flg = i;
            break;
        }
    }

    // Check if index is not -1 then
    // reverse the suffix from the
    // index stored at flg
    if (flg != -1)
    {

        // Reversal of suffix
        for (int i = flg, j = A.size() - 1;
             i <= j; i++, j--)
        {

            // Swapping Step
            int temp = A[i];
            A[i] = A[j];
            A[j] = temp;
        }
    }

    // Print the final Array
    for (int i = 0; i < A.size(); i++)
         cout<<A[i]<<" ";
}

// Driver Code
int main()
{
  vector<int> arr= { 3, 5, 4, 1, 2 };

  // Function Call
  LLA(arr);
}

// This code is contributed by mohit kumar 29.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;

class GFG {

    // Function that
    public static void LLA(int A[])
    {

        // Stores the index that have
        // element less than the
        // element at last index
        int flg = -1;

        // Traverse the array
        for (int i = 0; i < A.length; i++) {

            // Checks if value at the
            // current index is less
            // than value at last index
            if (A[i] < A[A.length - 1]) {

                // Assign the current
                // index value to index
                flg = i;
                break;
            }
        }

        // Check if index is not -1 then
        // reverse the suffix from the
        // index stored at flg
        if (flg != -1) {

            // Reversal of suffix
            for (int i = flg, j = A.length - 1;
                 i <= j; i++, j--) {

                // Swapping Step
                int temp = A[i];
                A[i] = A[j];
                A[j] = temp;
            }
        }

        // Print the final Array
        for (int i = 0; i < A.length; i++)
            System.out.print(A[i] + " ");
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 3, 5, 4, 1, 2 };

        // Function Call
        LLA(arr);
    }
}
```

## 蟒蛇 3

```
# Python program for the above approach

# Function that
def LLA(A):

    # Stores the index that have
    # element less than the
    # element at last index
    flg = -1;

    # Traverse the array
    for i in range(len(A)):

        # Checks if value at the
        # current index is less
        # than value at last index
        if (A[i] < A[len(A) - 1]):

            # Assign the current
            # index value to index
            flg = i;
            break;

    # Check if index is not -1 then
    # reverse the suffix from the
    # index stored at flg
    if (flg != -1):

        # Reversal of suffix
        j = len(A) - 1;
        for i in range(flg, j + 1):

            # Swapping Step
            temp = A[i];
            A[i] = A[j];
            A[j] = temp;
            j -= 1;

    # Print the final Array
    for i in range(len(A)):
        print(A[i], end=" ");

# Driver Code
if __name__ == '__main__':
    arr = [3, 5, 4, 1, 2];

    # Function Call
    LLA(arr);

    # This code is contributed by 29AjayKumar
```

## C#

```
// C# program for the above approach
using System;

public class GFG
{

  // Function that
  public static void LLA(int []A)
  {

    // Stores the index that have
    // element less than the
    // element at last index
    int flg = -1;

    // Traverse the array
    for (int i = 0; i < A.Length; i++)
    {

      // Checks if value at the
      // current index is less
      // than value at last index
      if (A[i] < A[A.Length - 1])
      {

        // Assign the current
        // index value to index
        flg = i;
        break;
      }
    }

    // Check if index is not -1 then
    // reverse the suffix from the
    // index stored at flg
    if (flg != -1)
    {

      // Reversal of suffix
      for (int i = flg, j = A.Length - 1;
           i <= j; i++, j--)
      {

        // Swapping Step
        int temp = A[i];
        A[i] = A[j];
        A[j] = temp;
      }
    }

    // Print the readonly Array
    for (int i = 0; i < A.Length; i++)
      Console.Write(A[i] + " ");
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int []arr = { 3, 5, 4, 1, 2 };

    // Function Call
    LLA(arr);
  }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function that
function LLA(A)
{

    // Stores the index that have
    // element less than the
    // element at last index
    var flg = -1;
    var i,j;

    // Traverse the array
    for (i = 0; i < A.length; i++)
    {

        // Checks if value at the
        // current index is less
        // than value at last index
        if (A[i] < A[A.length - 1])
        {

            // Assign the current
            // index value to index
            flg = i;
            break;
        }
    }

    // Check if index is not -1 then
    // reverse the suffix from the
    // index stored at flg
    if (flg != -1)
    {

        // Reversal of suffix
        for (i = flg, j = A.length - 1;
             i <= j; i++, j--)
        {

            // Swapping Step
            var temp = A[i];
            A[i] = A[j];
            A[j] = temp;
        }
    }

    // Print the final Array
    for (i = 0; i < A.length; i++)
         document.write(A[i] + " ");
}

// Driver Code
  var arr =  [3, 5, 4, 1, 2];

  // Function Call
  LLA(arr);

</script>
```

**Output:** 

```
3 5 4 2 1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)