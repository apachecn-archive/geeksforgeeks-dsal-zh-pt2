# 最小化两个数组之间的交换，使得第一个数组的和超过第二个数组的和

> 原文:[https://www . geesforgeks . org/minimum-在两个阵列之间交换-这样第一个阵列的总和就超过了第二个阵列的总和/](https://www.geeksforgeeks.org/minimize-swaps-between-two-arrays-such-that-sum-of-the-first-array-exceeds-sum-of-the-second-array/)

给定两个大小分别为 **N** 和 **M** 的[阵列](https://www.geeksforgeeks.org/arrays-in-c-cpp/)**arr 1【】**和**arr 2【】**，任务是计算两个阵列之间所需的最小交换次数，以便使阵列[的总和](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/) **arr1** []大于 **arr2** []。

**示例:**

> **输入:** arr1[] = {1，3，2，4}，arr2[] = {6，7，8}
> **输出:** 1
> **解释:**
> 将 arr1[0]换成 arr2[2]使 arr1[]之和等于 17，大于 14。
> 因此，所需的互换次数为 1。
> 
> **输入:** arr1[] = {2，2}，arr2[] = {5，5，5 }
> T3】输出: 2

**方法:**给定的问题可以通过[对两个数组](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)进行排序并执行交换来获得最大化**arr 1【】**的和来解决。按照以下步骤解决问题:

*   [对两个数组进行排序](https://www.geeksforgeeks.org/sort-c-stl/)，将数组的[和分别计算为 **sum1** 和 **sum2** 。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)
*   将变量**计数**初始化为 **0** 以存储所需的交换计数，并将 **j** 至**(M–1)**指向数组的最后一个元素 **arr2[]** 。
*   [使用变量 **i** 遍历阵列](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr 1【】**，并执行以下步骤:
    *   检查 **sum1** 是否小于或等于 **sum2** ，然后将当前元素**arr【I】**与元素**arr 2【j】**交换，以最大化 **sum1** 。
    *   交换后，更新 **sum1** 、 **sum2** 的值，递减 **j** 指向倒数第二个元素，递增**计数**。
*   完成上述步骤后，打印**计数**的值，作为所需交换的最小计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum count
// of swaps required between the two
// arrays to make the sum of arr1[]
// greater than that of arr2[]
int maximumCount(int arr1[], int arr2[],
                 int s1, int s2)
{
    // Stores the sum of the two arrays
    int sum1 = 0, sum2 = 0;

    // Calculate sum of arr1[]
    for (int i = 0; i < s1; i++) {
        sum1 += arr1[i];
    }

    // Calculate sum of arr2[]
    for (int j = 0; j < s2; j++) {
        sum2 += arr2[j];
    }

    int len = 0;
    if (s1 >= s2) {
        len = s2;
    }
    else {
        len = s1;
    }

    // Sort the arrays arr1[] and arr2[]
    sort(arr1, arr1 + s1);
    sort(arr2, arr2 + s2);

    int j = 0, k = s2 - 1, count = 0;

    // Traverse the array arr[]
    for (int i = 0; i < len; i++) {

        // If the sum1 is less than
        // or equal to sum2
        if (sum1 <= sum2) {

            // Swapping the elements
            if (arr2[k] >= arr1[i]) {

                // Update the sum1 and sum2
                int dif1 = arr1[j], dif2 = arr2[k];
                sum1 -= dif1;
                sum1 += dif2;

                sum2 -= dif2;
                sum2 += dif1;
                j++;
                k--;

                // Increment the count
                count++;
            }
            else {
                break;
            }
        }
        else {
            break;
        }
    }

    // Return the final count
    return count;
}

// Driver Code
int main()
{
    int arr1[] = { 1, 3, 2, 4 };
    int arr2[] = { 6, 7, 8 };
    int N = sizeof(arr1) / sizeof(arr1[0]);
    int M = sizeof(arr2) / sizeof(arr2[0]);

    // Function Call
    cout << maximumCount(arr1, arr2, N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;
class GFG
{

  // Function to find the minimum count
  // of swaps required between the two
  // arrays to make the sum of arr1[]
  // greater than that of arr2[]
  static int maximumCount(int[] arr1, int[] arr2, int s1,
                          int s2)
  {

    // Stores the sum of the two arrays
    int sum1 = 0, sum2 = 0;

    // Calculate sum of arr1[]
    for (int i = 0; i < s1; i++)
    {
      sum1 += arr1[i];
    }

    // Calculate sum of arr2[]
    for (int j = 0; j < s2; j++)
    {
      sum2 += arr2[j];
    }

    int len = 0;
    if (s1 >= s2)
    {
      len = s2;
    }
    else
    {
      len = s1;
    }

    // Sort the arrays arr1[] and arr2[]
    Arrays.sort(arr1);
    Arrays.sort(arr2);

    int j = 0, k = s2 - 1, count = 0;

    // Traverse the array arr[]
    for (int i = 0; i < len; i++)
    {

      // If the sum1 is less than
      // or equal to sum2
      if (sum1 <= sum2)
      {

        // Swapping the elements
        if (arr2[k] >= arr1[i])
        {

          // Update the sum1 and sum2
          int dif1 = arr1[j], dif2 = arr2[k];
          sum1 -= dif1;
          sum1 += dif2;

          sum2 -= dif2;
          sum2 += dif1;
          j++;
          k--;

          // Increment the count
          count++;
        }
        else
        {
          break;
        }
      }
      else
      {
        break;
      }
    }

    // Return the final count
    return count;
  }

  // Driver Code
  public static void main(String[] args)
  {

    int[] arr1 = new int[] { 1, 3, 2, 4 };
    int[] arr2 = new int[] { 6, 7, 8 };
    int N = arr1.length;
    int M = arr2.length;

    // Function Call
    System.out.println(maximumCount(arr1, arr2, N, M));
  }
}

// This code is contributed by dharanendralv23
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the minimum count
# of swaps required between the two
# arrays to make the sum of arr1[]
# greater than that of arr2[]
def maximumCount(arr1, arr2, s1, s2) :

    # Stores the sum of the two arrays
    sum1 = 0
    sum2 = 0

    # Calculate sum of arr1[]
    for i in range(s1):
        sum1 += arr1[i]

    # Calculate sum of arr2[]
    for j in range(s2):
        sum2 += arr2[j]

    len = 0
    if (s1 >= s2) :
        lenn = s2  
    else :
        lenn = s1

    # Sort the arrays arr1[] and arr2[]
    arr1.sort();
    arr2.sort();
    j = 0
    k = s2 - 1
    count = 0

    # Traverse the array arr[]
    for i in range(lenn):

        # If the sum1 is less than
        # or equal to sum2
        if (sum1 <= sum2) :

            # Swapping the elements
            if (arr2[k] >= arr1[i]) :

                # Update the sum1 and sum2
                dif1 = arr1[j]
                dif2 = arr2[k]
                sum1 -= dif1
                sum1 += dif2
                sum2 -= dif2
                sum2 += dif1
                j += 1
                k -= 1

                # Increment the count
                count += 1           
            else :
                break          
        else :
            break

    # Return the final count
    return count

# Driver Code

arr1 = [ 1, 3, 2, 4 ]
arr2 = [ 6, 7, 8 ]
N = len(arr1)
M = len(arr2)

# Function Call
print(maximumCount(arr1, arr2, N, M))

# This code is contributed by sanjoy_62
```

## C#

```
// C# program for the above approach
using System;
class GFG {

  // Function to find the minimum count
  // of swaps required between the two
  // arrays to make the sum of arr1[]
  // greater than that of arr2[]
  static int maximumCount(int[] arr1, int[] arr2, int s1,
                          int s2)
  {
    // Stores the sum of the two arrays
    int sum1 = 0, sum2 = 0;

    // Calculate sum of arr1[]
    for (int i = 0; i < s1; i++) {
      sum1 += arr1[i];
    }

    // Calculate sum of arr2[]
    for (int a = 0; a < s2; a++) {
      sum2 += arr2[a];
    }

    int len = 0;
    if (s1 >= s2) {
      len = s2;
    }
    else {
      len = s1;
    }

    // Sort the arrays arr1[] and arr2[]
    Array.Sort(arr1);
    Array.Sort(arr2);

    int j = 0, k = s2 - 1, count = 0;

    // Traverse the array arr[]
    for (int i = 0; i < len; i++) {

      // If the sum1 is less than
      // or equal to sum2
      if (sum1 <= sum2) {

        // Swapping the elements
        if (arr2[k] >= arr1[i]) {

          // Update the sum1 and sum2
          int dif1 = arr1[j], dif2 = arr2[k];
          sum1 -= dif1;
          sum1 += dif2;

          sum2 -= dif2;
          sum2 += dif1;
          j++;
          k--;

          // Increment the count
          count++;
        }
        else {
          break;
        }
      }
      else {
        break;
      }
    }

    // Return the final count
    return count;
  }

  // Driver Code
  static public void Main()
  {

    int[] arr1 = new int[] { 1, 3, 2, 4 };
    int[] arr2 = new int[] { 6, 7, 8 };
    int N = arr1.Length;
    int M = arr2.Length;

    // Function Call
    Console.WriteLine(maximumCount(arr1, arr2, N, M));
  }
}

// This code is contributed by dharanendralv23
```

## java 描述语言

```
<script>

// Javascript program of the above approach

  // Function to find the minimum count
  // of swaps required between the two
  // arrays to make the sum of arr1[]
  // greater than that of arr2[]
  function maximumCount( arr1, arr2, s1,
                          s2)
  {

    // Stores the sum of the two arrays
    let sum1 = 0, sum2 = 0;

    // Calculate sum of arr1[]
    for (let i = 0; i < s1; i++)
    {
      sum1 += arr1[i];
    }

    // Calculate sum of arr2[]
    for (let j = 0; j < s2; j++)
    {
      sum2 += arr2[j];
    }

    let len = 0;
    if (s1 >= s2)
    {
      len = s2;
    }
    else
    {
      len = s1;
    }

    // Sort the arrays arr1[] and arr2[]
    arr1.sort();
    arr2.sort();

    let j = 0, k = s2 - 1, count = 0;

    // Traverse the array arr[]
    for (let i = 0; i < len; i++)
    {

      // If the sum1 is less than
      // or equal to sum2
      if (sum1 <= sum2)
      {

        // Swapping the elements
        if (arr2[k] >= arr1[i])
        {

          // Update the sum1 and sum2
          let dif1 = arr1[j], dif2 = arr2[k];
          sum1 -= dif1;
          sum1 += dif2;

          sum2 -= dif2;
          sum2 += dif1;
          j++;
          k--;

          // Increment the count
          count++;
        }
        else
        {
          break;
        }
      }
      else
      {
        break;
      }
    }

    // Return the final count
    return count;
  }

    // Driver Code

    let arr1 = [ 1, 3, 2, 4 ];
    let arr2 = [ 6, 7, 8 ];
    let N = arr1.length;
    let M = arr2.length;

    // Function Call
    document.write(maximumCount(arr1, arr2, N, M));

</script>
```

**输出:**

```
1
```

***时间复杂度:**O(N * log N+M * log M)*
T5**辅助空间:** O(1)