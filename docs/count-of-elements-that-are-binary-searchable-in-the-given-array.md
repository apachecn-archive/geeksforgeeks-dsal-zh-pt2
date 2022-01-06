# 给定数组中可二进制搜索的元素计数

> 原文:[https://www . geesforgeks . org/给定数组中可二进制搜索的元素计数/](https://www.geeksforgeeks.org/count-of-elements-that-are-binary-searchable-in-the-given-array/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找出给定数组中[个可二进制搜索的](https://www.geeksforgeeks.org/variants-of-binary-search/)个整数的最大计数。

**示例:**

> **输入:** arr[] = {1，3，2}
> **输出:** 2
> **说明:** arr[0]，可以找到 arr[1]。
> 
> **输入:** arr[] = {3，2，1，10，23，22，21}
> **输出:** 3
> **解释:** arr[1]，arr[3]，arr[5]无论数组是否排序都可以使用二分搜索法找到。

**方法:**给定的问题可以通过[使用二分搜索法](https://www.geeksforgeeks.org/search-an-element-in-a-sorted-and-pivoted-array/)方法分别搜索数组中的每个元素并增加数组中存在的那些整数的计数来解决。按照以下步骤解决问题:

*   使变量**计数= 0** ，该变量将存储可二进制搜索的元素计数。
*   对于每个元素，在范围**【0，N)** 内执行[二分搜索法](https://www.geeksforgeeks.org/binary-search/)如下:
    *   将变量 **l** 初始化为 **0** ，将 **r** 初始化为 **N-1** ，对**arr【I】**执行二分搜索法运算。
    *   [每次迭代 while 循环](https://www.geeksforgeeks.org/c-c-while-loop-with-examples/)直到 **l** 小于等于 **r，**计算由 **(l + r)/2** 表示的中间值。
        *   如果 **arr[mid]** 等于 **arr[i]** ，那么将**计数**增加 **1** 。
        *   如果 **arr[mid]** 小于 **arr[i]，**则将 **l** 改为 **mid + 1** 。
        *   否则，将 **r** 更改为**mid-1**。
*   最终答案将存储在变量**计数**中。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the total count of
// elements that are binary searchable
int totalBinarySearchable(vector<int> arr)
{

    // Stores the count of element that
    // are binary searchable
    int count = 0;
    int N = arr.size();

    // For each element check if it can
    // be found by doing a binary search
    for (int i = 0; i < N; i++) {

        // Binary search range
        int l = 0, r = N - 1;

        // Do a binary Search
        while (l <= r) {
            int mid = (l + r) / 2;

            // Array element found
            if (arr[mid] == arr[i]) {
                count++;
                break;
            }
            if (arr[mid] < arr[i]) {
                l = mid + 1;
            }
            else {
                r = mid - 1;
            }
        }
    }

    // Return the total count
    return count;
}

// Driver Code
int main()
{
    vector<int> arr = { 3, 2, 1, 10,
                        23, 22, 21 };
    cout << totalBinarySearchable(arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
import java.io.*;

class GFG
{

    // Function to find the total count of
    // elements that are binary searchable
    static int totalBinarySearchable(int[] arr)
    {

        // Stores the count of element that
        // are binary searchable
        int count = 0;
        int N = arr.length;

        // For each element check if it can
        // be found by doing a binary search
        for (int i = 0; i < N; i++) {

            // Binary search range
            int l = 0, r = N - 1;

            // Do a binary Search
            while (l <= r) {
                int mid = (l + r) / 2;

                // Array element found
                if (arr[mid] == arr[i]) {
                    count++;
                    break;
                }
                if (arr[mid] < arr[i]) {
                    l = mid + 1;
                }
                else {
                    r = mid - 1;
                }
            }
        }

        // Return the total count
        return count;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = { 3, 2, 1, 10, 23, 22, 21 };

        System.out.println(totalBinarySearchable(arr));
    }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# python program for the above approach

# Function to find the total count of
# elements that are binary searchable
def totalBinarySearchable(arr):

        # Stores the count of element that
        # are binary searchable
    count = 0
    N = len(arr)

    # For each element check if it can
    # be found by doing a binary search
    for i in range(0, N):

                # Binary search range
        l = 0
        r = N - 1

        # Do a binary Search
        while (l <= r):
            mid = (l + r) // 2

            # Array element found
            if (arr[mid] == arr[i]):
                count += 1
                break

            if (arr[mid] < arr[i]):
                l = mid + 1

            else:
                r = mid - 1

        # Return the total count
    return count

# Driver Code
if __name__ == "__main__":

    arr = [3, 2, 1, 10,
           23, 22, 21]
    print(totalBinarySearchable(arr))

    # This code is contributed by rakeshsahni
```

## C#

```
// C# code for the above approach
using System;
public class GFG
{

    // Function to find the total count of
    // elements that are binary searchable
    static int totalBinarySearchable(int[] arr)
    {

        // Stores the count of element that
        // are binary searchable
        int count = 0;
        int N = arr.Length;

        // For each element check if it can
        // be found by doing a binary search
        for (int i = 0; i < N; i++) {

            // Binary search range
            int l = 0, r = N - 1;

            // Do a binary Search
            while (l <= r) {
                int mid = (l + r) / 2;

                // Array element found
                if (arr[mid] == arr[i]) {
                    count++;
                    break;
                }
                if (arr[mid] < arr[i]) {
                    l = mid + 1;
                }
                else {
                    r = mid - 1;
                }
            }
        }

        // Return the total count
        return count;
    }

    // Driver Code
    public static void Main(string[] args)
    {
        int[] arr = { 3, 2, 1, 10, 23, 22, 21 };

        Console.WriteLine(totalBinarySearchable(arr));
    }
}

// This code is contributed by rrrtnx.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the total count of
// elements that are binary searchable
function totalBinarySearchable(arr)
{

  // Stores the count of element that
  // are binary searchable
  let count = 0;
  let N = arr.length;

  // For each element check if it can
  // be found by doing a binary search
  for (let i = 0; i < N; i++)
  {

    // Binary search range
    let l = 0,
      r = N - 1;

    // Do a binary Search
    while (l <= r) {
      let mid = Math.floor((l + r) / 2);

      // Array element found
      if (arr[mid] == arr[i]) {
        count++;
        break;
      }
      if (arr[mid] < arr[i]) {
        l = mid + 1;
      } else {
        r = mid - 1;
      }
    }
  }

  // Return the total count
  return count;
}

// Driver Code
let arr = [3, 2, 1, 10, 23, 22, 21];
document.write(totalBinarySearchable(arr));

// This code is contributed by gfgking.
</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(N*log(N))*
***辅助空间:** O(1)*