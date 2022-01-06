# 从一个数组中找出一个三元组(I，j，k)，使得 i < j < k 和 arr【I】<arr【j】>arr【k】

> 原文:[https://www . geeksforgeeks . org/find-a-triple-I-j-k-from-a-array-j-k-so-I-j-k-and-arri-arr j-arrk/](https://www.geeksforgeeks.org/find-a-triplet-i-j-k-from-an-array-such-that-i-j-k-and-arri-arrj-arrk/)

给定一个由第一个 **N** 自然数的[排列组成的](https://www.geeksforgeeks.org/check-if-an-array-is-a-permutation-of-numbers-from-1-to-n/)[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是从给定数组中找到任意三元组 **(i，j，k)** ，使得**0≤I<j<k≤(N–1)**和**arr【I】<arr【j】**和**arr【j】如果不存在这样的三元组，则打印【T16 "-" 1 "**。

**示例:**

> **输入:** arr[] = {4，3，5，2，1，6 }
> T3】输出:1 2 3
> T6】解释:对于三元组(1，2，3)，arr[2] > arr[1](即 5 > 3)和 arr[2] > arr[3](即 5 > 2)。
> 
> **输入:** arr[] = {3，2，1}
> **输出:** -1

**天真方法:**最简单的方法是[从给定的数组中生成所有可能的三元组](https://www.geeksforgeeks.org/python-ways-to-create-triplets-from-given-list/)**arr【】**如果存在任何满足给定条件的三元组，则打印该三元组。否则，打印**-1”**。

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(1)*

**有效方法:**上述方法可以通过观察阵列仅包含来自范围**【1，N】**的不同元素来优化。如果存在任何具有给定标准的三元组，那么该三元组必须彼此相邻。

因此，想法是[在范围**【1，N–2】**上遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**，如果存在任何索引 I 使得**arr【I–1】<arr【I】**和**arr【I】>arr【I+1】**，则打印三元组**(I–1，I，i + 1)** 作为结果。否则，打印**-1”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find a triplet such
// that i < j < k and arr[i] < arr[j]
// and arr[j] > arr[k]
void print_triplet(int arr[], int n)
{
    // Traverse the array
    for (int i = 1; i <= n - 2; i++) {

        // Condition to satisfy for
        // the resultant triplet
        if (arr[i - 1] < arr[i]
            && arr[i] > arr[i + 1]) {

            cout << i - 1 << " "
                 << i << " " << i + 1;
            return;
        }
    }

    // Otherwise, triplet doesn't exist
    cout << -1;
}

// Driver Code
int main()
{
    int arr[] = { 4, 3, 5, 2, 1, 6 };
    int N = sizeof(arr) / sizeof(int);
    print_triplet(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find a triplet such
// that i < j < k and arr[i] < arr[j]
// and arr[j] > arr[k]
static void print_triplet(int arr[], int n)
{

    // Traverse the array
    for(int i = 1; i <= n - 2; i++)
    {

        // Condition to satisfy for
        // the resultant triplet
        if (arr[i - 1] < arr[i] &&
            arr[i] > arr[i + 1])
        {
            System.out.print(i - 1 + " " + i + " " +
                            (i + 1));
            return;
        }
    }

    // Otherwise, triplet doesn't exist
    System.out.print(-1);
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 4, 3, 5, 2, 1, 6 };
    int N = arr.length;

    print_triplet(arr, N);
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find a triplet such
# that i < j < k and arr[i] < arr[j]
# and arr[j] > arr[k]
def print_triplet(arr, n):

    # Traverse the array
    for i in range(1, n - 1):

        # Condition to satisfy for
        # the resultant triplet
        if (arr[i - 1] < arr[i] and
            arr[i] > arr[i + 1]):
            print(i - 1, i, i + 1)
            return

    # Otherwise, triplet doesn't exist
    print(-1)

# Driver Code
if __name__ == "__main__":

    arr = [ 4, 3, 5, 2, 1, 6 ]
    N = len(arr)

    print_triplet(arr, N)

# This code is contributed by chitranayal
```

## C#

```
// C# program to implement
// the above approach
using System;
public class GFG
{

// Function to find a triplet such
// that i < j < k and arr[i] < arr[j]
// and arr[j] > arr[k]
static void print_triplet(int[] arr, int n)
{

    // Traverse the array
    for(int i = 1; i <= n - 2; i++)
    {

        // Condition to satisfy for
        // the resultant triplet
        if (arr[i - 1] < arr[i] &&
            arr[i] > arr[i + 1])
        {
            Console.Write(i - 1 + " " + i + " " +
                            (i + 1));
            return;
        }
    }

    // Otherwise, triplet doesn't exist
    Console.Write(-1);
}

// Driver Code
public static void Main(String[] args)
{
    int[] arr = { 4, 3, 5, 2, 1, 6 };
    int N = arr.Length;

    print_triplet(arr, N);
}
}

// This code is contributed by splevel62.
```

## java 描述语言

```
<script>

      // JavaScript program to implement
      // the above approach

      // Function to find a triplet such
      // that i < j < k and arr[i] < arr[j]
      // and arr[j] > arr[k]
      function print_triplet(arr, n)
      {
        // Traverse the array
        for (var i = 1; i <= n - 2; i++)
        {
          // Condition to satisfy for
          // the resultant triplet
          if (arr[i - 1] < arr[i] && arr[i] > arr[i + 1])
          {
            document.write(i - 1 + " " + i + " " + (i + 1));
            return;
          }
        }

        // Otherwise, triplet doesn't exist
        document.write(-1);
      }

      // Driver Code
      var arr = [4, 3, 5, 2, 1, 6];
      var N = arr.length;

      print_triplet(arr, N);

</script>
```

**Output:** 

```
1 2 3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)