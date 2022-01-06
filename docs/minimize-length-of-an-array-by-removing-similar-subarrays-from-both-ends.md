# 通过从两端移除相似的子阵列来最小化阵列的长度

> 原文:[https://www . geesforgeks . org/通过从两端移除相似子阵列来最小化阵列长度/](https://www.geeksforgeeks.org/minimize-length-of-an-array-by-removing-similar-subarrays-from-both-ends/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是通过从包含相同单个元素的数组的开始和结束处重复移除子数组来最小化给定数组的[长度。](https://www.geeksforgeeks.org/how-to-determine-length-or-size-of-an-array-in-java/)

**示例:**

> **输入:** arr[] = { 3，1，2，1，1，2，1，3 }
> T3】输出:0
> T6】解释:
> 
> 1.  由于第一个和最后一个元素都是 3，删除它们会将 arr[]修改为{1，2，1，1，2，1}。
> 2.  由于第一个和最后一个元素都是 1，删除它们会将 arr[]修改为{2，1，1，2}。
> 3.  由于第一个和最后一个元素都是 2，删除它们会将 arr[]修改为{1，1}。
> 4.  由于第一个和最后一个元素都是 1，删除它们会将 arr[]修改为{}。
> 
> **输入:** arr[] = {1，1，2，3，3，1，2，2，1}
> **输出:** 3
> **解释:**
> 
> 1.  从开头删除{ 1，1 }并从结尾删除{ 1 }会将 arr[]修改为{ 2，3，3，1，2，2 }。
> 2.  从开头删除{ 2 }并从结尾删除{ 2，2 }会将 arr[]修改为{ 3，3，1 }。
> 3.  无法删除更多元素。

**进场:**思路是用[两点手法](https://www.geeksforgeeks.org/two-pointers-technique/)解决问题。按照以下步骤解决问题:

1.  初始化两个指针**前= 0** 、**后= N–1**到[同时从两端遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)。
2.  [横阵](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)T2【arr】至**前<后:**
    *   如果两个元素不同，则[断开](https://www.geeksforgeeks.org/break-statement-cc/)循环。
    *   否则，递增**前**指针，递减**后**指针，直到它们指向与当前元素不同的元素。
3.  将两个指针位置之差打印为数组的最小长度。

下面是上述方法的实现:

## C++

```
// C++ program for
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to minimize length of
// the array by removing similar
// subarrays from both ends of the array
void findMinLength(int arr[], int N)
{
    // Initialize two pointers
    int front = 0, back = N - 1;

    while (front < back) {

        // Stores the current integer
        int x = arr[front];

        // Check if the elements at
        // both ends are same or not
        if (arr[front] != arr[back])
            break;

        // Move the front pointer
        while (arr[front] == x
               && front <= back)
            front++;

        // Move the rear pointer
        while (arr[back] == x
               && front <= back)
            back--;
    }

    // Print the minimized length of the array
    cout << back - front + 1 << endl;
}

// Driver Code
int main()
{
    // Input
    int arr[] = { 1, 1, 2, 3, 3, 1, 2, 2, 1 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call to find the
    // minimized length of the array
    findMinLength(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

  // Function to minimize length of
  // the array by removing similar
  // subarrays from both ends of the array
  static void findMinLength(int arr[], int N)
  {
    // Initialize two pointers
    int front = 0, back = N - 1;
    while (front < back) {

      // Stores the current integer
      int x = arr[front];

      // Check if the elements at
      // both ends are same or not
      if (arr[front] != arr[back])
        break;

      // Move the front pointer
      while (arr[front] == x
             && front <= back)
        front++;

      // Move the rear pointer
      while (arr[back] == x
             && front <= back)
        back--;
    }

    // Print the minimized length of the array
    System.out.println( back - front + 1 );
  }

  // Driver Code
  public static void main(String[] args)
  {

    // Input
    int arr[] = { 1, 1, 2, 3, 3, 1, 2, 2, 1 };
    int N = arr.length;

    // Function call to find the
    // minimized length of the array
    findMinLength(arr, N);
  }
}

// This code is contributed by sanjoy_62.
```

## 蟒蛇 3

```
# Python program for
# the above approach

# Function to minimize length of
# the array by removing similar
# subarrays from both ends of the array
def findMinLength(arr, N):

    # Initialize two pointers
    front = 0
    back = N - 1
    while (front < back):

        # Stores the current integer
        x = arr[front]

        # Check if the elements at
        # both ends are same or not
        if arr[front] != arr[back]:
            break

            # Move the front pointer
        while (arr[front] == x and front <= back):
            front += 1

            # Move the rear pointer
        while (arr[back] == x and front <= back):
            back -= 1

    # Print the minimized length of the array
    print(back - front + 1)

# Driver Code
# Input
arr = [1, 1, 2, 3, 3, 1, 2, 2, 1]
N = len(arr)

# Function call to find the
# minimized length of the array
findMinLength(arr, N)

# This code is contributed by sudhanshugupta2019a.
```

## C#

```
// C# program for the above approach
using System;
public class GFG
{

  // Function to minimize length of
  // the array by removing similar
  // subarrays from both ends of the array
  static void findMinLength(int []arr, int N)
  {

    // Initialize two pointers
    int front = 0, back = N - 1;
    while (front < back)
    {

      // Stores the current integer
      int x = arr[front];

      // Check if the elements at
      // both ends are same or not
      if (arr[front] != arr[back])
        break;

      // Move the front pointer
      while (arr[front] == x
             && front <= back)
        front++;

      // Move the rear pointer
      while (arr[back] == x
             && front <= back)
        back--;
    }

    // Print the minimized length of the array
    Console.WriteLine( back - front + 1 );
  }

  // Driver Code
  public static void Main(String[] args)
  {

    // Input
    int []arr = { 1, 1, 2, 3, 3, 1, 2, 2, 1 };
    int N = arr.Length;

    // Function call to find the
    // minimized length of the array
    findMinLength(arr, N);
  }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
// JavaScript program for
// the above approach

// Function to minimize length of
// the array by removing similar
// subarrays from both ends of the array
function findMinLength(arr, N)
{

    // Initialize two pointers
    let front = 0, back = N - 1;
    while (front < back)
    {

        // Stores the current integer
        let x = arr[front];

        // Check if the elements at
        // both ends are same or not
        if (arr[front] != arr[back])
            break;

        // Move the front pointer
        while (arr[front] == x
            && front <= back)
            front++;

        // Move the rear pointer
        while (arr[back] == x
            && front <= back)
            back--;
    }

    // Print the minimized length of the array
    document.write(back - front + 1);
    document.write("<br>");
}

// Driver Code

    // Input
    let arr = [ 1, 1, 2, 3, 3, 1, 2, 2, 1 ];
    let N = arr.length;

    // Function call to find the
    // minimized length of the array
    findMinLength(arr, N);

// This code is contributed by Surbhi Tyagi.
</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)