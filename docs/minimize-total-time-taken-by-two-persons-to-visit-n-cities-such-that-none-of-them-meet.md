# 最大限度地减少两个人访问 N 个城市的总时间，使他们都不符合

> 原文:[https://www . geeksforgeeks . org/minimum-两个人访问 n 个城市的总时间-他们都不见面/](https://www.geeksforgeeks.org/minimize-total-time-taken-by-two-persons-to-visit-n-cities-such-that-none-of-them-meet/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，其中**arr【I】**是访问 **i <sup>th</sup>** 城市所需的时间，任务是找到两个人访问所有 **N** 城市所需的最小总时间，使得他们中没有人在任何城市相遇。

**示例:**

> **输入:** arr[] = {2，8，3}
> **输出:** 16
> **解释:**
> 按以下给定顺序访问城市所需时间最短:
> 第一人称 **:** 第二城市→第一城市→第三城市
> 第二人称:第一城市→第三城市→第二城市。
> 
> **输入:** arr[]={1，10，6，7，5 }
> T3】输出: 29

**方法:**给定的问题可以基于以下观察来解决:

*   假设**I<sup>th</sup>T3【城市】访问时间最长 **T** 一个人访问所有城市的总时间是所有阵元的[和，说**和**。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)**
*   如果 **1 <sup>st</sup>** 的人访问了**I<sup>th</sup>T7】的城市，那么在 **T** 的时间，如果可能的话，第二个人会在那个时间访问其他城市。**
*   如果 **T** 的值最多为**(sum–T)**，那么两人可以在 **sum** 时间内分别游览该地。
*   否则，**2<sup>2</sup>3**的人就要等着参观 **i <sup>th</sup> 城市**了。那么，所需的总时间将是 **2 * T** ，因为 **2 <sup>nd</sup>** 人只有在第一个人出来时才能参观 **i <sup>th</sup>** 城市。
*   因此，从以上观察，答案将是 **2 * T** 和**之和**的最大值。

因此，从以上观察，[求数组元素/a 的和>，求数组](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)中存在的 [最大元素，并在两倍的**最大元素**和**和**之间打印最大值。](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum time
// to visit all the cities such that
// both the person never meets
void minimumTime(int* arr, int n)
{
    // Initialize sum as 0
    int sum = 0;

    // Find the maximum element
    int T = *max_element(arr, arr + n);

    // Traverse the array
    for (int i = 0; i < n; i++) {

        // Increment sum by arr[i]
        sum += arr[i];
    }

    // Print maximum of 2*T and sum
    cout << max(2 * T, sum);
}

// Driver Code
int main()
{
    int arr[] = { 2, 8, 3 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    minimumTime(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Function to find the minimum time
// to visit all the cities such that
// both the person never meets
static void minimumTime(int[] arr, int n)
{

    // Initialize sum as 0
    int sum = 0;

    // Find the maximum element
    int T = Arrays.stream(arr).max().getAsInt();

    // Traverse the array
    for (int i = 0; i < n; i++)
    {

        // Increment sum by arr[i]
        sum += arr[i];
    }

    // Print maximum of 2*T and sum
    System.out.println(Math.max(2 * T, sum));
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 2, 8, 3 };
    int N = arr.length;

    // Function Call
    minimumTime(arr, N);
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the minimum time
# to visit all the cities such that
# both the person never meets
def minimumTime(arr, n):

  # Initialize sum as 0
    sum = 0

    # Find the maximum element
    T = max(arr)

    # Traverse the array
    for i in range(n):

        # Increment sum by arr[i]
        sum += arr[i]

    # Prmaximum of 2*T and sum
    print(max(2 * T, sum))

# Driver Code
if __name__ == '__main__':
    arr = [2, 8, 3]
    N = len(arr)

    # Function Call
    minimumTime(arr, N)

    # This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Linq;
class GFG
{

// Function to find the minimum time
// to visit all the cities such that
// both the person never meets
static void minimumTime(int[] arr, int n)
{

    // Initialize sum as 0
    int sum = 0;

    // Find the maximum element
    int T = arr.Min();

    // Traverse the array
    for (int i = 0; i < n; i++)
    {

        // Increment sum by arr[i]
        sum += arr[i];
    }

    // Print maximum of 2*T and sum
    Console.WriteLine(Math.Max(2 * T, sum));
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 2, 8, 3 };
    int N = arr.Length;

    // Function Call
    minimumTime(arr, N);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// javascript program for the above approach

    // Function to find the minimum time
    // to visit all the cities such that
    // both the person never meets
    function minimumTime(arr , n) {

        // Initialize sum as 0
        var sum = 0;

        // Find the maximum element
        var T =Math.max(...arr);

        // Traverse the array
        for (i = 0; i < n; i++) {

            // Increment sum by arr[i]
            sum += arr[i];
        }

        // Print maximum of 2*T and sum
        document.write(Math.max(2 * T, sum));
    }

    // Driver code
    var arr = [ 2, 8, 3 ];
    var N = arr.length;

    // Function Call
    minimumTime(arr, N);

// This code is contributed by todaysgaurav
</script>
```

**Output:** 

```
16
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)