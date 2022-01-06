# 通过将奇数大小的子阵列移动到给定阵列的末端，最大化偶数索引和奇数索引处的元素和的差。

> 原文:[https://www . geeksforgeeks . org/通过将奇数大小的子阵列移动到给定阵列的末端来最大化偶数索引和奇数索引的元素总和的差/](https://www.geeksforgeeks.org/maximize-the-difference-of-sum-of-elements-at-even-indices-and-odd-indices-by-shifting-an-odd-sized-subarray-to-end-of-given-array/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是通过将任意**奇数**长度的**子数组**移动到数组的**末端**来最大化**偶数索引**处的元素与**奇数索引**处的元素的**和**之差。

**例:**

> ***输入:*** arr[] = {1，2，3，4，5，6}
> ***输出:*** 3
> **解释**:最初偶数索引处的元素之和= 1 + 3 + 5 = 9
> 奇数索引处的元素之和= 2 + 4 + 6 = 12
> 差值= 9 -12 = -3
> 将子阵列从[0，2]移动到最后，阵列变成{ 0 3}
> 偶数索引处的元素之和= 4 + 6 + 2 = 12
> 奇数索引处的元素之和= 5 + 1 + 3 = 9
> 差值= 12–9 = 3
> 这给出了所有此类移位中最大值等于 3 的答案。
> 
> **输入:** arr[] = {3，4，8 }
> T3】输出: 7

**逼近**:任务可以通过**数学求解，**使用[前缀求和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)技术。这个问题可以分为 4 种情况:

> **<u>情况 1</u> :** 当数组 **N 的长度为偶数**且 **l** (子数组的开始)为偶数 **{a，b，c，d，e，f}** 对于 **l = 2，r =4(基于一个索引)**
> **初始:+a–b+ c–d+e-f**在将子数组【2，4】移动到数组的末尾时 d}
> **决赛:+a-e+f–b+ c-d**
> **跳水时将阵列分成 3 个子组[1，l]，[l，r]，(r，N]。**
> 零件 1**【1，l)** 的符号保持不变，零件 2**【l，r】**保持不变，零件 3 **(r，N)**换挡后变为负(符号相反)。
> 如果计算了 prefix_sum 数组，则移位后的和变为
> sum 1 = prefix _ sum(l-1)+(prefix _ sum(r)–prefix _ sum(l-1))–((prefix _ sum(N)–prefix _ sum(r))
> **sum 1 = 2 * prefix _ sum(r)–prefix _ sum(N)**
> 
> **<u>情况 2</u> :** 当数组 **N 的长度为偶数时**和 **l** (子数组的开始)为奇数{a，b，c，d，e，f}对于 **l = 3，r = 5(基于一个索引)**
> **初始:+a–b+ c–d+e-f**在将[3，5]移动到末尾时，数组变为= **{a，b，f e}**
> **最终:+a–b+ f–c+d–e**
> **潜水时，将阵列分成 3 个子组[1，l]，[l，r]，(r，N]。**
> 零件 1**【1，l)** 的符号保持不变，零件 2**【l，r】**在换挡后变为反符号，零件 3 **(r，N)**变为反符号。
> 如果计算了 prefix_sum 数组，则移位后的和变为
> sum 2 = prefix _ sum(l-1)–(prefix _ sum(r)–prefix _ sum(l-1))–((prefix _ sum(N)–prefix _ sum(r))
> **sum 2 = 2 * prefix _ sum(l-1)–prefix _ sum(N)**
> 
> **<u>情况 3</u> :** 当数组 **N 的长度为奇数**和 **l** (子数组的开始)为偶数{a，b，c，d，e}时，l = 2，r = 4(基于一个索引)
> **初始:+a–b+ c–d+e**在将子数组【2，4】移动到末尾时，数组变为= **{a，e，b，c， d}**
> **最终:+a–e+b–c+d**
> 潜水时，将阵列分成 3 个子组**【1，l】、【l，r】、【r，N】**。
> 第 1 部分**【1，l)** 的符号保持不变，第 2 部分**【l，r】**在换挡后变为反符号，第 3 部分 **(r，N)**变为负符号(反符号)。
> 如果计算前缀 _sum 数组，则移位后的和变为
> sum3 =前缀 _ sum(l-1)–(前缀 _ sum(r)–前缀 _ sum(l-1))–((前缀 _ sum(N)–前缀 _sum(r))
> **sum3 = 2*前缀 _ sum(l-1)–前缀 _sum(N)**
> 
> **<u>情况 4</u> :** 当数组的长度 **N 为奇数**和 **l** (子数组的开始)为奇数{a，b，c，d，e}时，l = 3，r =3(基于一个索引)
> **初始:+a–b+ c–d+e**在将[3，5]移动到末尾时，数组变为= **{a，b，d，e， c}**
> **决赛:+a–b+ d–e+c**
> 跳水时将阵列分成 3 个子组**【1，l】、【l，r】、【r，N】**。
> 第 1 部分**【1，l)** 的符号保持不变，第 2 部分**【l，r】**成为相反符号，第 3 部分 **(r，N)**保持不变。
> 如果计算前缀 _sum 数组，则移位后的和变为
> sum 4 = prefix _ sum(l-1)+(prefix _ sum(r)–prefix _ sum(l-1))–((prefix _ sum(N)–prefix _ sum(r))
> **sum 4 = 2 * prefix _ sum(r)–prefix _ sum(N)**
> 
> *   如果 **n 为偶数**结果变为: **max(sum1，sum2)。**
> *   如果 **n 为奇数**结果变为: **max(sum3，sum4)。**

按照以下步骤解决问题:

*   用 0 初始化大小为 **n+1** 的向量**前缀 _ 和**
*   现在通过将数组的奇数索引乘以-1 来修改它们。
*   遍历[ **1，n]** 范围内的数组，填充**前缀 _sum** 向量。
*   如果数组的大小是**甚至**
*   将变量 **maxval** 初始化为 **-1e8** 来存储最大和。
*   迭代**前缀和**向量并检查
    *   如果我将 maxval 指定为 **max(maxval，2 * prefix _ sum[I]–prefix _ sum[n])**。
    *   否则将 maxval 指定为 **max(maxval，2 * prefix _ sum[I]–prefix _ sum[n])**。
*   如果数组的大小为**奇数**。
*   将变量 **maxval** 初始化为 **-1e8** 来存储最大和。
*   迭代**前缀和**向量并检查
    *   如果我将 maxval 指定为 **max(maxval，2 * prefix _ sum[I–1]–prefix _ sum[n])**
    *   否则将 maxval 指定为 **max(maxval，2 * prefix _ sum[I]–prefix _ sum[n])**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum value of
// difference between sum of elements
// at even indices and sum of elements
// at odd indices by shifting
// a subarray of odd length to the
// end of the array
int find_maxsum(int arr[], int n)
{
    vector<int> prefix_sum(n + 1, 0);

      // Modify the array to keep
    // alternative +ve and -ve
    for (int i = 0; i < n; i++) {
        if (i % 2 == 1) {
            arr[i] = -arr[i];
        }
    }

    // Function to find the prefix sum
    for (int i = 1; i <= n; i++) {
        prefix_sum[i] = prefix_sum[i - 1]
            + arr[i - 1];
    }

    // If n is even
    if (n % 2 == 0) {

          // Initialize the maxval to -1e8
        int maxval = -1e8;
        for (int i = 1; i <= n; i++) {

              // If i is even (case-1)
            if (i % 2 == 0) {
                maxval = max(maxval, 2 *
                             prefix_sum[i]
                             - prefix_sum[n]);
            }

            // If i is odd (case-2)
            else {
                maxval = max(maxval, 2 *
                             prefix_sum[i - 1]
                             - prefix_sum[n]);
            }
        }

        // return the maxval
        return maxval;
    }
    else {
        // Initialize the maxval to -1e8
        int maxval = -1e8;
        for (int i = 1; i <= n; i++) {

              // If i is even (case 3)
            if (i % 2 == 0) {
                maxval = max(maxval, 2 *
                             prefix_sum[i - 1]
                             - prefix_sum[n]);
            }

            // If i is odd (case 4)
            else {
                maxval = max(maxval, 2 *
                             prefix_sum[i]
                             - prefix_sum[n]);
            }
        }

        // Return the maxval
        return maxval;
    }
}

int main()
{
    // Initialize an array
    int arr[] = { 1, 2, 3, 4, 5, 6 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call
    cout << find_maxsum(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class GFG
{

  // Function to find the maximum value of
  // difference between sum of elements
  // at even indices and sum of elements
  // at odd indices by shifting
  // a subarray of odd length to the
  // end of the array
  static int find_maxsum(int arr[], int n)
  {
    int prefix_sum[] = new int[n + 1];
    for(int i = 0; i < n + 1; i++) {
      prefix_sum[i] = 0;
    }

    // Modify the array to keep
    // alternative +ve and -ve
    for (int i = 0; i < n; i++) {
      if (i % 2 == 1) {
        arr[i] = -arr[i];
      }
    }

    // Function to find the prefix sum
    for (int i = 1; i <= n; i++) {
      prefix_sum[i] = prefix_sum[i - 1]
        + arr[i - 1];
    }

    // If n is even
    if (n % 2 == 0) {

      // Initialize the maxval to -1e8
      int maxval = (int)-1e8;
      for (int i = 1; i <= n; i++) {

        // If i is even (case-1)
        if (i % 2 == 0) {
          maxval = Math.max(maxval, 2 *
                            prefix_sum[i]
                            - prefix_sum[n]);
        }

        // If i is odd (case-2)
        else {
          maxval = Math.max(maxval, 2 *
                            prefix_sum[i - 1]
                            - prefix_sum[n]);
        }
      }

      // return the maxval
      return maxval;
    }
    else
    {

      // Initialize the maxval to -1e8
      int maxval = (int)-1e8;
      for (int i = 1; i <= n; i++) {

        // If i is even (case 3)
        if (i % 2 == 0) {
          maxval = Math.max(maxval, 2 *
                            prefix_sum[i - 1]
                            - prefix_sum[n]);
        }

        // If i is odd (case 4)
        else {
          maxval = Math.max(maxval, 2 *
                            prefix_sum[i]
                            - prefix_sum[n]);
        }
      }

      // Return the maxval
      return maxval;
    }
  }

  public static void main(String args[])
  {

    // Initialize an array
    int arr[] = { 1, 2, 3, 4, 5, 6 };
    int N = arr.length;

    // Function call
    System.out.println(find_maxsum(arr, N));
  }
}

// This code is contributed by Samim Hossain Mondal.
```

**Output**

```
3
```

***时间复杂度:*** O(N)
***辅助空间:*** O(N)