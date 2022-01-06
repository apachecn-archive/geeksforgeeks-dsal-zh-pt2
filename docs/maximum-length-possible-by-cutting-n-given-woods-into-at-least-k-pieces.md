# 将 N 块给定的木材切割成至少 K 块的最大可能长度

> 原文:[https://www . geeksforgeeks . org/通过将给定的木材切割成至少 k 块的最大可能长度/](https://www.geeksforgeeks.org/maximum-length-possible-by-cutting-n-given-woods-into-at-least-k-pieces/)

给定一个大小为 **N** 的[阵](https://www.geeksforgeeks.org/array-data-structure/) **木【】**，代表 **N** 片木的长度，以及一个整数 **K** ，至少需要从给定的木片上切下相同长度的 **K** 片。任务是找到这些 **K** 木件可以获得的最大可能长度。

**示例:**

> **输入:**木材[] = {5，9，7}，K = 3
> **输出:** 5
> **说明:**
> 切 arr[0] = 5 = 5
> 切 arr[1] = 9 = 5 + 4
> 切 arr[2] = 7 = 5 + 2
> 因此，将木材切成 3 块所能得到的最大长度为 5。
> 
> **输入:**木材[] = {5，9，7}，K = 4
> **输出:** 4
> **解释:**
> 切 arr[0] = 5 = 4 + 1
> 切 arr[1] = 9 = 2 * 4 + 1
> 切 arr[2] = 7 = 4 + 3
> 因此，将木材切割成 4 块可以获得的最大长度为 4。

**方法:**这个问题可以用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)解决。按照以下步骤解决问题:

*   从数组 **木[]** 中找到[最大元素并存储在变量中，比如 **Max** 。](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)
*   **L** 的值必须在**【1，最大】**的范围内。因此，在**【1，最大】**范围内应用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)。
*   初始化两个变量，比如说**左= 1** 和**右=最大**来存储 **L** 值所在的范围。
*   检查是否可以将木材切割成 **K** 片，每片长度等于**(左+右)/ 2** 。如果发现是真的，那么更新**左=(左+右)/ 2** 。
*   否则，更新**右=(左+右)/ 2** 。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if it is possible to cut
// woods into K pieces of length len
bool isValid(int wood[], int N, int len, int K)
{

    // Stores count of pieces
    // having length equal to K
    int count = 0;

    // Traverse wood[] array
    for (int i = 0; i < N; i++) {

        // Update count
        count += wood[i] / len;
    }
    return count >= K;
}

// Function to find the maximum value of L
int findMaxLen(int wood[], int N, int K)
{

    // Stores minimum possible of L
    int left = 1;

    // Stores maximum possible value of L
    int right = *max_element(wood,
                             wood + N);

    // Apply binary search over
    // the range [left, right]
    while (left <= right) {

        // Stores mid value of
        // left and right
        int mid = left + (right - left) / 2;

        // If it is possible to cut woods
        // into K pieces having length
        // of each piece equal to mid
        if (isValid(wood, N, mid,
                    K)) {

            // Update left
            left = mid + 1;
        }
        else {

            // Update right
            right = mid - 1;
        }
    }
    return right;
}

// Driver Code
int main()
{
    int wood[] = { 5, 9, 7 };
    int N = sizeof(wood) / sizeof(wood[0]);
    int K = 4;
    cout << findMaxLen(wood, N, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to check if it is possible
// to cut woods into K pieces of
// length len
static boolean isValid(int wood[], int N,
                       int len, int K)
{

    // Stores count of pieces
    // having length equal to K
    int count = 0;

    // Traverse wood[] array
    for(int i = 0; i < N; i++)
    {

        // Update count
        count += wood[i] / len;
    }
    return count >= K;
}

// Function to find the maximum value of L
static int findMaxLen(int wood[], int N,
                      int K)
{

    // Stores minimum possible of L
    int left = 1;

    // Stores maximum possible value of L
    int right = Arrays.stream(wood).max().getAsInt();

    // Apply binary search over
    // the range [left, right]
    while (left <= right)
    {

        // Stores mid value of
        // left and right
        int mid = left + (right - left) / 2;

        // If it is possible to cut woods
        // into K pieces having length
        // of each piece equal to mid
        if (isValid(wood, N, mid, K))
        {

            // Update left
            left = mid + 1;
        }
        else
        {

            // Update right
            right = mid - 1;
        }
    }
    return right;
}

// Driver Code
public static void main(String[] args)
{
    int wood[] = { 5, 9, 7 };
    int N = wood.length;
    int K = 4;

    System.out.print(findMaxLen(wood, N, K));
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to check if it is possible to
# cut woods into K pieces of length len
def isValid(wood, N, len, K):

    # Stores count of pieces
    # having length equal to K
    count = 0

    # Traverse wood[] array
    for i in range(N):

        # Update count
        count += wood[i] // len

    return (count >= K)

# Function to find the maximum value of L
def findMaxLen(wood, N, K):

    # Stores minimum possible of L
    left = 1

    # Stores maximum possible value of L
    right = max(wood)

    # Apply binary search over
    # the range [left, right]
    while (left <= right):

        # Stores mid value of
        # left and right
        mid = left + (right - left) // 2

        # If it is possible to cut woods
        # into K pieces having length
        # of each piece equal to mid
        if (isValid(wood, N, mid, K)):

            # Update left
            left = mid + 1
        else:

            # Update right
            right = mid - 1

    return right

# Driver Code
if __name__ == '__main__':

    wood = [ 5, 9, 7 ]
    N = len(wood)
    K = 4

    print(findMaxLen(wood, N, K))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Linq;
class GFG{

// Function to check if it is possible
// to cut woods into K pieces of
// length len
static bool isValid(int []wood, int N,
                    int len, int K)
{   
  // Stores count of pieces
  // having length equal to K
  int count = 0;

  // Traverse wood[] array
  for(int i = 0; i < N; i++)
  {
    // Update count
    count += wood[i] / len;
  }
  return count >= K;
}

// Function to find the maximum
// value of L
static int findMaxLen(int []wood,
                      int N, int K)
{   
  // Stores minimum possible
  // of L
  int left = 1;

  // Stores maximum possible
  // value of L
  int right = wood.Max();

  // Apply binary search over
  // the range [left, right]
  while (left <= right)
  {
    // Stores mid value of
    // left and right
    int mid = left +
              (right - left) / 2;

    // If it is possible to cut woods
    // into K pieces having length
    // of each piece equal to mid
    if (isValid(wood, N,
                mid, K))
    {
      // Update left
      left = mid + 1;
    }
    else
    {
      // Update right
      right = mid - 1;
    }
  }
  return right;
}

// Driver Code
public static void Main(String[] args)
{
  int []wood = {5, 9, 7};
  int N = wood.Length;
  int K = 4;
  Console.Write(findMaxLen(wood,
                           N, K));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

    // Function to check if it is possible
    // to cut woods into K pieces of
    // length len
    function isValid(wood , N , len , K) {

        // Stores count of pieces
        // having length equal to K
        var count = 0;

        // Traverse wood array
        for (i = 0; i < N; i++) {

            // Update count
            count += parseInt(wood[i] / len);
        }
        return count >= K;
    }

    // Function to find the maximum value of L
    function findMaxLen(wood , N , K) {

        // Stores minimum possible of L
        var left = 1;

        // Stores maximum possible value of L
        var right = Math.max.apply(Math,wood);

        // Apply binary search over
        // the range [left, right]
        while (left <= right) {

            // Stores mid value of
            // left and right
            var mid = left + (right - left) / 2;

            // If it is possible to cut woods
            // into K pieces having length
            // of each piece equal to mid
            if (isValid(wood, N, mid, K)) {

                // Update left
                left = mid + 1;
            } else {

                // Update right
                right = mid - 1;
            }
        }
        return right;
    }

    // Driver Code

        var wood = [ 5, 9, 7 ];
        var N = wood.length;
        var K = 4;

        document.write(findMaxLen(wood, N, K));

// This code is contributed by todaysgaurav

</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(N * Log <sub>2</sub> M)，其中 M 为给定数组的最大元素*
***辅助空间:** O(1)*