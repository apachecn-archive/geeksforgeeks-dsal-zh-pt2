# 使数组异或等于其总和一半的最小插入数

> 原文:[https://www . geeksforgeeks . org/最小插入对等于其和的一半的数组进行异或运算/](https://www.geeksforgeeks.org/minimum-insertions-to-make-xor-of-an-array-equal-to-half-of-its-sum/)

给定一个正整数数组，任务是找出该数组中需要完成的最小插入次数，使该数组的异或等于其和的一半，即 **2 *所有元素的异或=所有元素的和**
**示例:**

> **输入:** arr[] = {1 2 3 4 5}
> **输出:** 1 16
> **解释:**
> 在修改后的数组{1 2 3 4 5 1 16}中，
> sum = 1+2+3+4+5+1+16 = 32
> xor = 1 ^ 2 ^ 3 ^ 4 ^ 5 ^ 1 ^ 16 = 16
> 和，2 * 16 == 32
> 由此可知
> 
> **输入:** 7 11 3 25 51 32 9 29
> **输出:** 17 184
> **解释:**
> 在修改后的数组中{ 7 11 3 25 51 32 9 29 17 184}
> 和= 7+11+3+25+51+32+9+29+17+184 = 368
> 异或= 7 ^ 11 ^ 3 ^ 25 ^ 51 ^ 32 ^ 9 ^ 29 ^ 17 184 = 184
> 和，2 * 184 == 368
> 因此，条件**所有元素的 2 *异或=所有元素的和**成立。

**方法:**
要解决这个问题，我们需要重点关注 XOR 的两个基本性质:

*   异或= 0
*   异或 0 = 1

我们需要按照以下步骤来解决问题:

*   计算所有数组元素 (S)的[和所有元素](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/) (X)的[异或。如果 **S == 2*X** ，则不需要改变阵列。这种情况打印-1。](https://www.geeksforgeeks.org/find-xor-of-all-elements-in-an-array/)
*   否则，请执行以下操作:
    1.  如果 **X = 0** ，只需将 **S** 插入阵列即可。现在异或是 **S** ，和是 **2S** 。
    2.  否则，在数组中加上 **X** ，使数组的新 Xor 等于 0。然后，在阵列中插入 **S+X** 。现在，和是 **2(S+X)** ，异或是 **S+X**

下面是上述方法的实现。

## C++

```
// C++ Program to make XOR of
// of all array elements equal
// to half of its sum
// by minimum insertions

#include <bits/stdc++.h>
using namespace std;

// Function to make XOR of the
// array equal to half of its sum
int make_xor_half(vector<int>& arr)
{
    int sum = 0, xr = 0;

    // Calculate the sum and
    // Xor of all the elements
    for (int a : arr) {
        sum += a;
        xr ^= a;
    }

    // If the required condition
    // satisfies already, return
    // the original array
    if (2 * xr == sum)
        return -1;

    // If Xor is already zero,
    // Insert sum
    if (xr == 0) {
        arr.push_back(sum);
        return 1;
    }

    // Otherwise, insert xr
    // and insert sum + xr
    arr.push_back(xr);
    arr.push_back(sum + xr);
    return 2;
}

// Driver Code
int main()
{

    int N = 7;
    vector<int> nums
        = { 3, 4, 7, 1, 2, 5, 6 };

    int count = make_xor_half(nums);

    if (count == -1)
        cout << "-1" << endl;
    else if (count == 1)
        cout << nums[N] << endl;
    else
        cout << nums[N] << " "
             << nums[N + 1] << endl;

    return 0;
}
```

## 蟒蛇 3

```
# Python3 program to make XOR of
# of all array elements equal to 
# half of its sum by minimum 
# insertions

# Function to make XOR of the
# array equal to half of its sum
def make_xor_half(arr):

    sum = 0; xr = 0;

    # Calculate the sum and
    # Xor of all the elements
    for a in arr:
        sum += a;
        xr ^= a;

    # If the required condition
    # satisfies already, return
    # the original array
    if (2 * xr == sum):
        return -1;

    # If Xor is already zero,
    # Insert sum
    if (xr == 0):
        arr.append(sum);
        return 1;

    # Otherwise, insert xr
    # and insert sum + xr
    arr.append(xr);
    arr.append(sum + xr);
    return 2;

# Driver code
if __name__ == "__main__":

    N = 7;
    nums = [ 3, 4, 7, 1, 2, 5, 6 ];
    count = make_xor_half(nums);

    if (count == -1):
        print("-1");

    elif (count == 1):
        print(nums[N]);

    else:
        print(nums[N], nums[N + 1]);

# This code is contributed by AnkitRai01
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to make XOR of all
// array elements equal to half
// of its sum by minimum insertions
import java.util.*;

class GFG{

// Function to make XOR of the
// array equal to half of its sum
static int make_xor_half(ArrayList<Integer> arr)
{
  int sum = 0, xr = 0;

  // Calculate the sum and
  // Xor of all the elements
  for (int i = 0;
           i < arr.size(); i++) 
  {
    int a = arr.get(i);
    sum += a;
    xr ^= a;
  }

  // If the required condition
  // satisfies already, return
  // the original array
  if (2 * xr == sum)
    return -1;

  // If Xor is already zero,
  // Insert sum
  if (xr == 0)
  {
    arr.add(sum);
    return 1;
  }

  // Otherwise, insert xr
  // and insert sum + xr
  arr.add(xr);
  arr.add(sum + xr);
  return 2;
}

// Driver code
public static void main(String[] args)
{
  int N = 7;
  ArrayList<Integer> nums =
  new ArrayList<Integer>(
      Arrays.asList(3, 4, 7,
                    1, 2, 5, 6));

  int count = make_xor_half(nums);

  if (count == -1)
    System.out.print(-1 + "\n");
  else if (count == 1)
    System.out.print(nums.get(N) + "\n");
  else
    System.out.print(nums.get(N) + " " +
                     nums.get(N + 1) + "\n");
}
}

// This code is contributed by Chitranayal
```

## C#

```
// C# program to make XOR of all
// array elements equal to half
// of its sum by minimum insertions
using System;
using System.Collections;
using System.Collections.Generic;

class GFG{

// Function to make XOR of the
// array equal to half of its sum
static int make_xor_half(ArrayList arr)
{
    int sum = 0, xr = 0;

    // Calculate the sum and
    // Xor of all the elements
    foreach(int a in arr)
    {
        sum += a;
        xr ^= a;
    }

    // If the required condition
    // satisfies already, return
    // the original array
    if (2 * xr == sum)
        return -1;

    // If Xor is already zero,
    // Insert sum
    if (xr == 0)
    {
        arr.Add(sum);
        return 1;
    }

    // Otherwise, insert xr
    // and insert sum + xr
    arr.Add(xr);
    arr.Add(sum + xr);
    return 2;
}

// Driver code
public static void Main(string[] args)
{
    int N = 7;
    ArrayList nums = new ArrayList(){ 3, 4, 7, 1,
                                      2, 5, 6 };

    int count = make_xor_half(nums);

    if (count == -1)
        Console.Write(-1 + "\n");
    else if (count == 1)
        Console.Write(nums[N] + "\n");
    else
        Console.Write(nums[N] + " " +
                      nums[N + 1] + "\n");
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript Program to make XOR of
// of all array elements equal
// to half of its sum
// by minimum insertions

// Function to make XOR of the
// array equal to half of its sum
function make_xor_half(arr)
{
    let sum = 0, xr = 0;

    // Calculate the sum and
    // Xor of all the elements
    for (let a = 0; a < arr.length; a++)
    {
        sum += arr[a];
        xr ^= arr[a];
    }

    // If the required condition
    // satisfies already, return
    // the original array
    if (2 * xr == sum)
        return -1;

    // If Xor is already zero,
    // Insert sum
    if (xr == 0) {
        arr.push(sum);
        return 1;
    }

    // Otherwise, insert xr
    // and insert sum + xr
    arr.push(xr);
    arr.push(sum + xr);
    return 2;
}

// Driver Code

    let N = 7;
    let nums
        = [ 3, 4, 7, 1, 2, 5, 6 ];

    let count = make_xor_half(nums);

    if (count == -1)
        document.write("-1<br>");
    else if (count == 1)
        document.write(nums[N] + "<br>");
    else
        document.write(nums[N] + " "
             + nums[N + 1]);

</script>
```

**Output:** 

```
28
```

**时间复杂度:** *O(N)* 其中 N 是数组的大小。