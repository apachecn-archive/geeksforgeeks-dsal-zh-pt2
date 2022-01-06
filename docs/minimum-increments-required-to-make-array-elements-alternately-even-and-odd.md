# 使阵列元素交替为偶数和奇数所需的最小增量

> 原文:[https://www . geeksforgeeks . org/最小增量-制作数组元素所需-交替-偶数和奇数/](https://www.geeksforgeeks.org/minimum-increments-required-to-make-array-elements-alternately-even-and-odd/)

给定一个由 **N** 个正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找到使数组 **arr[]** 成为偶数和奇数交替序列所需的最小增量数。

**示例:**

> **输入:** arr[] = {1，4，6，8，9，5}
> **输出:** 2
> **解释:**
> 递增 arr[2]将 arr[]修改为{1，4，7，8，9，5}。
> 将 arr[5]增加 1 会将 arr[]修改为{1，4，7，8，9，6}。
> 
> **输入:** arr[] = {3，5，7，9，4，2}
> **输出:** 3
> **解释:**
> 将 arr[0]递增 1 将 arr[]修改为{4，5，7，9，4，2}。
> 将 arr[2]增加 1 会将 arr[]修改为{4，5，8，9，4，2}。
> 将 arr[5]增加 1 会将 arr[]修改为{4，5，8，9，4，3}。

**方法:**为了解决给定的问题，思路是检查使阵列元素奇数和偶数交替以及偶数和奇数交替所需的增量数量。最后，打印获得的两个增量计数的最小值。按照以下步骤解决问题:

*   初始化一个变量，比如说 **cnt** 为 **0** ，以存储将数组转换为偶数和奇数交替序列所需的增量计数，反之亦然。
*   [使用变量 **i** 遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**，并执行以下步骤:
    *   如果 [**i** 为偶数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)且**arr【I】**为奇数，则将 **cnt** 递增 1。
    *   如果 **i** 为奇数，**arr【I】**为偶数，则将 **cnt** 增加 1。
*   完成上述步骤后， **cnt** 和**(N–CNT)**的最小值即为所需结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
using namespace std;

// Function to find the minimum number of
// increments required to make the array
// even-odd alternately or vice-versa
int minIncr(int *arr,int n)
{

    // Store the minimum number of
    // increments required
    int forEven = 0;

    // Traverse the array arr[]
    for(int i = 0; i < n; i++)
    {

        // Increment forEven if even
        // element is present at an
        // odd index
        if(i % 2){
            if((arr[i] % 2) == 0)
                forEven += 1;
        }

        // Increment forEven if odd
        // element is present at an
        // even index
        else{
            if(arr[i] % 2)
                forEven += 1;
        }
    }

    // Return the minimum number of increments
    return min(forEven, n - forEven);
}

int main()
{

    // Driver Code
    int arr[] = {1, 4, 6, 8, 9, 5};
    int n = sizeof(arr)/sizeof(arr[0]);
    cout<<minIncr(arr,n);
    return 0;
}

// This code is contributed by rohitsingh07052.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to find the minimum number of
// increments required to make the array
// even-odd alternately or vice-versa
static int minIncr(int []arr, int n)
{

    // Store the minimum number of
    // increments required
    int forEven = 0;

    // Traverse the array arr[]
    for(int i = 0; i < n; i++)
    {

        // Increment forEven if even
        // element is present at an
        // odd index
        if (i % 2 == 1)
        {
            if ((arr[i] % 2) == 0)
                forEven += 1;
        }

        // Increment forEven if odd
        // element is present at an
        // even index
        else
        {
            if (arr[i] % 2 == 1)
                forEven += 1;
        }
    }

    // Return the minimum number of increments
    return Math.min(forEven, n - forEven);
}

// Driver Code
public static void main (String[] args)
{
    int arr[] = { 1, 4, 6, 8, 9, 5 };
    int n = arr.length;

    System.out.println(minIncr(arr,n));
}
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the minimum number of
# increments required to make the array
# even-odd alternately or vice-versa
def minIncr(arr):

    # Store the minimum number of
    # increments required
    forEven = 0

    # Traverse the array arr[]
    for i in range(len(arr)):

        # Increment forEven if even
        # element is present at an
        # odd index
        if i % 2:
            if not arr[i] % 2:
                forEven += 1

        # Increment forEven if odd
        # element is present at an
        # even index
        else:
            if arr[i] % 2:
                forEven += 1

    # Return the minimum number of increments
    return min(forEven, len(arr)-forEven)

# Driver Code
arr = [1, 4, 6, 8, 9, 5]
print(minIncr(arr))
```

## C#

```
// C# program for the above approach
using System;
public class GFG
{

  // Function to find the minimum number of
  // increments required to make the array
  // even-odd alternately or vice-versa
  static int minIncr(int []arr, int n)
  {

    // Store the minimum number of
    // increments required
    int forEven = 0;

    // Traverse the array []arr
    for(int i = 0; i < n; i++)
    {

      // Increment forEven if even
      // element is present at an
      // odd index
      if (i % 2 == 1)
      {
        if ((arr[i] % 2) == 0)
          forEven += 1;
      }

      // Increment forEven if odd
      // element is present at an
      // even index
      else
      {
        if (arr[i] % 2 == 1)
          forEven += 1;
      }
    }

    // Return the minimum number of increments
    return Math.Min(forEven, n - forEven);
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int []arr = { 1, 4, 6, 8, 9, 5 };
    int n = arr.Length;

    Console.WriteLine(minIncr(arr,n));
  }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the minimum number of
// increments required to make the array
// even-odd alternately or vice-versa
function minIncr(arr, n)
{

    // Store the minimum number of
    // increments required
    let forEven = 0;

    // Traverse the array arr[]
    for(let i = 0; i < n; i++)
    {

        // Increment forEven if even
        // element is present at an
        // odd index
        if(i % 2){
            if((arr[i] % 2) == 0)
                forEven += 1;
        }

        // Increment forEven if odd
        // element is present at an
        // even index
        else{
            if(arr[i] % 2)
                forEven += 1;
        }
    }

    // Return the minimum number of increments
    return Math.min(forEven, n - forEven);
}

// Driver Code
let arr = [1, 4, 6, 8, 9, 5];
let n = arr.length;
document.write(minIncr(arr,n));

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)