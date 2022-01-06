# 在给定的大数数组中找到第 k 个最大的数

> 原文:[https://www . geesforgeks . org/find-kth-给定大数数组中的最大数/](https://www.geeksforgeeks.org/finding-kth-largest-number-in-given-array-of-large-numbers/)

给定一个代表大数的字符串数组**arr【】**和一个整数 **K，**的任务是在给定的数组中找到第几个最大的整数 **K** 。

**示例:**

> **输入:**arr[]= {“10”、“7”、“3”、“6”}，K = 3
> **输出:**“6”
> **说明:**以非递减方式排列数组会给出{“3”、“6”、“7”、“10”}。
> 显然第三大整数是 6。
> 
> **输入:**arr[]= {“10”、“7”、“6”、“7”、“11”}，K = 2
> **输出:**“10”
> **解释:**以非递减方式排列数组将给出{“6”、“7”、“7”、“10”、“11”}
> 显然第二大整数是 10。

**天真法(不正确):**通常这类问题可以通过将字符串转换为整数，然后找到第 k 个最大数来解决。但是既然我们说的是大数，也就是表示整数长度的字符串 **100** ，那么**就不可能把它们转换成整数**。

**正确方法:**这个问题可以使用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)通过实现自定义比较器来解决。

按照以下步骤解决给定的问题。

*   使用自定义排序以非递减顺序对数组进行排序。
*   在自定义排序功能中将有两种情况:
    *   两个传递的字符串大小相等，那么只有当一个字符串在字典上小于另一个字符串时才交换。
    *   两个传递的字符串的大小不相等，那么只有当一个字符串的大小小于另一个字符串的大小时才交换。
*   排序后打印 Kth 最大整数。

下面是上述方法的实现:

## C++

```
// C++ implementation for above approach

#include <bits/stdc++.h>
using namespace std;

// Custom comparator to sort
// the array of strings
bool comp(string& a, string& b)
{
    // If sizes of string a and b are equal
    // then return true if a is
    // lexicographically smaller than b
    if (a.size() == b.size())
        return a < b;

    // Return true if size of a
    // is smaller than b
    return a.size() < b.size();
}

// Function that returns
// kth largest integer
string kthLargestInteger(
    string arr[], int n, int k)
{

    // Sort string arr in non-decreasing order
    // using custom comparator function
    sort(arr, arr + n, comp);

    return arr[n - k];
}

// Driver Code
int main()
{
    int N = 4;
    string arr[N] = { "10", "7", "3", "6" };
    int K = 4;

    cout << kthLargestInteger(arr, N, K)
         << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
import java.util.*;

class GFG {
    // Custom comparator to sort
    // the array of strings

    // Function that returns
    // kth largest integer
    static String kthLargestInteger(String arr[], int n,
                                    int k)
    {

        // Sort string arr in non-decreasing order
        // using custom comparator function
        Arrays.sort(arr, new Comparator<String>() {
            @Override public int compare(String a, String b)
            {
                return Integer.valueOf(a).compareTo(
                    Integer.valueOf(b));
            }
        });

        return arr[n - k];
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 4;
        String arr[] = { "10", "7", "3", "6" };
        int K = 4;

        System.out.println(kthLargestInteger(arr, N, K));
    }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python 3 implementation for above approach

# Function that returns
# kth largest integer
def kthLargestInteger(
        arr, n, k):

    # Sort string arr in non-decreasing order
    # using custom comparator function
    arr = [int(i) for i in arr]
    arr.sort()

    return arr[n - k]

# Driver Code
if __name__ == "__main__":

    N = 4
    arr = ["10", "7", "3", "6"]
    K = 4

    print(kthLargestInteger(arr, N, K))

    # This code is contributed by ukasp.
```

## C#

```
// C# code for the above approach
using System;

public class GFG
{

  // Custom comparator to sort
  // the array of strings

  // Function that returns
  // kth largest integer
  static String kthLargestint(String []arr, int n,
                              int k)
  {

    // Sort string arr in non-decreasing order
    // using custom comparator function
    Array.Sort(arr,CompareStrings);

    return arr[n - k];
  }
  static int CompareStrings(string a, string b)
  {
    return Int32.Parse(a).CompareTo(
      Int32.Parse(b));
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int N = 4;
    String []arr = { "10", "7", "3", "6" };
    int K = 4;

    Console.WriteLine(kthLargestint(arr, N, K));
  }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javsacript implementation for above approach

// Custom comparator to sort
// the array of strings
function comp(a, b)
{

  // If sizes of string a and b are equal
  // then return true if a is
  // lexicographically smaller than b
  if (a.length == b.length)
    return a - b;

  // Return true if size of a
  // is smaller than b
  return (a.length - b.length);
}

// Function that returns
// kth largest integer
function kthLargestInteger(arr, n, k) {

  // Sort string arr in non-decreasing order
  // using custom comparator function
  arr.sort(comp);
  console.log(arr)

  return arr[n - k];
}

// Driver Code

let N = 4;
let arr = ["10", "7", "3", "6"];
let K = 4;

document.write(kthLargestInteger(arr, N, K))

// This code is contributed by saurbh_jaiswal.
</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(N * log N)，其中 N 为数组的大小。

**辅助空间:** O(1)