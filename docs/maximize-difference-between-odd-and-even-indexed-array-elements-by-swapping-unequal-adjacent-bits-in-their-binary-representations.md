# 通过交换奇数和偶数索引数组元素的二进制表示中不相等的相邻位来最大化奇数和偶数索引数组元素之间的差异

> 原文:[https://www . geesforgeks . org/通过交换二进制表示中不相等的相邻位来最大化奇数和偶数索引数组元素之间的差异/](https://www.geeksforgeeks.org/maximize-difference-between-odd-and-even-indexed-array-elements-by-swapping-unequal-adjacent-bits-in-their-binary-representations/)

给定一个由正整数 **N** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是通过多次交换任意数组元素的二进制表示中的不相等的相邻位，找到位于数组偶数和奇数索引处的数组元素的[和之间的最大绝对差。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)

**示例:**

> **输入:** arr[] = {5，7，3，1，8}
> **输出:** 9
> **解释:**
> arr[0]=(5)<sub>10</sub>=(101)<sub>2</sub>。左移位使 arr[0]=(110)<sub>2</sub>=(6)<sub>10</sub>。
> 因此，arr[]数组修改为{5，7，3，1，8}。
> 因此，最大绝对差=(6+3+8)–(7+1)= 9。
> 
> **输入:** arr[] = {54，32，11，23}
> **输出:** 58
> **解释:**
> 通过向左移动 arr[0] (= 54)的最后两个设置位，将 arr[0]修改为 60。因此，数组 arr[]修改为{60，32，11，23}。
> 通过右移 arr[1] (= 32)的所有设置位，将 arr[1]修改为 1。因此，数组 arr[]修改为{60，1，11，23}
> 通过左移 arr[2] (= 11)的最后三个设置位，将 arr[2]修改为 14。因此，数组 arr[]修改为{60，1，14，23}。
> 通过右移 arr[3] (= 23)的所有设置位，将 arr[3]修改为 15。因此，数组 arr[]修改为{60，1，14，15}。
> 因此，最大绝对差=(60+14)–(15+1)= 58。

**进场:**思路是利用观察任何[设定位](https://www.geeksforgeeks.org/set-k-th-bit-given-number/)都可以移动到任何其他位置。按照以下步骤解决问题:

*   定义一个函数，比如**最大化()**，通过移动两个不相等的相邻位来[最大化一个数。](https://www.geeksforgeeks.org/maximize-given-integer-by-swapping-pairs-of-unequal-bits/)
*   定义一个函数，比如**最小化()**，通过移动两个不相等的相邻位来最小化一个数。
*   执行以下操作:
    *   初始化一个变量，比如**和**，来存储最小化的值。
    *   要最小化一个数字，将所有[设置位](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)移到右边位置，将所有未设置位移到左边位置。
    *   遍历范围**【0，设置位计数–1】**并将 **ans** 更新为 **ans | 1** 。如果 **i** 不等于设置位的[计数，则](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)[左移](https://www.geeksforgeeks.org/left-shift-right-shift-operators-c-cpp/) **ans** 到 **1** 。
    *   返回**和**的值。
*   首先，找出通过最大化放置在偶数索引处的元素和最小化放置在奇数索引处的元素所获得的差异。将其存储在一个变量中，比如 **caseOne** 。
*   现在，找出通过最小化放置在偶数索引处的元素和最大化放置在奇数索引处的元素所获得的差异。将其存储在一个变量中，比如**案例二**。
*   完成以上步骤后，打印**案例一**和**案例二**的最大值。

下面是上述方法的实现:

## C++

```
// CPP program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to count total number
// of bits present in a number
int countBit(int n){
  return int(log2(n))+1;
}

// Function to count total
// set bits in a number
int countSetBit(int n){

  // Stores the count
  // of set bits
  int ans = 0;

  while(n > 0){

    ans += (n & 1);

    // Right shift by 1
    n >>= 1;
  }

  // Return the final count
  return ans;
}

// Function to find maximum number
// by shifting two unequal bits
int maximize(int n){

  // Count set bits in number n
  int bits = countBit(n);
  int setBits = countSetBit(n);
  int ans = 0;

  // Iterate the string bits
  for(int i = 0; i < bits; i++){

    if (i < setBits)
      ans |= 1;
    if(i != setBits - 1)
      ans <<= 1;

  }
  return ans;
}

// Function to find minimum number
// by shifting two unequal bits
int minimize(int n){

  int setBits = countSetBit(n);
  int ans = 0;

  // Iterate the set bit
  for (int i = 0; i < setBits; i++){
    ans |= 1;
    if (i != setBits - 1)
      ans <<= 1;
  }
  return ans;
}

// Function to find the maximum difference
int maxDiff(vector<int> arr){

  // Stores the maximum difference
  int caseOne = 0;

  // Stores the sum of elements
  // placed at odd positions
  int SumOfOdd = 0;

  // Stores the sum of elements
  // placed at even positions
  int SumOfeven = 0;

  // Traverse the array
  for(int i = 0; i < arr.size(); i++){
    if (i % 2)
      SumOfOdd += minimize(arr[i]);

    else
      SumOfeven += maximize(arr[i]);
  }

  // Update CaseOne
  caseOne = abs(SumOfOdd - SumOfeven);

  // Stores the maximum difference
  int caseTwo = 0;

  // Assign value O
  SumOfOdd = 0;
  SumOfeven = 0;

  // Traverse the array
  for(int i = 0; i < arr.size(); i++)
  {
    if (i % 2)
      SumOfOdd += maximize(arr[i]);
    else
      SumOfeven += minimize(arr[i]);
  }
  // Update caseTwo
  caseTwo = abs(SumOfOdd - SumOfeven);

  // Return maximum of caseOne and CaseTwo
  return max(caseOne, caseTwo);

}

// Drivers Code
int main()
{
  vector<int> arr{54, 32, 11, 23};

  // Function Call
  cout<<maxDiff(arr);

}
// This code is contributed by ipg2016107.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to count total number
// of bits present in a number
static int countBit(int n){
  return (int)((Math.log(n) / Math.log(2))+1);
}

// Function to count total
// set bits in a number
static int countSetBit(int n){

  // Stores the count
  // of set bits
  int ans = 0;

  while(n > 0){

    ans += (n & 1);

    // Right shift by 1
    n >>= 1;
  }

  // Return the final count
  return ans;
}

// Function to find maximum number
// by shifting two unequal bits
static int maximize(int n){

  // Count set bits in number n
  int bits = countBit(n);
  int setBits = countSetBit(n);
  int ans = 0;

  // Iterate the string bits
  for(int i = 0; i < bits; i++){

    if (i < setBits)
      ans |= 1;
    if(i != setBits - 1)
      ans <<= 1;

  }
  return ans;
}

// Function to find minimum number
// by shifting two unequal bits
static int minimize(int n){

  int setBits = countSetBit(n);
  int ans = 0;

  // Iterate the set bit
  for (int i = 0; i < setBits; i++){
    ans |= 1;
    if (i != setBits - 1)
      ans <<= 1;
  }
  return ans;
}

// Function to find the maximum difference
static int maxDiff(int[] arr){

  // Stores the maximum difference
  int caseOne = 0;

  // Stores the sum of elements
  // placed at odd positions
  int SumOfOdd = 0;

  // Stores the sum of elements
  // placed at even positions
  int SumOfeven = 0;

  // Traverse the array
  for(int i = 0; i < arr.length; i++){
    if ((i % 2) != 0)
      SumOfOdd += minimize(arr[i]);

    else
      SumOfeven += maximize(arr[i]);
  }

  // Update CaseOne
  caseOne = Math.abs(SumOfOdd - SumOfeven);

  // Stores the maximum difference
  int caseTwo = 0;

  // Assign value O
  SumOfOdd = 0;
  SumOfeven = 0;

  // Traverse the array
  for(int i = 0; i < arr.length; i++)
  {
    if ((i % 2) != 0)
      SumOfOdd += maximize(arr[i]);
    else
      SumOfeven += minimize(arr[i]);
  }

  // Update caseTwo
  caseTwo = Math.abs(SumOfOdd - SumOfeven);

  // Return maximum of caseOne and CaseTwo
  return Math.max(caseOne, caseTwo);

}

// Driver code
public static void main(String[] args)
{
    int[] arr = {54, 32, 11, 23};

    // Function Call
    System.out.println(maxDiff(arr));
}
}

// This code is contributed by souravghosh0416.
```

## 蟒蛇 3

```
# Python program for the above approach
import math

# Function to count total number
# of bits present in a number
def countBit(n):
    return int(math.log(n, 2))+1

# Function to count total
# set bits in a number
def countSetBit(n):

    # Stores the count
    # of set bits
    ans = 0

    while n:

        ans += n & 1

        # Right shift by 1
        n >>= 1

    # Return the final count
    return ans

# Function to find maximum number
# by shifting two unequal bits
def maximize(n):

    # Count set bits in number n
    bits = countBit(n)
    setBits = countSetBit(n)
    ans = 0

    # Iterate the string bits
    for i in range(bits):

        if i < setBits:
            ans |= 1
        if i != setBits - 1:
            ans <<= 1
    return ans

# Function to find minimum number
# by shifting two unequal bits
def minimize(n):

    setBits = countSetBit(n)
    ans = 0

    # Iterate the set bit
    for i in range(setBits):
        ans |= 1
        if i != setBits-1:
            ans <<= 1

    return ans

# Function to find the maximum difference
def maxDiff(arr):

    # Stores the maximum difference
    caseOne = 0

    # Stores the sum of elements
    # placed at odd positions
    SumOfOdd = 0

    # Stores the sum of elements
    # placed at even positions
    SumOfeven = 0

    # Traverse the array
    for i in range(len(arr)):
        if i % 2:
            SumOfOdd += minimize(arr[i])

        else:
            SumOfeven += maximize(arr[i])
    # Update CaseOne
    caseOne = abs(SumOfOdd - SumOfeven)

    # Stores the maximum difference
    caseTwo = 0

    # Assign value O
    SumOfOdd = 0
    SumOfeven = 0

    # Traverse the array
    for i in range(len(arr)):
        if i % 2:
            SumOfOdd += maximize(arr[i])
        else:
            SumOfeven += minimize(arr[i])
    # Update caseTwo
    caseTwo = abs(SumOfOdd - SumOfeven)

    # Return maximum of caseOne and CaseTwo
    return max(caseOne, caseTwo)

# Drivers Code
arr = [54, 32, 11, 23]

# Function Call
print(maxDiff(arr))
```

## C#

```
// C# program for the above approach
using System;
class GFG{

  // Function to count total number
  // of bits present in a number
  static int countBit(int n){
    return (int)((Math.Log(n) / Math.Log(2))+1);
  }

  // Function to count total
  // set bits in a number
  static int countSetBit(int n){

    // Stores the count
    // of set bits
    int ans = 0;

    while(n > 0){

      ans += (n & 1);

      // Right shift by 1
      n >>= 1;
    }

    // Return the final count
    return ans;
  }

  // Function to find maximum number
  // by shifting two unequal bits
  static int maximize(int n){

    // Count set bits in number n
    int bits = countBit(n);
    int setBits = countSetBit(n);
    int ans = 0;

    // Iterate the string bits
    for(int i = 0; i < bits; i++){

      if (i < setBits)
        ans |= 1;
      if(i != setBits - 1)
        ans <<= 1;

    }
    return ans;
  }

  // Function to find minimum number
  // by shifting two unequal bits
  static int minimize(int n){

    int setBits = countSetBit(n);
    int ans = 0;

    // Iterate the set bit
    for (int i = 0; i < setBits; i++){
      ans |= 1;
      if (i != setBits - 1)
        ans <<= 1;
    }
    return ans;
  }

  // Function to find the maximum difference
  static int maxDiff(int[] arr){

    // Stores the maximum difference
    int caseOne = 0;

    // Stores the sum of elements
    // placed at odd positions
    int SumOfOdd = 0;

    // Stores the sum of elements
    // placed at even positions
    int SumOfeven = 0;

    // Traverse the array
    for(int i = 0; i < arr.Length; i++){
      if ((i % 2) != 0)
        SumOfOdd += minimize(arr[i]);

      else
        SumOfeven += maximize(arr[i]);
    }

    // Update CaseOne
    caseOne = Math.Abs(SumOfOdd - SumOfeven);

    // Stores the maximum difference
    int caseTwo = 0;

    // Assign value O
    SumOfOdd = 0;
    SumOfeven = 0;

    // Traverse the array
    for(int i = 0; i < arr.Length; i++)
    {
      if ((i % 2) != 0)
        SumOfOdd += maximize(arr[i]);
      else
        SumOfeven += minimize(arr[i]);
    }

    // Update caseTwo
    caseTwo = Math.Abs(SumOfOdd - SumOfeven);

    // Return maximum of caseOne and CaseTwo
    return Math.Max(caseOne, caseTwo);

  }

  // Driver Code
  public static void Main(string[] args)
  {
    int[] arr = {54, 32, 11, 23};

    // Function Call
    Console.Write(maxDiff(arr));
  }
}

// This code is contributed by code_hunt.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to count total number
// of bits present in a number
function countBit(n){
  return parseInt(log2(n))+1;
}

// Function to count total
// set bits in a number
function countSetBit(n){

  // Stores the count
  // of set bits
  let ans = 0;

  while(n > 0){

    ans += (n & 1);

    // Right shift by 1
    n >>= 1;
  }

  // Return the final count
  return ans;
}

// Function to find maximum number
// by shifting two unequal bits
function maximize(n){

  // Count set bits in number n
  let bits = countBit(n);
  let setBits = countSetBit(n);
  let ans = 0;

  // Iterate the string bits
  for(let i = 0; i < bits; i++){

    if (i < setBits)
      ans |= 1;
    if(i != setBits - 1)
      ans <<= 1;

  }
  return ans;
}

// Function to find minimum number
// by shifting two unequal bits
function minimize(n){

  let setBits = countSetBit(n);
  let ans = 0;

  // Iterate the set bit
  for (let i = 0; i < setBits; i++){
    ans |= 1;
    if (i != setBits - 1)
      ans <<= 1;
  }
  return ans;
}

// Function to find the maximum difference
function maxDiff(arr){

  // Stores the maximum difference
  let caseOne = 0;

  // Stores the sum of elements
  // placed at odd positions
  let SumOfOdd = 0;

  // Stores the sum of elements
  // placed at even positions
  let SumOfeven = 0;

  // Traverse the array
  for(let i = 0; i < arr.length; i++){
    if (i % 2)
      SumOfOdd += minimize(arr[i]);

    else
      SumOfeven += maximize(arr[i]);
  }

  // Update CaseOne
  caseOne = Math.abs(SumOfOdd - SumOfeven);

  // Stores the maximum difference
  let caseTwo = 0;

  // Assign value O
  SumOfOdd = 0;
  SumOfeven = 0;

  // Traverse the array
  for(let i = 0; i < arr.length; i++)
  {
    if (i % 2)
      SumOfOdd += maximize(arr[i]);
    else
      SumOfeven += minimize(arr[i]);
  }

  // Update caseTwo
  caseTwo = Math.abs(SumOfOdd - SumOfeven);

  // Return maximum of caseOne and CaseTwo
  return Math.max(caseOne, caseTwo);

}

// Drivers Code
  let arr = [54, 32, 11, 23];

  // Function Call
  document.write(maxDiff(arr));

  // This code is contributed by rishavmahato348.
</script>
```

**Output:** 

```
58
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)