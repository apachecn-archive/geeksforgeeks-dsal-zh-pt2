# 通过将给定数组划分为给定大小获得的 K 个数组的最大值和最小值之和最大化

> 原文:[https://www . geeksforgeeks . org/通过将给定数组划分为给定大小获得的 k 个数组的最大值和最小值之和最大化/](https://www.geeksforgeeks.org/maximize-sum-of-max-and-min-of-each-of-k-arrays-obtained-by-dividing-given-array-into-given-sizes/)

给定两个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)，**arr【】**的 **N** 大小和**div【】**的 **K** 大小。将 **arr[]** 分成 **K** 个不同的数组，每个**div【I】**大小。任务是求**最大化**后的**总和**每个分阵的**最大值**和**最小值**。

**示例:**

> **输入:** arr[] = {3，1，7，4}，div[] = {1，3}，N = 4，K = 2
> **输出:** 19
> **说明:**分阵方式如下:
> 
> *   {7}，最大值和最小值之和= (7 + 7) = 14
> *   {1，3，4}，最大值和最小值之和= (4 + 1) = 5
> 
> 总和= 14 + 5 = 19。
> 
> **输入:** arr[] = {10，12，10，12，10，12}、div[] = {3，3}、N = 6，K = 2
> **输出:** 44

**方法:**按照以下步骤解决问题:

1.  取一个变量 **count1** 来计算**div【】**中的 **1s** 的个数。
2.  [排序](https://www.geeksforgeeks.org/sort-c-stl)两个数组，**arr【】**按照**降序**排序，**div【】**按照**升序**排序。
3.  取一个变量 say， **ans** 存储答案，另一个变量 say **t** 表示在**div【】**中从哪个索引开始迭代。
4.  迭代该数组直到 **K** ，在每次迭代中**将**元素添加到 ans 中，**再次将**元素**添加到**ans 中，而 **count1** 大于 **0** ，因为**大小为 1** 的数组具有与**最大值**和**最小值**相同的**元素。**
5.  再次迭代一个从数组的 **Kth** 索引到**结束**的循环。**在**和**中添加**元素，更新索引。
6.  返回**和**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the total sum after
// maximizing the sum of maximum and
// minimum of each divided array
int maximizeSum(int arr[], int divi[], int N, int K)
{
    // Variable to count 1s in divi[]
    int count1 = 0;
    for (int i = 0; i < K; i++) {
        if (divi[i] == 1) {
            count1++;
        }
    }

    // Sort arr[] in desecending order
    sort(arr, arr + N, greater<int>());

    // Sort divi[] in ascending order
    sort(divi, divi + K);

    // Temporary variable to store
    // the count of 1s in the divi[]

    int t = count1;
    // Variable to store answer
    int ans = 0;

    // Iterate over the array till K
    for (int i = 0; i < K; i++) {
        // Add the current element to ans
        ans += arr[i];

        // If count1 is greater than 0,
        // decrement it by 1 and update the
        // ans by again adding the same element
        if (count1 > 0) {
            count1--;
            ans += arr[i];
        }
    }

    // Traverse the array from Kth index
    // to the end
    for (int i = K; i < N; i++) {
        // Update the index
        i += divi[t] - 2;

        // Add the value at that index to ans
        ans += arr[i];
        t++;
    }
    // Return ans
    return ans;
}

// Driver Code
int main()
{
    int arr[] = { 3, 1, 7, 4 };
    int divi[] = { 1, 3 };

    int N = sizeof(arr) / sizeof(arr[0]);
    int K = sizeof(divi) / sizeof(divi[0]);

    cout << maximizeSum(arr, divi, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
import java.util.Arrays;
import java.util.Collections;

class GFG
{

    // Function to find the total sum after
    // maximizing the sum of maximum and
    // minimum of each divided array
    static int maximizeSum(int arr[], int divi[], int N,
                           int K)
    {

        // Variable to count 1s in divi[]
        int count1 = 0;
        for (int i = 0; i < K; i++) {
            if (divi[i] == 1) {
                count1++;
            }
        }

        // Sort arr[] in desecending order
        Arrays.sort(arr);
        reverse(arr);

        // Sort divi[] in ascending order
        Arrays.sort(divi);

        // Temporary variable to store
        // the count of 1s in the divi[]

        int t = count1;
        // Variable to store answer
        int ans = 0;

        // Iterate over the array till K
        for (int i = 0; i < K; i++) {
            // Add the current element to ans
            ans += arr[i];

            // If count1 is greater than 0,
            // decrement it by 1 and update the
            // ans by again adding the same element
            if (count1 > 0) {
                count1--;
                ans += arr[i];
            }
        }

        // Traverse the array from Kth index
        // to the end
        for (int i = K; i < N; i++) {
            // Update the index
            i += divi[t] - 2;

            // Add the value at that index to ans
            ans += arr[i];
            t++;
        }
        // Return ans
        return ans;
    }
    public static void reverse(int[] array)
    {

        // Length of the array
        int n = array.length;

        // Swaping the first half elements with last half
        // elements
        for (int i = 0; i < n / 2; i++) {

            // Storing the first half elements temporarily
            int temp = array[i];

            // Assigning the first half to the last half
            array[i] = array[n - i - 1];

            // Assigning the last half to the first half
            array[n - i - 1] = temp;
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 3, 1, 7, 4 };
        int divi[] = { 1, 3 };

        int N = arr.length;
        int K = divi.length;

        System.out.println(maximizeSum(arr, divi, N, K));
    }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the total sum after
# maximizing the sum of maximum and
# minimum of each divided array
def maximizeSum(arr, divi, N, K):

    # Variable to count 1s in divi[]
    count1 = 0
    for i in range(K):
        if (divi[i] == 1):
            count1 += 1

    # Sort arr[] in desecending order
    arr.sort()
    arr.reverse()

    # Sort divi[] in ascending order
    divi.sort()

    # Temporary variable to store
    # the count of 1s in the divi[]

    t = count1
    # Variable to store answer
    ans = 0

    # Iterate over the array till K
    for i in range(K):
        # Add the current element to ans
        ans += arr[i]

        # If count1 is greater than 0,
        # decrement it by 1 and update the
        # ans by again adding the same element
        if (count1 > 0):
            count1 -= 1
            ans += arr[i]

    # Traverse the array from Kth index
    # to the end
    i = K
    while(i < N):
        # Update the index
        i += divi[t] - 2

        # Add the value at that index to ans
        ans += arr[i]
        t += 1
        i += 1

    # Return ans
    return ans

# Driver Code
arr = [3, 1, 7, 4]
divi = [1, 3]

N = len(arr)
K = len(divi)

print(maximizeSum(arr, divi, N, K))

# This code is contributed by gfgking
```

## C#

```
// C# code for the above approach

using System;

public class GFG
{

    // Function to find the total sum after
    // maximizing the sum of maximum and
    // minimum of each divided array
    static int maximizeSum(int []arr, int []divi, int N,
                           int K)
    {

        // Variable to count 1s in divi[]
        int count1 = 0;
        for (int i = 0; i < K; i++) {
            if (divi[i] == 1) {
                count1++;
            }
        }

        // Sort arr[] in desecending order
        Array.Sort(arr);
        reverse(arr);

        // Sort divi[] in ascending order
        Array.Sort(divi);

        // Temporary variable to store
        // the count of 1s in the divi[]

        int t = count1;
        // Variable to store answer
        int ans = 0;

        // Iterate over the array till K
        for (int i = 0; i < K; i++) {
            // Add the current element to ans
            ans += arr[i];

            // If count1 is greater than 0,
            // decrement it by 1 and update the
            // ans by again adding the same element
            if (count1 > 0) {
                count1--;
                ans += arr[i];
            }
        }

        // Traverse the array from Kth index
        // to the end
        for (int i = K; i < N; i++) {
            // Update the index
            i += divi[t] - 2;

            // Add the value at that index to ans
            ans += arr[i];
            t++;
        }
        // Return ans
        return ans;
    }
    public static void reverse(int[] array)
    {

        // Length of the array
        int n = array.Length;

        // Swaping the first half elements with last half
        // elements
        for (int i = 0; i < n / 2; i++) {

            // Storing the first half elements temporarily
            int temp = array[i];

            // Assigning the first half to the last half
            array[i] = array[n - i - 1];

            // Assigning the last half to the first half
            array[n - i - 1] = temp;
        }
    }

    // Driver Code
    public static void Main(string[] args)
    {
        int []arr = { 3, 1, 7, 4 };
        int []divi = { 1, 3 };

        int N = arr.Length;
        int K = divi.Length;

        Console.WriteLine(maximizeSum(arr, divi, N, K));
    }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>
    // JavaScript program for the above approach

    // Function to find the total sum after
    // maximizing the sum of maximum and
    // minimum of each divided array
    const maximizeSum = (arr, divi, N, K) => {
        // Variable to count 1s in divi[]
        let count1 = 0;
        for (let i = 0; i < K; i++) {
            if (divi[i] == 1) {
                count1++;
            }
        }

        // Sort arr[] in desecending order
        arr.sort();
        arr.reverse();

        // Sort divi[] in ascending order
        divi.sort();

        // Temporary variable to store
        // the count of 1s in the divi[]

        let t = count1;
        // Variable to store answer
        let ans = 0;

        // Iterate over the array till K
        for (let i = 0; i < K; i++) {
            // Add the current element to ans
            ans += arr[i];

            // If count1 is greater than 0,
            // decrement it by 1 and update the
            // ans by again adding the same element
            if (count1 > 0) {
                count1--;
                ans += arr[i];
            }
        }

        // Traverse the array from Kth index
        // to the end
        for (let i = K; i < N; i++) {
            // Update the index
            i += divi[t] - 2;

            // Add the value at that index to ans
            ans += arr[i];
            t++;
        }
        // Return ans
        return ans;
    }

    // Driver Code
    let arr = [3, 1, 7, 4];
    let divi = [1, 3];

    let N = arr.length
    let K = divi.length

    document.write(maximizeSum(arr, divi, N, K));

    // This code is contributed by rakeshsahni

</script>
```

**Output**

```
19
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)