# K 大小的任何子阵列中出现的最大偶数

> 原文:[https://www . geesforgeks . org/最大偶数-出现在任何大小的子阵列中-k/](https://www.geeksforgeeks.org/maximum-even-numbers-present-in-any-subarray-of-size-k/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**和一个整数 **K** ，任务是找出任何大小为 **K** 的子数组中出现的偶数的最大数量。

**示例:**

> **输入:** arr[] = {2，3，5，4，7，6}，K = 3
> **输出:** 2
> **说明:**
> 偶数计数最大的 K(=3)大小的子阵为{ arr[3]，arr[4]，arr[5] }
> 因此，需要的输出为 2
> 
> **输入** : arr[] = {4，3，2，6}，K = 2
> **输出:** 2

**天真法:**解决这个问题最简单的方法就是[生成所有可能大小的子阵**K**T5】并统计子阵中的偶数。最后，打印获得的最大计数。](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum count of
// even numbers from all the subarrays of
// size K
int maxEvenIntegers(int arr[], int N, int M)
{

    // Stores the maximum count of even numbers
    // from all the subarrays of size K
    int ans = 0;

    // Generate all subarrays of size K
    for (int i = 0; i <= N - M; i++) {

        // Store count of even numbers
        // in current subarray of size K
        int cnt = 0;

        // Traverse the current subarray
        for (int j = 0; j < M; j++) {

            // If current element
            // is an even number
            if (arr[i + j] % 2 == 0)
                cnt++;
        }

        // Update the answer
        ans = max(ans, cnt);
    }

    // Return answer
    return ans;
}

// Driver Code
int main()
{

    int arr[] = { 2, 3, 5, 4, 7, 6 };
    int K = 3;

    // Size of the input array
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << maxEvenIntegers(arr, N, K) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG
{

// Function to find the maximum count of
// even numbers from all the subarrays of
// size K
static int maxEvenIntegers(int arr[], int N, int M)
{

    // Stores the maximum count of even numbers
    // from all the subarrays of size K
    int ans = 0;

    // Generate all subarrays of size K
    for (int i = 0; i <= N - M; i++)
    {

        // Store count of even numbers
        // in current subarray of size K
        int cnt = 0;

        // Traverse the current subarray
        for (int j = 0; j < M; j++)
        {

            // If current element
            // is an even number
            if (arr[i + j] % 2 == 0)
                cnt++;
        }

        // Update the answer
        ans = Math.max(ans, cnt);
    }

    // Return answer
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 2, 3, 5, 4, 7, 6 };
    int K = 3;

    // Size of the input array
    int N = arr.length;
    System.out.print(maxEvenIntegers(arr, N, K) +"\n");

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the maximum count of
# even numbers from all the subarrays of
# size K
def maxEvenIntegers(arr, N, K):

    # Stores the maximum count of even numbers
    # from all the subarrays of size K
    ans = 0
    # Generate all subarrays of size K
    for i in range(N-K+1):
        # Store count of even numbers
        # in current subarray of size K
        cnt = 0

        # Traverse the current subarray
        for j in range(0, K):
            if arr[i+j] % 2 == 0:
                cnt += 1
        # Update the answer
        ans = max(cnt, ans)
    # Return answer
    return ans

# Driver Code
if __name__ == '__main__':
    arr = [2, 3, 5, 4, 7, 6]
    K = 3
    # Size of the input array
    N = len(arr)
    print(maxEvenIntegers(arr, N, K))

# This code is contributed by MuskanKalra1
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG
{

    // Function to find the maximum count of
    // even numbers from all the subarrays of
    // size K
    static int maxEvenIntegers(int []arr, int N, int M)
    {

        // Stores the maximum count of even numbers
        // from all the subarrays of size K
        int ans = 0;

        // Generate all subarrays of size K
        for (int i = 0; i <= N - M; i++)
        {

            // Store count of even numbers
            // in current subarray of size K
            int cnt = 0;

            // Traverse the current subarray
            for (int j = 0; j < M; j++)
            {

                // If current element
                // is an even number
                if (arr[i + j] % 2 == 0)
                    cnt++;
            }

            // Update the answer
            ans = Math.Max(ans, cnt);
        }

        // Return answer
        return ans;
    }

    // Driver Code
    public static void Main(string[] args)
    {
        int []arr = { 2, 3, 5, 4, 7, 6 };
        int K = 3;

        // Size of the input array
        int N = arr.Length;
        Console.WriteLine(maxEvenIntegers(arr, N, K));
    }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>
// Java script program to implement
// the above approach

// Function to find the maximum count of
// even numbers from all the subarrays of
// size K
function maxEvenIntegers(arr,  N,  M)
{

    // Stores the maximum count of even numbers
    // from all the subarrays of size K
    let ans = 0;

    // Generate all subarrays of size K
    for (let i = 0; i <= N - M; i++)
    {

        // Store count of even numbers
        // in current subarray of size K
        let cnt = 0;

        // Traverse the current subarray
        for (let j = 0; j < M; j++)
        {

            // If current element
            // is an even number
            if (arr[i + j] % 2 == 0)
                cnt++;
        }

        // Update the answer
        ans = Math.max(ans, cnt);
    }

    // Return answer
    return ans;
}

// Driver Code

    let arr = [ 2, 3, 5, 4, 7, 6 ];
    let K = 3;

    // Size of the input array
    let N = arr.length;
    document.write(maxEvenIntegers(arr, N, K) +"<br>");

//contributed by bobby

</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N * K)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以使用[滑动窗口技术](https://www.geeksforgeeks.org/window-sliding-technique/)进行优化。按照以下步骤解决问题:

*   初始化一个变量，比如 **cntMaxEven** ，将偶数的最大计数存储在大小为 **K** 的[子阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)中。
*   计算子阵列 **{ arr[0]，…arr[K–1]}**中偶数的计数，并存储到 **cntMaxEven** 中。
*   通过迭代范围**【K，N-1】**遍历剩余的子阵列大小 **K** 。对于每次 **i <sup>th</sup>** 迭代，移除子阵列的第一个元素，并将阵列的当前 **i <sup>th</sup>** 元素插入到当前子阵列中。
*   对当前子阵列中的偶数进行计数，并将 **cntMaxEven** 更新为当前子阵列和 **cntMaxEven** 中偶数的最大计数。
*   最后打印 **cntMaxEven** 的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum count of
// even numbers from all the subarrays of
// size K
int maxEvenIntegers(int arr[], int N, int M)
{

    // Stores the count of even numbers
    // in a subarray of size K
    int curr = 0;

    // Calculate the count of even numbers
    // in the current subarray
    for (int i = 0; i < M; i++) {

        // If current element is
        // an even number
        if (arr[i] % 2 == 0)
            curr++;
    }

    // Stores the maximum count of even numbers
    // from all the subarrays of size K
    int ans = curr;

    // Traverse remaining subarrays of size K
    // using sliding window technique
    for (int i = M; i < N; i++) {

        // If the first element of
        // the subarray is even
        if (arr[i - M] % 2 == 0) {

            // Update curr
            curr--;
        }

        // If i-th element is even increment
        // the count
        if (arr[i] % 2 == 0)
            curr++;

        // Update the answer
        ans = max(ans, curr);
    }

    // Return answer
    return ans;
}

// Driver Code
int main()
{
    int arr[] = { 2, 3, 5, 4, 7, 6 };
    int M = 3;

    // Size of the input array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call
    cout << maxEvenIntegers(arr, N, M) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG
{

  // Function to find the maximum count of
  // even numbers from all the subarrays of
  // size K
  static int maxEvenIntegers(int arr[], int N, int M)
  {

    // Stores the count of even numbers
    // in a subarray of size K
    int curr = 0;

    // Calculate the count of even numbers
    // in the current subarray
    for (int i = 0; i < M; i++)
    {

      // If current element is
      // an even number
      if (arr[i] % 2 == 0)
        curr++;
    }

    // Stores the maximum count of even numbers
    // from all the subarrays of size K
    int ans = curr;

    // Traverse remaining subarrays of size K
    // using sliding window technique
    for (int i = M; i < N; i++)
    {

      // If the first element of
      // the subarray is even
      if (arr[i - M] % 2 == 0)
      {

        // Update curr
        curr--;
      }

      // If i-th element is even increment
      // the count
      if (arr[i] % 2 == 0)
        curr++;

      // Update the answer
      ans = Math.max(ans, curr);
    }

    // Return answer
    return ans;
  }

  // Driver Code
  public static void main(String[] args)
  {
    int arr[] = { 2, 3, 5, 4, 7, 6 };
    int M = 3;

    // Size of the input array
    int N = arr.length;

    // Function call
    System.out.print(maxEvenIntegers(arr, N, M) +"\n");

  }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the maximum count of
# even numbers from all the subarrays of
# size M
def maxEvenIntegers(arr, N, M):

    # Stores the count of even numbers
    # in a subarray of size M
    curr = 0

    # Calculate the count of even numbers
    # in the current subarray
    for i in range(0, M):

        # If current element is
        # an even number
        if(arr[i] % 2 == 0):
            curr += 1

    # Stores the maximum count of even numbers
    # from all the subarrays of size M
    ans = curr

    # Traverse remaining subarrays of size M
    # using sliding window technique
    for i in range(M, N):

        # If the first element of
        # the subarray is even
        if(arr[i - M] % 2 == 0):

            # update curr
            curr -= 1

        # If i-th element is even increment
        # the count
        if(arr[i] % 2 == 0):
            curr += 1

            # update the answer
            ans = max(curr, ans)

    # Return answer
    return ans

# Driver Code
if __name__ == '__main__':
    arr = [2, 3, 5, 4, 7, 6]
    M = 3

    # Size of the input array
    N = len(arr)

    # Function call
    print(maxEvenIntegers(arr, N, M))

# This code is contributed by MuskanKalra1
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG
{

  // Function to find the maximum count of
  // even numbers from all the subarrays of
  // size K
  static int maxEvenints(int []arr, int N, int M)
  {

    // Stores the count of even numbers
    // in a subarray of size K
    int curr = 0;

    // Calculate the count of even numbers
    // in the current subarray
    for (int i = 0; i < M; i++)
    {

      // If current element is
      // an even number
      if (arr[i] % 2 == 0)
        curr++;
    }

    // Stores the maximum count of even numbers
    // from all the subarrays of size K
    int ans = curr;

    // Traverse remaining subarrays of size K
    // using sliding window technique
    for (int i = M; i < N; i++)
    {

      // If the first element of
      // the subarray is even
      if (arr[i - M] % 2 == 0)
      {

        // Update curr
        curr--;
      }

      // If i-th element is even increment
      // the count
      if (arr[i] % 2 == 0)
        curr++;

      // Update the answer
      ans = Math.Max(ans, curr);
    }

    // Return answer
    return ans;
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int []arr = { 2, 3, 5, 4, 7, 6 };
    int M = 3;

    // Size of the input array
    int N = arr.Length;

    // Function call
    Console.Write(maxEvenints(arr, N, M) +"\n");
  }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program to implement
// the above approach

  // Function to find the maximum count of
  // even numbers from all the subarrays of
  // size K
  function maxEvenLetegers(arr, N, M)
  {

    // Stores the count of even numbers
    // in a subarray of size K
    let curr = 0;

    // Calculate the count of even numbers
    // in the current subarray
    for (let i = 0; i < M; i++)
    {

      // If current element is
      // an even number
      if (arr[i] % 2 == 0)
        curr++;
    }

    // Stores the maximum count of even numbers
    // from all the subarrays of size K
    let ans = curr;

    // Traverse remaining subarrays of size K
    // using sliding window technique
    for (let i = M; i < N; i++)
    {

      // If the first element of
      // the subarray is even
      if (arr[i - M] % 2 == 0)
      {

        // Update curr
        curr--;
      }

      // If i-th element is even increment
      // the count
      if (arr[i] % 2 == 0)
        curr++;

      // Update the answer
      ans = Math.max(ans, curr);
    }

    // Return answer
    return ans;
  }

// Driver Code

    let arr = [ 2, 3, 5, 4, 7, 6 ];
    let M = 3;

    // Size of the input array
    let N = arr.length;

    // Function call
    document.write(maxEvenLetegers(arr, N, M) +"\n");

     // This code is contributed by souravghosh0416.
</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N)*

***辅助空间:*** O(1)