# 计数由具有精确的 K 组位的元素组成的子阵列

> 原文:[https://www . geeksforgeeks . org/count-subarrays-由元素组成-具有精确的 k-set-bit/](https://www.geeksforgeeks.org/count-subarrays-made-up-of-elements-having-exactly-k-set-bits/)

给定一个由 **N** 个整数和一个整数 **K** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是计算[个子数组](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)的数量，这些子数组可能由具有精确 **K** [组位](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)的元素组成。

**示例:**

> **输入:** arr[] = {4，2，1，5，6}，K = 2
> **输出:** 3
> **解释:**由正好具有 2 个设置位的元素组成的子阵列是{5}、{6}和{5，6}。
> 
> **输入:** arr[] = {4，2，1，5，6}，K = 1
> T3】输出: 6

**天真方法:**解决问题最简单的方法是[生成给定数组](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)的所有可能的子数组，并对那些由恰好具有 **K** 设置位的元素组成的子数组进行计数。最后，打印此类子阵列的计数。

***时间复杂度:** O(N <sup>3</sup> log(M))，其中 **M** 是数组* *中最大的* [*元素。*
***辅助空间:** O(1)*](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)

**高效方法:**思路是用 **K** 集合位保持对连续数组元素的跟踪，并找到那些连续元素集合的子数组的计数。按照以下步骤解决问题:

*   初始化一个变量，将 **res** 设为 **0** ，以存储由具有 **K** [设置位](https://www.geeksforgeeks.org/count-set-bits-integer-using-lookup-table/)的元素组成的子阵列的总数。初始化一个变量，比如说**计数**为 **0** ，以存储具有 **K** 设置位的一组连续元素的计数。
*   [遍历给定数组 **arr[]**](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) ，并执行以下步骤:
    *   如果当前元素**arr【I】**有 **K 设置位**，那么将**计数**增加 **1** 。
    *   否则，将 **res** 的值增加**(计数*(计数–1))/2**作为由先前连续元素形成的子阵列的总数，并将**计数**设置为 **0** 。
*   完成上述步骤后，打印 **res** 的值作为子阵列的合成计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
using namespace std;

// Function to count the number
// of set bits in an integer N
int countSet(int N)
{

  // Stores the count of set bits
  int ans = 0;

  // While N is non-zero
  while(N)
  {

    // If the LSB is 1, then
    // increment ans by 1
    ans += N & 1;
    N >>= 1;
  }

  // Return the total set bits
  return ans;
}

// Function to count the number of
// subarrays having made up of
// elements having K set bits
int countSub(int *arr,int k)
{

  // Stores the total count of
  // resultant subarrays
  int ans = 0;
  int setK = 0;

  // Traverse the given array
  for(int i = 0; i < 5; i++)
  {

    // If the current element
    // has K set bits
    if(countSet(arr[i]) == k)
      setK += 1;

    // Otherwise
    else
      setK = 0;

    // Increment count of subarrays
    ans += setK;
  }

  // Return total count of subarrays
  return ans;
}

// Driver Code
int main()
{
  int arr[] = {4, 2, 1, 5, 6};
  int K = 2;

  // Function Call
  cout<<(countSub(arr, K));
  return 0;
}

// This code is contributed by rohitsingh07052.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to count the number
// of set bits in an integer N
static int countSet(int N)
{

    // Stores the count of set bits
    int ans = 0;

    // While N is non-zero
    while(N > 0)
    {

        // If the LSB is 1, then
        // increment ans by 1
        ans += N & 1;
        N >>= 1;
    }

    // Return the total set bits
    return ans;
}

// Function to count the number of
// subarrays having made up of
// elements having K set bits
static int countSub(int []arr,int k)
{

    // Stores the total count of
    // resultant subarrays
    int ans = 0;
    int setK = 0;

    // Traverse the given array
    for(int i = 0; i < 5; i++)
    {

        // If the current element
        // has K set bits
        if (countSet(arr[i]) == k)
            setK += 1;

        // Otherwise
        else
            setK = 0;

        // Increment count of subarrays
        ans += setK;
    }

    // Return total count of subarrays
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = {4, 2, 1, 5, 6};
    int K = 2;

    // Function Call
    System.out.print(countSub(arr, K));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the number
# of set bits in an integer N
def countSet(N):

    # Stores the count of set bits
    ans = 0

    # While N is non-zero
    while N:

        # If the LSB is 1, then
        # increment ans by 1
        ans += N & 1
        N >>= 1

    # Return the total set bits
    return ans

# Function to count the number of
# subarrays having made up of
# elements having K set bits
def countSub(arr, k):

    # Stores the total count of
    # resultant subarrays
    ans = 0
    setK = 0

    # Traverse the given array
    for i in arr:

        # If the current element
        # has K set bits
        if countSet(i) == k:
            setK += 1

        # Otherwise
        else:
            setK = 0

        # Increment count of subarrays
        ans += setK

    # Return total count of subarrays
    return ans

# Driver Code
arr = [4, 2, 1, 5, 6]
K = 2

# Function Call
print(countSub(arr, K))
```

## C#

```
// C# program for the above approach
using System;

class GFG {

  // Function to count the number
  // of set bits in an integer N
  static int countSet(int N)
  {

    // Stores the count of set bits
    int ans = 0;

    // While N is non-zero
    while (N > 0)
    {

      // If the LSB is 1, then
      // increment ans by 1
      ans += N & 1;
      N >>= 1;
    }

    // Return the total set bits
    return ans;
  }

  // Function to count the number of
  // subarrays having made up of
  // elements having K set bits
  static int countSub(int[] arr, int k)
  {

    // Stores the total count of
    // resultant subarrays
    int ans = 0;
    int setK = 0;

    // Traverse the given array
    for (int i = 0; i < 5; i++) {

      // If the current element
      // has K set bits
      if (countSet(arr[i]) == k)
        setK += 1;

      // Otherwise
      else
        setK = 0;

      // Increment count of subarrays
      ans += setK;
    }

    // Return total count of subarrays
    return ans;
  }

  // Driver Code
  public static void Main(string[] args)
  {
    int[] arr = { 4, 2, 1, 5, 6 };
    int K = 2;

    // Function Call
    Console.WriteLine(countSub(arr, K));
  }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to count the number
// of set bits in an integer N
function countSet(N)
{

// Stores the count of set bits
let ans = 0;

// While N is non-zero
while(N)
{

    // If the LSB is 1, then
    // increment ans by 1
    ans += N & 1;
    N >>= 1;
}

// Return the total set bits
return ans;
}

// Function to count the number of
// subarrays having made up of
// elements having K set bits
function countSub(arr,k)
{

// Stores the total count of
// resultant subarrays
let ans = 0;
let setK = 0;

// Traverse the given array
for(let i = 0; i < 5; i++)
{

    // If the current element
    // has K set bits
    if(countSet(arr[i]) == k)
    setK += 1;

    // Otherwise
    else
    setK = 0;

    // Increment count of subarrays
    ans += setK;
}

// Return total count of subarrays
return ans;
}

// Driver Code

let arr = [4, 2, 1, 5, 6];
let K = 2;

// Function Call
document.write((countSub(arr, K)));

// This code is contributed by Mayank Tyagi
</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(N*log(M))，其中 M 为阵中* [*最大元素*](https://www.geeksforgeeks.org/c-program-find-largest-element-array/) *。*
***辅助空间:** O(1)*