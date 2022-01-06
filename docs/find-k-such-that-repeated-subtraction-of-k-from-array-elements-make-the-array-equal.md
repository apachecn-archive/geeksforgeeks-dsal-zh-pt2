# 求 K，使得从数组元素中重复减去 K，使数组相等

> 原文:[https://www . geeksforgeeks . org/find-k-so-从数组元素中重复减去 k-使数组相等/](https://www.geeksforgeeks.org/find-k-such-that-repeated-subtraction-of-k-from-array-elements-make-the-array-equal/)

给定一个大小为 **N** 的数组 **arr[]** ，任务是找到一个整数 **K** 的值，这样它从数组元素中的重复减法将使所有数组元素处于最小运算中。

**示例:**

> **输入:** arr[] = {5，3，3，7}
> **输出:** 2
> **解释:**至少必须执行 2 次运算:
> 第一次运算:从索引{0，3}处的元素中减去 2，arr[] = {3，3，3，3}，5}
> 第二次运算:从索引 3 处的元素中减去 2，arr[] = {3，3，3 }，3}
> 所以，K 的值= 2
> 
> **输入:** arr[] = {-1，0，-1，0，-1 }
> T3】输出: 1

**方法:**要使数组中的所有元素 **arr** 相等，需要将所有元素更改为数组中的最小值。所以，所有数组元素与最小元素之差的 [gcd](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) 将是 **K** 的值。现在，要解决以下问题，请按照以下步骤操作:

1.  创建一个变量 **mn** 来存储数组 **arr** 中的最小元素。
2.  现在，遍历数组 **arr** ，找到所有数组元素与 **mn** 之间差异的 gcd。将该值存储在变量 **K.** 中
3.  返回 **K** ，作为这个问题的答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the value to be
// subtracted from array elements
// to make all elements equal
int findtheValue(int arr[], int N)
{
    // Miniumum element in the array
    int mn = *min_element(arr, arr + N);

    int K = arr[0] - mn;

    // Traverse the array to find the gcd
    // of the differences between
    // all array elements and mn
    for (int i = 1; i < N; ++i) {
        K = __gcd(K, arr[i] - mn);
    }

    return K;
}

// Driver Code
int main()
{
    int arr[] = { 5, 3, 3, 7 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << findtheValue(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG {

    static int gcd(int a, int b)
    {
        if (b == 0)
            return a;
        return gcd(b, a % b);
    }

    public static int getMin(int[] inputArray){
        int minValue = inputArray[0];
        for(int i = 1; i < inputArray.length; i++){
          if(inputArray[i] < minValue){
            minValue = inputArray[i];
          }
        }
        return minValue;
      }

    // Function to find the value to be
    // subtracted from array elements
    // to make all elements equal
    static int findtheValue(int[] arr, int N)
    {
        // Miniumum element in the array
        int mn = getMin(arr);
        int K = arr[0] - mn;

        // Traverse the array to find the gcd
        // of the differences between
        // all array elements and mn
        for (int i = 1; i < N; ++i) {
            K = gcd(K, arr[i] - mn);

        }

        return K;
    }

    // Driver Code
    public static void main(String args[])
    {
        int[] arr = { 5, 3, 3, 7 };
        int N = arr.length;
        System.out.println(findtheValue(arr, N));
    }
}

// This code is contributed by saurabh_jaiswal.
```

## 蟒蛇 3

```
# python program for the above approach
import math

# Function to find the value to be
# subtracted from array elements
# to make all elements equal

def findtheValue(arr, N):

    # Miniumum element in the array
    mn = min(arr)

    K = arr[0] - mn

    # Traverse the array to find the gcd
    # of the differences between
    # all array elements and mn
    for i in range(1, N):
        K = math.gcd(K, arr[i] - mn)

    return K

# Driver Code
if __name__ == "__main__":

    arr = [5, 3, 3, 7]
    N = len(arr)
    print(findtheValue(arr, N))

# This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;
using System.Linq;
class GFG {

    static int gcd(int a, int b)
    {
        if (b == 0)
            return a;
        return gcd(b, a % b);
    }

    // Function to find the value to be
    // subtracted from array elements
    // to make all elements equal
    static int findtheValue(int[] arr, int N)
    {
        // Miniumum element in the array
        int mn = arr.Min();
        int K = arr[0] - mn;

        // Traverse the array to find the gcd
        // of the differences between
        // all array elements and mn
        for (int i = 1; i < N; ++i) {
            K = gcd(K, arr[i] - mn);

        }

        return K;
    }

    // Driver Code
    public static void Main()
    {
        int[] arr = { 5, 3, 3, 7 };
        int N = arr.Length;
        Console.WriteLine(findtheValue(arr, N));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
// JavaScript program for the above approach
 let gcd = function(a, b) {
  if (!b) {
    return a;
  }

  return gcd(b, a % b);
}
// Function to find the value to be
// subtracted from array elements
// to make all elements equal
function findtheValue(arr, N)
{

    // Miniumum element in the array
    let mn = Math.min(...arr)

    let K = arr[0] - mn;

    // Traverse the array to find the gcd
    // of the differences between
    // all array elements and mn
    for (let i = 1; i < N; ++i) {
        K = gcd(K, arr[i] - mn);
    }

    return K;
}

// Driver Code
let arr = [ 5, 3, 3, 7 ]
let N = arr.length
document.write(findtheValue(arr, N))

// This code is contributed by rohitsingh07052.
</script>
```

**Output**

```
2
```

**时间复杂度:** O(Nlog(mn))
**辅助空间:** O(1)