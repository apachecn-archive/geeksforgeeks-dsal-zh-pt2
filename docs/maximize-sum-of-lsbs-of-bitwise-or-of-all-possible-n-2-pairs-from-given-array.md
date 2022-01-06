# 最大化给定数组中所有可能的 N/2 对的按位或的 LSB 之和

> 原文:[https://www . geeksforgeeks . org/最大化给定数组中所有可能的 n-2 对位或的 LSB 总和/](https://www.geeksforgeeks.org/maximize-sum-of-lsbs-of-bitwise-or-of-all-possible-n-2-pairs-from-given-array/)

给定一个由 **N** 正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，其中 **N** 为偶数，任务是形成 **N/2** 对，使得所有这些对的[位“或”位](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)的[最低有效位](https://www.geeksforgeeks.org/find-significant-set-bit-number/)之和最大。

**示例:**

> **输入:** arr[] = {1，2，3，4，5，6，7，8}
> **输出:** 8
> **解释:**
> 关于成对为(8，4)、(6，2)、(1，3)、(5，7)、 对的按位 OR 由下式给出:
> 8 OR 4 = 12 和 LSB = 4
> 6 OR 2 = 6 和 LSB = 2
> 1 OR 3 = 3 和 LSB = 1
> 5 OR 7 = 7 和 LSB = 1
> 所有 LSB 的和为 4 + 2 + 1 + 1 = 8，这是最大可能和。
> 
> **输入:** arr[] = {1，2，3，4，5}
> **输出:** 3

**方法:**可以通过找到每个数组元素的 LSB**arr【I】**并将其存储在另一个数组中来解决给定的问题，比如说 **lsb_arr[]** 和[按照降序对这个数组进行排序](https://www.geeksforgeeks.org/python-list-sort-method/)。现在，只存储每个数组元素的 LSB 就足够了，因为在答案中，只需要考虑 [**LSB**](https://www.geeksforgeeks.org/flip-consecutive-set-bits-starting-from-lsb-of-a-given-number/) 。因此，只有最低有效位可以用于[逐位或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)运算。现在，考虑每对 **(i，i + 1)** ，并将这两个的最小值加到结果中。按照以下步骤解决给定的问题:

*   [初始化一个列表](https://www.geeksforgeeks.org/python-which-is-faster-to-initialize-lists/) **lsb_arr[]** 来存储所有数组元素的最低有效位 **arr[i]** 。
*   [遍历范围](https://www.geeksforgeeks.org/iterate-over-a-list-in-python/)**【0，N)** ，将每个**arr【I】**的 LSB 存储在 **lsb_arr[]** 中。
*   [按降序排列列表**LSB _ arr[]**](https://www.geeksforgeeks.org/sort-in-python/)。
*   将变量**和**初始化为 **0** ，以存储[最低有效位](https://www.geeksforgeeks.org/position-of-rightmost-set-bit/)的结果和。
*   [使用变量 **i** 遍历范围](https://www.geeksforgeeks.org/iterate-over-a-list-in-python/)**【0，N】**，将 **(i + 1)** 位置的元素值添加到变量 **ans** 中，并将 **i** 的值增加 **2** 。
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function top get LSB value of v
int chk(int n)
{

    // Binary conversion
    vector<int> v;

    while (n != 0) {
        v.push_back(n % 2);
        n = n / 2;
    }

    for (int i = 0; i < v.size(); i++) {
        if (v[i] == 1) {
            return pow(2, i);
        }
    }

    return 0;
}

// Function to find the sum of LSBs of
// all possible pairs of the given array
void sumOfLSB(int arr[], int N)
{

    // Stores the LSB of array elements
    vector<int> lsb_arr;
    for (int i = 0; i < N; i++) {

        // Storing the LSB values
        lsb_arr.push_back(chk(arr[i]));
    }
    // Sort the array lab_arr[]
    sort(lsb_arr.begin(), lsb_arr.end(), greater<int>());

    int ans = 0;

    for (int i = 0; i < N - 1; i += 2) {

        // Taking pairwise sum to get
        // the maximum sum of LSB
        ans += (lsb_arr[i + 1]);
    }

    // Print the result
    cout << (ans);
}

// Driver Code
int main()
{
    int N = 5;
    int arr[] = { 1, 2, 3, 4, 5 };

    // Function Call
    sumOfLSB(arr, N);
}

// This code is contributed by Potta Lokesh
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Function top get LSB value of v
static int chk(int n)
{

    // Binary conversion
    Vector<Integer> v = new Vector<Integer>();

    while (n != 0) {
        v.add(n % 2);
        n = n / 2;
    }

    for (int i = 0; i < v.size(); i++) {
        if (v.get(i) == 1) {
            return (int) Math.pow(2, i);
        }
    }

    return 0;
}

// Function to find the sum of LSBs of
// all possible pairs of the given array
static void sumOfLSB(int arr[], int N)
{

    // Stores the LSB of array elements
    Vector<Integer> lsb_arr = new Vector<Integer>() ;
    for (int i = 0; i < N; i++) {

        // Storing the LSB values
        lsb_arr.add(chk(arr[i]));
    }

    // Sort the array lab_arr[]
    Collections.sort(lsb_arr);

    int ans = 0;

    for (int i = 0; i < N - 1; i += 2) {

        // Taking pairwise sum to get
        // the maximum sum of LSB
        ans += (lsb_arr.get(i + 1));
    }

    // Print the result
    System.out.print(ans);
}

// Driver Code
public static void main(String[] args)
{
    int N = 5;
    int arr[] = { 1, 2, 3, 4, 5 };

    // Function Call
    sumOfLSB(arr, N);
}
}

// This code contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python program for the above approach

# Function top get LSB value of v
def chk(v):

    # Binary conversion
    v = list(bin(v)[2:])
    v.reverse()

    if('1' in v):
        v = v.index('1')
        return (2**v)
    else:
        return 0

# Function to find the sum of LSBs of
# all possible pairs of the given array
def sumOfLSB(arr, N):

    # Stores the LSB of array elements
    lsb_arr = []
    for i in range(N):

        # Storing the LSB values
        lsb_arr.append(chk(arr[i]))

    # Sort the array lab_arr[]
    lsb_arr.sort(reverse=True)

    ans = 0

    for i in range(0, N-1, 2):

        # Taking pairwise sum to get
        # the maximum sum of LSB
        ans += (lsb_arr[i+1])

    # Print the result
    print(ans)

# Driver Code
N = 5
arr = [1, 2, 3, 4, 5]

# Function Call
sumOfLSB(arr, N)
```

## java 描述语言

```
<script>
    // JavaScript program for the above approach

    // Function top get LSB value of v
    const chk = (n) => {

        // Binary conversion
        let v = [];

        while (n != 0) {
            v.push(n % 2);
            n = parseInt(n / 2);
        }

        for (let i = 0; i < v.length; i++) {
            if (v[i] == 1) {
                return Math.pow(2, i);
            }
        }

        return 0;
    }

    // Function to find the sum of LSBs of
    // all possible pairs of the given array
    const sumOfLSB = (arr, N) => {

        // Stores the LSB of array elements
        let lsb_arr = [];
        for (let i = 0; i < N; i++) {

            // Storing the LSB values
            lsb_arr.push(chk(arr[i]));
        }
        // Sort the array lab_arr[]

        lsb_arr.sort((a, b) => a - b)
        let ans = 0;

        for (let i = 0; i < N - 1; i += 2) {

            // Taking pairwise sum to get
            // the maximum sum of LSB
            ans += (lsb_arr[i + 1]);
        }

        // Print the result
        document.write(ans);
    }

    // Driver Code
    let N = 5;
    let arr = [1, 2, 3, 4, 5];

    // Function Call
    sumOfLSB(arr, N);

    // This code is contributed by rakeshsahni
</script>
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG
{

// Function top get LSB value of v
static int chk(int n)
{

    // Binary conversion
    List<int> v = new List<int>();

    while (n != 0) {
        v.Add(n % 2);
        n = n / 2;
    }

      int j = 0;
    foreach(int i in v) {
        if (i == 1) {
            return (int) Math.Pow(2.0, (double)j);
        }
          j++;
    }

    return 0;
}

// Function to find the sum of LSBs of
// all possible pairs of the given array
static void sumOfLSB(int[] arr, int N)
{

    // Stores the LSB of array elements
      int[] lsb_arr = new int[N];

    for (int i = 0; i < N; i++) {

        // Storing the LSB values
        lsb_arr[i] = chk(arr[i]);
    }

    // Sort the array lab_arr[]
    Array.Sort(lsb_arr);

    int ans = 0;

    for (int i = 0; i < N - 1; i += 2) {

        // Taking pairwise sum to get
        // the maximum sum of LSB
        ans += (lsb_arr[i + 1]);
    }

    // Print the result
    Console.WriteLine(ans);
}

// Driver Code
static public void Main (){

    int N = 5;
    int[] arr = { 1, 2, 3, 4, 5 };

    // Function Call
    sumOfLSB(arr, N);
}
}

// This code is contributed by Dharanendra L V.
```

**Output:** 

```
3
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*