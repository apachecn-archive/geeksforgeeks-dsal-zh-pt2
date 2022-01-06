# 给定数组中 K 个数字串联的最大可能数量

> 原文:[https://www . geeksforgeeks . org/给定数组中 k 个数字的最大可能连接数/](https://www.geeksforgeeks.org/maximum-possible-number-with-concatenations-of-k-numbers-from-given-array/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** 和一个正整数 **K** ，任务是从数组 **arr[]** 中选择 **K** 个整数，使得它们的连接形成最大可能的整数。创建数字时，必须至少选择一次所有数组元素。

**注:**始终保证 **N** 大于等于 **K** 。

**示例:**

> **输入:** arr[] = {3，2，7}，K = 3
> **输出:** 732
> **解释:**
> 由于每个数组元素至少要使用一次，最大可能的数量是 732。
> 
> **输入:** arr[] = {1，10，100}，K = 4
> T3】输出: 110100100

**做法:**以上问题可以通过[排序](https://www.geeksforgeeks.org/sorting-algorithms/)[将数字转换为字符串](https://www.geeksforgeeks.org/stdto_string-in-cpp/)来解决。最佳方法是一次获取所有数字。之后，取位数最多的数字。在平局的情况下，取字典上最大的数字。使用[到 _string()](https://www.geeksforgeeks.org/stdto_string-in-cpp/) 函数转换字符串中的所有数字。按照以下步骤解决问题:

*   初始化一个空字符串 **res** 来存储答案。
*   [按升序排列数组**数字[]** 。](https://www.geeksforgeeks.org/sort-c-stl/)
*   [初始化字符串向量](https://www.geeksforgeeks.org/array-strings-c-3-different-ways-create/) **v[]** 。
*   [使用变量 **i** 和](https://www.geeksforgeeks.org/range-based-loop-c/)[迭代范围](https://www.geeksforgeeks.org/vectorpush_back-vectorpop_back-c-stl/)**【0，K)** 将字符串编号**数字【I】**推入向量**v【】**。
*   将 **N** 的值减少 **K** 并将数值**数字【K-1】****N**次推入向量 **v[]** 。
*   [使用比较器功能对向量 **v[]** 进行排序。](https://www.geeksforgeeks.org/sorting-a-vector-in-c/)
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【v . size()-1，0】**，并将值**v【I】**添加到变量 **res** 中。
*   执行上述步骤后，打印 **res** 的值作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Custom comparator function
bool str_cmp(string s1, string s2)
{
    return (s1 + s2 < s2 + s1);
}

// Function to get the largest possible
// string
string largestNumber(vector<int> arr,
                     int K)
{
    int N = arr.size();

    // Initialize a new variable which
    // will store the answers.
    string res = "";

    // Sort the numbers array in
    // non-decreasing order
    sort(arr.begin(), arr.end());

    // Stores the array element which will
    // be used to construct the answer
    vector<string> v;

    // Take all numbers atleast once
    for (int i = 0; i < N; i++) {
        v.push_back(to_string(arr[i]));
    }
    K -= N;

    // Take the largest digits number
    // for remaining required numbers
    while (K) {
        v.push_back(to_string(arr[N - 1]));
        K--;
    }

    // Sort the final answer according to
    // the comparator function.
    sort(v.begin(), v.end(), str_cmp);
    for (int i = v.size() - 1; i >= 0; i--)
        res += v[i];

    return res;
}

// Driver Code
int main()
{
    vector<int> arr = { 1, 10, 100 };
    int K = 4;
    cout << largestNumber(arr, K);

    return 0;
}
```

## java 描述语言

```
<script>
      // JavaScript Program to implement
      // the above approach

      // Function to get the largest possible
      // string
      function largestNumber(arr,
          K) {
          let N = arr.length;

          // Initialize a new variable which
          // will store the answers.
          let res = "";
          // Sort the numbers array in
          // non-decreasing order
          arr.sort(function (a, b) { return a - b })

          // Stores the array element which will
          // be used to construct the answer
          let v = [];

          // Take all numbers atleast once
          for (let i = 0; i < N; i++) {
              v.push(arr[i].toString());
          }
          K -= N;

          // Take the largest digits number
          // for remaining required numbers
          while (K) {
              v.push(arr[N - 1].toString());
              K--;
          }

          // Sort the final answer according to
          // the comparator function.
          v.sort(function (s1, s2) { return parseInt(s1 + s2) - parseInt(s2 + s1) });
          for (let i = v.length - 1; i >= 0; i--)
              res += v[i];

          return res;
      }

      // Driver Code

      let arr = [1, 10, 100];
      let K = 4;
      document.write(largestNumber(arr, K));

     // This code is contributed by Potta Lokesh

  </script>
```

**Output:** 

```
110100100
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*