# 通过使给定数组不递减来实现最大可能和

> 原文:[https://www . geeksforgeeks . org/最大可能通过制作给定数组实现的总和-非递减/](https://www.geeksforgeeks.org/maximum-sum-possible-by-making-given-array-non-decreasing/)

给定一个[数组](https://www.geeksforgeeks.org/array-data-structure/) arr[]，任务是通过将数组元素重复递减 1，从给定数组中获得一个最大和的[非递减数组](https://www.geeksforgeeks.org/check-whether-an-array-can-be-made-strictly-decreasing-by-modifying-at-most-one-element/)。

**说明:**

> **输入:** arr[] = {1，5，2，3，4}
> **输出:** 12
> **解释:**通过将 5 减 2 将给定数组修改为{1，2，2，3，4}，以从非递减数组中获得最大可能和。
> 
> **输入:** arr[] = {1，2，5，9，-3}
> **输出:** -15

**方法:**按照以下步骤解决问题:

*   [反向遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)。
*   将每对相邻元素与[进行比较，检查数组是否不递减](https://www.geeksforgeeks.org/check-if-an-array-is-increasing-or-decreasing/)，即检查**a[I–1]≤a[I]。**
*   如果发现为假，分配**一个[I–1]=一个[i]** 。
*   完成上述步骤后，p[rin t]为修改后数组的和。

下面是上述方法的实现:

## C++

```
// C++ program for the
// above approach
#include <bits/stdc++.h>
using namespace std;
int maximumSum(vector<int> a,
               int n)
{
  //Traverse the array in
  // reverse
  for (int i = n - 1; i >= 0; i--)
  {
    //If a[i] is decreasing
    if (!(a[i - 1] <= a[i]))
      a[i - 1] = a[i];
  }

  int sum = 0;

  for(int i : a) sum += i;

  //Return sum of the array
  return sum;
}

//Driver code
int main()
{
  //Given array arr[]
  vector<int> arr = {1, 5, 2, 3, 4};
  int N = arr.size();

  cout << (maximumSum(arr, N));
}

// This code is contributed by Mohit Kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach
import java.util.*;
class GFG{
static int maximumSum(int[] a,
                      int n)
{
  //Traverse the array in
  // reverse
  for (int i = n - 1; i > 0; i--)
  {
    //If a[i] is decreasing
    if (!(a[i - 1] <= a[i]))
      a[i - 1] = a[i];
  }

  int sum = 0;

  for(int i : a) sum += i;

  //Return sum of the array
  return sum;
}

//Driver code
public static void main(String[] args)
{
  //Given array arr[]
  int[] arr = {1, 5, 2, 3, 4};

  int N = arr.length;
  System.out.print(maximumSum(arr, N));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program for the
# above approach

def maximumSum(a, n):

    # Traverse the array in reverse
    for i in range(n-1, 0, -1):

        # If a[i] is decreasing
        if not a[i-1] <= a[i]:
            a[i-1] = a[i]

    # Return sum of the array
    return sum(a)

# Driver Code
if __name__ == '__main__':

    arr = [1, 5, 2, 3, 4]
    N = len(arr)

    print(maximumSum(arr, N))
```

## C#

```
// C# program for the
// above approach
using System;

class GFG{

static int maximumSum(int[] a, int n)
{

    // Traverse the array in
    // reverse
    for(int i = n - 1; i > 0; i--)
    {

        // If a[i] is decreasing
        if (!(a[i - 1] <= a[i]))
            a[i - 1] = a[i];
    }

    int sum = 0;

    foreach(int i in a) sum += i;

    // Return sum of the array
    return sum;
}

// Driver code
public static void Main(String[] args)
{

    // Given array []arr
    int[] arr = { 1, 5, 2, 3, 4 };

    int N = arr.Length;

    Console.Write(maximumSum(arr, N));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// JavaScript program for the
// above approach

function maximumSum(a,n)
{
    //Traverse the array in
  // reverse
  for (let i = n - 1; i > 0; i--)
  {
    //If a[i] is decreasing
    if (!(a[i - 1] <= a[i]))
      a[i - 1] = a[i];
  }

  let sum = 0;

  for(let i=0;i< a.length;i++) sum += a[i];

  //Return sum of the array
  return sum;
}

//Driver code
let arr=[1, 5, 2, 3, 4];
let N = arr.length;
document.write(maximumSum(arr, N));

// This code is contributed by patel2127

</script>
```

**Output:** 

```
12
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)