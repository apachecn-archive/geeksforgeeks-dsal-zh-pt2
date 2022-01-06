# 通过最多一次交换，数组的字典最小排列

> 原文:[https://www . geeksforgeeks . org/按字典顺序排列的最大可能置换数组/](https://www.geeksforgeeks.org/lexicographically-smallest-permutation-of-the-array-possible-by-at-most-one-swap/)

给定一个代表第一个自然数**的[排列](https://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/)的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是通过最多交换一对数组元素来找到给定数组 **arr[]** 的字典最小排列。如果无法使数组按字典顺序变小，则打印 **"-1"** 。**

****示例:****

> ****输入:** arr[] = {3，2，1，4}
> **输出:** 1 2 3 4
> **解释:**交换索引 2 和 0 处的元素，修改后的数组是{1，2，3，4}，这是给定数组 arr[]，在字典上的最小排列。**
> 
> ****输入:** arr[] = {1，2，3，4}
> **输出:** -1**

****方法:**思路是找到第一个不在正确位置的数组元素，即**arr【I】**与索引 **(i + 1)** 不一样，换成正确位置的元素。按照以下步骤解决此问题:**

*   **[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**找到索引 **i** ，使得**arr【I】**不等于 **(i + 1)** ，说 **idx** ，将 **(i + 1)** 存储在一个变量中，说 **ele** 。**
*   **现在，找到 **ele** 的索引，说 **newIdx** 。**
*   **完成上述步骤后，存在两个索引 **idx** 和 **newIdx** 。可以通过在索引 **idx** 和**新 Idx** 处交换元素来形成数组的字典最小排列。现在，[打印数组 **arr[]**](https://www.geeksforgeeks.org/c-program-to-print-an-array-using-recursion/) 。否则，打印**-1”**。**

**下面是上述方法的实现:**

## **C++14**

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
#include <iostream>
using namespace std;

// Function to print the
// elements of the array arr[]
void print(int arr[], int N)
{
    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {
        cout << arr[i] << " ";
    }
}

// Function to convert given array to
// lexicographically smallest permutation
// possible by swapping at most one pair
void makeLexicographically(int arr[], int N)
{
    // Stores the index of the first
    // element which is not at its
    // correct position
    int index = 0;
    int temp = 0;

    // Checks if any such array
    // element exists or not
    int check = 0;
    int condition = 0;

    int element = 0;

    // Traverse the given array
    for (int i = 0; i < N; ++i) {

        // If element is found at i
        if (element == arr[i]) {
            check = i;
            break;
        }

        // If the first array is
        // not in correct position
        else if (arr[i] != i + 1 && check == 0) {

            // Store the index of
            // the first elements
            index = i;
            check = 1;
            condition = -1;

            // Store the index of
            // the first element
            element = i + 1;
        }
    }

    // Swap the pairs
    if (condition == -1) {

        temp = arr[index];
        arr[index] = arr[check];
        arr[check] = temp;
    }

    // Print the array
    print(arr, N);
}

// Driver code
int main()
{

    // Given array
    int arr[] = { 1, 2, 3, 4 };

    // Store the size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    makeLexicographically(arr, N);
    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.io.*;

class GFG {

    // Function to print the
    // elements of the array arr[]
    static void print(int arr[])
    {
        // Traverse the array arr[]
        for (int element : arr) {
            System.out.print(element + " ");
        }
    }

    // Function to convert given array to
    // lexicographically smallest permutation
    // possible by swapping at most one pair
    static void makeLexicographically(
        int arr[], int length)
    {
        // Stores the index of the first
        // element which is not at its
        // correct position
        int index = 0;
        int temp = 0;

        // Checks if any such array
        // element exists or not
        int check = 0;
        int condition = 0;

        int element = 0;

        // Traverse the given array
        for (int i = 0; i < length; ++i) {

            // If element is found at i
            if (element == arr[i]) {
                check = i;
                break;
            }

            // If the first array is
            // not in correct position
            else if (arr[i] != i + 1
                     && check == 0) {

                // Store the index of
                // the first elements
                index = i;
                check = 1;
                condition = -1;

                // Store the index of
                // the first element
                element = i + 1;
            }
        }

        // Swap the pairs
        if (condition == -1) {

            temp = arr[index];
            arr[index] = arr[check];
            arr[check] = temp;
        }

        // Print the array
        print(arr);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 1, 2, 3, 4 };
        int N = arr.length;

        makeLexicographically(arr, N);
    }
}
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# Function to print the
# elements of the array arr[]
def printt(arr, N) :

    # Traverse the array arr[]
    for i in range(N):
        print(arr[i], end = " ")

# Function to convert given array to
# lexicographically smallest permutation
# possible by swapping at most one pair
def makeLexicographically(arr, N) :

    # Stores the index of the first
    # element which is not at its
    # correct position
    index = 0
    temp = 0

    # Checks if any such array
    # element exists or not
    check = 0
    condition = 0
    element = 0

    # Traverse the given array
    for i in range(N):

        # If element is found at i
        if (element == arr[i]) :
            check = i
            break

        # If the first array is
        # not in correct position
        elif (arr[i] != i + 1 and check == 0) :

            # Store the index of
            # the first elements
            index = i
            check = 1
            condition = -1

            # Store the index of
            # the first element
            element = i + 1

    # Swap the pairs
    if (condition == -1) :
        temp = arr[index]
        arr[index] = arr[check]
        arr[check] = temp

    # Print the array
    printt(arr, N)

# Driver code

# Given array
arr = [ 1, 2, 3, 4 ]

# Store the size of the array
N = len(arr)

makeLexicographically(arr, N)

# This code is contributed by code_hunt.
```

## **C#**

```
// C# program for the above approach
using System;

class GFG {

  // Function to print the
  // elements of the array arr[]
  static void print(int[] arr)
  {

    // Traverse the array arr[]
    foreach (int element in arr) {
      Console.Write(element + " ");
    }
  }

  // Function to convert given array to
  // lexicographically smallest permutation
  // possible by swapping at most one pair
  static void makeLexicographically(
    int []arr, int length)
  {

    // Stores the index of the first
    // element which is not at its
    // correct position
    int index = 0;
    int temp = 0;

    // Checks if any such array
    // element exists or not
    int check = 0;
    int condition = 0;

    int element = 0;

    // Traverse the given array
    for (int i = 0; i < length; ++i) {

      // If element is found at i
      if (element == arr[i]) {
        check = i;
        break;
      }

      // If the first array is
      // not in correct position
      else if (arr[i] != i + 1
               && check == 0) {

        // Store the index of
        // the first elements
        index = i;
        check = 1;
        condition = -1;

        // Store the index of
        // the first element
        element = i + 1;
      }
    }

    // Swap the pairs
    if (condition == -1) {

      temp = arr[index];
      arr[index] = arr[check];
      arr[check] = temp;
    }

    // Print the array
    print(arr);
  }

  // Driver Code
  public static void Main(string[] args)
  {
    int[] arr = { 1, 2, 3, 4 };
    int N = arr.Length;

    makeLexicographically(arr, N);
  }
}

// This code is contributed by ukasp.
```

## **java 描述语言**

```
<script>

// Javascript implementation of the above approach

// Function to print the
// elements of the array arr[]
function print(arr, N)
{
    // Traverse the array arr[]
    for (i = 0; i < N; i++) {
        document.write(arr[i]+ " ");
    }
}

// Function to convert given array to
// lexicographically smallest permutation
// possible by swapping at most one pair
function makeLexicographically(arr, N)
{
    // Stores the index of the first
    // element which is not at its
    // correct position
    var index = 0;
    var temp = 0;

    // Checks if any such array
    // element exists or not
    var check = 0;
    var condition = 0;

    var element = 0;

    // Traverse the given array
    for (i = 0; i < N; ++i) {

        // If element is found at i
        if (element == arr[i]) {
            check = i;
            break;
        }

        // If the first array is
        // not in correct position
        else if (arr[i] != i + 1 && check == 0) {

            // Store the index of
            // the first elements
            index = i;
            check = 1;
            condition = -1;

            // Store the index of
            // the first element
            element = i + 1;
        }
    }

    // Swap the pairs
    if (condition == -1) {

        temp = arr[index];
        arr[index] = arr[check];
        arr[check] = temp;
    }

    // Print the array
    print(arr, N);
}

// Driver code

    // Given array
    var arr = [1, 2, 3, 4]

    // Store the size of the array
    var N = arr.length;

    makeLexicographically(arr, N);

// This code is contributed by SURENDRA_GANGWAR.
</script>
```

****Output:** 

```
1 2 3 4
```** 

*****时间复杂度:**O(N)*
T5**辅助空间:** O(1)**