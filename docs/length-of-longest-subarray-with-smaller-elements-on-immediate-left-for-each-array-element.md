# 最长子阵列的长度，每个阵列元素的左边有较小的元素

> 原文:[https://www . geeksforgeeks . org/每个数组元素的紧邻左侧具有较小元素的最长子数组长度/](https://www.geeksforgeeks.org/length-of-longest-subarray-with-smaller-elements-on-immediate-left-for-each-array-element/)

给定一个长度为 **N** 的数组 **arr[]** ，任务是为给定数组中的每个元素找到最长子数组的长度，并且在最左边有更小的元素。

**示例:**

> **输入:** arr[] = { 2，1，7，6，7 }
> **输出:** 0 0 2 0 1
> **解释:**
> 索引 0 (2):没有子字符串出现在包含所有较小元素的紧邻左侧。因此，长度=0
> 索引 1 (1):没有子串出现在包含所有较小元素的最左边。因此，长度=0
> 索引 2 (7):子串{2，1}出现在最左边，包含所有较小的元素。因此，长度=2
> 索引 3 (6):没有子串出现在包含所有较小元素的最左边。因此，长度=0
> 索引 4 (2):子字符串{6}出现在最左边，包含所有较小的元素。所以，长度=1
> 
> **输入:** arr[] = { 4，5，7，6，10 }
> **输出:** 0 1 2 0 4

**方法:**对于每个元素，向左移动，直到左边的元素更大或者数组结束，以找到最长的子数组的长度，在紧邻的左边有更小的元素。按照以下步骤，解决这个问题:

1.  遍历数组 **arr[]** 中的每个元素。
2.  对于每个元素，在左侧运行另一个循环。
    *   计算所有小于当前元素的元素，直到出现更大的元素或数组结束。
3.  根据以上观察打印答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
using namespace std;

// Function to find the length of the longest
// subarray with smaller elements on the immediate
// left for each element in the given array
void subarrayLength(int* arr, int n)
{
    for (int i = 0; i < n; i++) {
        int ans = 0;
        for (int j = i - 1; j >= 0; j--) {

            // If a greater element comes
            if (arr[i] <= arr[j]) {
                break;
            }
            // Else
            ans++;
        }
        cout << ans << " ";
    }
}

// Driver Code
int main()
{

    int n = 5;
    int arr[n] = { 1, 4, 2, 6, 3 };
    subarrayLength(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to find the length of the longest
// subarray with smaller elements on the immediate
// left for each element in the given array
static void subarrayLength(int arr[], int n)
{
    for(int i = 0; i < n; i++)
    {
        int ans = 0;
        for(int j = i - 1; j >= 0; j--)
        {

            // If a greater element comes
            if (arr[i] <= arr[j])
            {
                break;
            }

            // Else
            ans++;
        }
        System.out.print(ans + " ");
    }
}

// Driver Code
public static void main(String args[])
{
    int n = 5;
    int arr[] = { 1, 4, 2, 6, 3 };

    subarrayLength(arr, n);
}
}

// This code is contributed by gfgking
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the length of the longest
# subarray with smaller elements on the immediate
# left for each element in the given array
def subarrayLength(arr, n):

    for i in range(0, n):
        ans = 0
        for j in range(i-1, -1, -1):

            # If a greater element comes
            if (arr[i] <= arr[j]):
                break

            # Else
            ans += 1
        print(ans, end=" ")

# Driver Code
if __name__ == "__main__":

    n = 5
    arr = [1, 4, 2, 6, 3]
    subarrayLength(arr, n)

# This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to find the length of the longest
// subarray with smaller elements on the immediate
// left for each element in the given array
static void subarrayLength(int []arr, int n)
{
    for(int i = 0; i < n; i++)
    {
        int ans = 0;
        for(int j = i - 1; j >= 0; j--)
        {

            // If a greater element comes
            if (arr[i] <= arr[j])
            {
                break;
            }

            // Else
            ans++;
        }
        Console.Write(ans + " ");
    }
}

// Driver Code
public static void Main()
{
    int n = 5;
    int []arr = { 1, 4, 2, 6, 3 };

    subarrayLength(arr, n);
}
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
      // JavaScript code for the above approach

      // Function to find the length of the longest
      // subarray with smaller elements on the immediate
      // left for each element in the given array
      function subarrayLength(arr, n)
      {
          for (let i = 0; i < n; i++)
          {
              let ans = 0;
              for (let j = i - 1; j >= 0; j--) {

                  // If a greater element comes
                  if (arr[i] <= arr[j]) {
                      break;
                  }

                  // Else
                  ans++;
              }
              document.write(ans + " ");
          }
      }

      // Driver Code
      let n = 5;
      let arr = [1, 4, 2, 6, 3];
      subarrayLength(arr, n);

// This code is contributed by Potta Lokesh
  </script>
```

**Output**

```
0 1 0 3 0 
```

**时间复杂度:**O(N<sup>2</sup>)
T5】辅助空间: O(1)