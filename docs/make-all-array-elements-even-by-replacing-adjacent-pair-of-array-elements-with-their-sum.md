# 用数组元素的和替换相邻的数组元素对，使所有数组元素均匀

> 原文:[https://www . geeksforgeeks . org/通过用数组元素的和替换相邻的数组元素对来制造所有数组元素偶数/](https://www.geeksforgeeks.org/make-all-array-elements-even-by-replacing-adjacent-pair-of-array-elements-with-their-sum/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是通过用它们的和替换一对相邻的元素来使所有数组元素[变得均匀。](https://www.geeksforgeeks.org/c-program-to-check-whether-a-given-number-is-even-or-odd/)

**示例:**

> **输入:** arr[] = { 2，4，5，11，6 }
> **输出:** 1
> **解释:**
> 将一对(arr[2]，arr[3])替换为它们的和(= 5 + 11 = 16)将 arr[]修改为{ 2，4，16，16，6 }
> 由于所有数组元素都是偶数，因此所需的输出为 1。
> 
> **输入:** arr[] = { 1，2，4，3，11 }
> **输出:** 3
> **解释:**
> 替换对(arr[3]，arr[4])并用它们的和(= 3 + 11 = 14)替换它们将 arr[]修改为{ 1，2，4，14，14 }
> 替换对(arr[0]，arr[1])并用它们的和(= 1 + 2 = 3)替换它们将 arr[]修改为 14 }
> 将对(arr[0]，arr[1])替换为它们的和(= 3 + 3 = 6)将 arr[]修改为{ 6，6，4，14，14 }。
> 因此，要求输出为 3。

**方法:**想法是利用两个[奇数](https://www.geeksforgeeks.org/c-program-to-check-whether-a-given-number-is-even-or-odd/)之和生成一个[偶数](https://www.geeksforgeeks.org/c-program-to-check-whether-a-given-number-is-even-or-odd/)的事实。按照以下步骤解决问题:

1.  初始化两个整数，比如说 **res** 来计算替换的数量， **odd_continuous_segment** 来计算连续奇数的数量
2.  [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并检查每个数组元素的以下条件:
    1.  [如果**arr【I】**为奇数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)，则将**奇数 _ 连续 _ 段**的计数增加 1
    2.  否则，如果**奇数 _ 连续 _ 段**为奇数，则以**奇数 _ 连续 _ 段/2** 递增 **res** 。否则，将 **res** 增加**odd _ continuous _ segment/2+2**，并将 **odd_continuous_segment** 分配给 **0** 。
3.  [检查**奇数 _ 连续 _ 段**是否为奇数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)。如果发现为真，则将 **res** 增加 **odd_continuous_segment / 2** 。否则将 **res** 增加**(odd _ continuous _ segment/2+2)**
4.  最后，打印得到的 **res** 值

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <iostream>
using namespace std;

// Function to find minimum count of operations
// required to make all array elements even
int make_array_element_even(int arr[], int N)
{
    // Stores minimum count of replacements
    // to make all array elements even
    int res = 0;

    // Stores the count of odd
    // continuous numbers
    int odd_cont_seg = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // If arr[i] is an odd number
        if (arr[i] % 2 == 1) {

            // Update odd_cont_seg
            odd_cont_seg++;
        }
        else {

            if (odd_cont_seg > 0) {

                // If odd_cont_seg is even
                if (odd_cont_seg % 2 == 0) {

                    // Update res
                    res += odd_cont_seg / 2;
                }

                else {

                    // Update res
                    res += (odd_cont_seg / 2) + 2;
                }

                // Reset odd_cont_seg = 0
                odd_cont_seg = 0;
            }
        }
    }

    // If odd_cont_seg exceeds 0
    if (odd_cont_seg > 0) {

        // If odd_cont_seg is even
        if (odd_cont_seg % 2 == 0) {

            // Update res
            res += odd_cont_seg / 2;
        }

        else {

            // Update res
            res += odd_cont_seg / 2 + 2;
        }
    }

    // Print the result
    return res;
}

// Drivers Code
int main()
{
    int arr[] = { 2, 4, 5, 11, 6 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << make_array_element_even(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG{

  // Function to find minimum count of operations
  // required to make all array elements even
  static int make_array_element_even(int arr[], int N)
  {

    // Stores minimum count of replacements
    // to make all array elements even
    int res = 0;

    // Stores the count of odd
    // continuous numbers
    int odd_cont_seg = 0;

    // Traverse the array
    for (int i = 0; i < N; i++)
    {

      // If arr[i] is an odd number
      if (arr[i] % 2 == 1)
      {

        // Update odd_cont_seg
        odd_cont_seg++;
      }
      else
      {
        if (odd_cont_seg > 0)
        {

          // If odd_cont_seg is even
          if (odd_cont_seg % 2 == 0)
          {

            // Update res
            res += odd_cont_seg / 2;
          }

          else
          {

            // Update res
            res += (odd_cont_seg / 2) + 2;
          }

          // Reset odd_cont_seg = 0
          odd_cont_seg = 0;
        }
      }
    }

    // If odd_cont_seg exceeds 0
    if (odd_cont_seg > 0)
    {

      // If odd_cont_seg is even
      if (odd_cont_seg % 2 == 0)
      {

        // Update res
        res += odd_cont_seg / 2;
      }

      else
      {

        // Update res
        res += odd_cont_seg / 2 + 2;
      }
    }

    // Print the result
    return res;
  }

  // Drivers Code
  public static void main(String[] args)
  {
    int arr[] = { 2, 4, 5, 11, 6 };
    int N = arr.length;
    System.out.print(make_array_element_even(arr, N));
  }
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python program to implement
# the above approach

# Function to find minimum count of operations
# required to make all array elements even
def make_array_element_even(arr, N):

    # Stores minimum count of replacements
    # to make all array elements even
    res = 0

    # Stores the count of odd
    # continuous numbers
    odd_cont_seg = 0

    # Traverse the array
    for i in range(0, N):

        # If arr[i] is an odd number
        if (arr[i] % 2 == 1):

            # Update odd_cont_seg
            odd_cont_seg+=1
        else:
            if (odd_cont_seg > 0):

                # If odd_cont_seg is even
                if (odd_cont_seg % 2 == 0):

                    # Update res
                    res += odd_cont_seg // 2

                else:

                    # Update res
                    res += (odd_cont_seg // 2) + 2

                # Reset odd_cont_seg = 0
                odd_cont_seg = 0

    # If odd_cont_seg exceeds 0
    if (odd_cont_seg > 0):

        # If odd_cont_seg is even
        if (odd_cont_seg % 2 == 0):

            # Update res
            res += odd_cont_seg // 2

        else:

            # Update res
            res += odd_cont_seg // 2 + 2

    # Prthe result
    return res

# Drivers Code
arr =  [2, 4, 5, 11, 6]
N = len(arr)
print(make_array_element_even(arr, N))

# This code is contributed by shubhamsingh10
```

## C#

```
// C# program to implement
// the above approach
using System;
public class GFG
{

  // Function to find minimum count of operations
  // required to make all array elements even
  static int make_array_element_even(int []arr, int N)
  {

    // Stores minimum count of replacements
    // to make all array elements even
    int res = 0;

    // Stores the count of odd
    // continuous numbers
    int odd_cont_seg = 0;

    // Traverse the array
    for (int i = 0; i < N; i++)
    {

      // If arr[i] is an odd number
      if (arr[i] % 2 == 1)
      {

        // Update odd_cont_seg
        odd_cont_seg++;
      }
      else
      {
        if (odd_cont_seg > 0)
        {

          // If odd_cont_seg is even
          if (odd_cont_seg % 2 == 0)
          {

            // Update res
            res += odd_cont_seg / 2;
          }

          else
          {

            // Update res
            res += (odd_cont_seg / 2) + 2;
          }

          // Reset odd_cont_seg = 0
          odd_cont_seg = 0;
        }
      }
    }

    // If odd_cont_seg exceeds 0
    if (odd_cont_seg > 0)
    {

      // If odd_cont_seg is even
      if (odd_cont_seg % 2 == 0)
      {

        // Update res
        res += odd_cont_seg / 2;
      }

      else
      {

        // Update res
        res += odd_cont_seg / 2 + 2;
      }
    }

    // Print the result
    return res;
  }

  // Drivers Code
  public static void Main(String[] args)
  {
    int []arr = { 2, 4, 5, 11, 6 };
    int N = arr.Length;
    Console.Write(make_array_element_even(arr, N));
  }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to find minimum count of operations
// required to make all array elements even
function make_array_element_even(arr, N)
{

    // Stores minimum count of replacements
    // to make all array elements even
    let res = 0;

    // Stores the count of odd
    // continuous numbers
    let odd_cont_seg = 0;

    // Traverse the array
    for(let i = 0; i < N; i++)
    {

        // If arr[i] is an odd number
        if (arr[i] % 2 == 1)
        {

            // Update odd_cont_seg
            odd_cont_seg++;
        }
        else
        {
            if (odd_cont_seg > 0)
            {

                // If odd_cont_seg is even
                if (odd_cont_seg % 2 == 0)
                {

                    // Update res
                    res += odd_cont_seg / 2;
                }
                else
                {

                    // Update res
                    res += (odd_cont_seg / 2) + 2;
                }

                // Reset odd_cont_seg = 0
                odd_cont_seg = 0;
            }
        }
    }

    // If odd_cont_seg exceeds 0
    if (odd_cont_seg > 0)
    {

        // If odd_cont_seg is even
        if (odd_cont_seg % 2 == 0)
        {

            // Update res
            res += odd_cont_seg / 2;
        }

        else
        {

            // Update res
            res += odd_cont_seg / 2 + 2;
        }
    }

    // Print the result
    return res;
}

// Driver Code

// Given array arr[]
let arr = [ 2, 4, 5, 11, 6 ];
let N = arr.length;

document.write(make_array_element_even(arr, N));

// This code is contributed by splevel62

</script>
```

**Output:** 

```
1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)