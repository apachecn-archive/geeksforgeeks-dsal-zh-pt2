# 要附加的最小数字，使得数组的平均值等于 1

> 原文:[https://www . geeksforgeeks . org/要追加的最小数字-数组平均值等于 1/](https://www.geeksforgeeks.org/minimum-numbers-to-be-appended-such-that-mean-of-array-is-equal-to-1/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[ ]** ，任务是找到使数组 **arr[ ]** 的平均值等于 1 所需的最小操作数。在一个操作中，可以在数组的末尾追加一个非负数。

**示例:**

> **输入:** N = 3，arr = {1，1，1}
> **输出:** 0
> **说明:**
> 可以看出 arr[ ]、(1+1+1)/3 = 1 的意思，
> 因此需要 0 次运算才能使阵列良好。
> 
> **输入:** N = 4，arr = {8，4，6，2}
> **输出:** 16
> **解释:**
> 由于给定数组的和为 20，元素个数为 4。
> 因此我们需要在数组的最后追加 16 个零，使其均值等于 1。

**方法:**上述问题可以借助数组和和以及数组中元素的个数，即 N 来解决，如下例:

*   如果数组和小于 N，它们之间的差可以附加到数组中，因此需要 1 次运算。
*   如果数组和等于 N，则平均值等于 1，因此需要 0 次运算。
*   如果数组和大于 N，则 0 可以在数组中追加(arraySum–N)次。因此，需要(arraySum–N)个操作。

按照以下步骤解决问题:

*   [**求数组 arr[ ]的和，比如 sum_arr。**T3】](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)
*   如果 **sum_arr > = N** ，则打印**sum _ arr–N**。
*   否则打印 **1** 。

下面是上述方法的实现。

## C++

```
// C++ program for above approach
#include<bits/stdc++.h>
using namespace std;

// Function to calculate minimum
// Number of operations
void minumumOperation(int N, int arr[]){

// Storing sum of array arr[]
    int sum_arr =  0;
    sum_arr = accumulate(arr, arr+N, sum_arr);

    if(sum_arr >= N)
      cout<<sum_arr-N<<endl;

    else
        cout<<1<<endl;
}

// Driver Code
int main(){
   int N = 4;
   int arr[] = {8, 4, 6, 2};

// Function Call
   minumumOperation(N, arr);
}

// This code is contributed by ipg2016107.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
class GFG
{

// Function to calculate minimum
// Number of operations
static void minumumOperation(int N, int arr[])
{

// Storing sum of array arr[]
    int sum_arr =  0;
    for(int i = 0; i < N; i++)
    {
        sum_arr += arr[i];
    }

    if(sum_arr >= N)
      System.out.println(sum_arr - N);

    else
        System.out.println("1");
}
// Driver Code
public static void main(String[] args)
{
     int N = 4;
   int arr[] = {8, 4, 6, 2};

// Function Call
   minumumOperation(N, arr);
}
}

// This code is contributed by dwivediyash
```

## 蟒蛇 3

```
# Python program for above approach

# Function to calculate minimum
# Number of operations
def minumumOperation(N, arr):

    # Storing sum of array arr[]
    sum_arr = sum(arr)

    if sum_arr >= N:
        print(sum_arr-N)

    else:
        print(1)

# Driver Code
N = 4
arr = [8, 4, 6, 2]

# Function Call
minumumOperation(N, arr)
```

## C#

```
// C# program for above approach
using System;
class GFG
{

  // Function to calculate minimum
  // Number of operations
  static void minumumOperation(int N, int []arr){

    // Storing sum of array arr[]
    int sum_arr =  0;
    for (int i = 0; i < N; i++) {
      sum_arr = sum_arr + arr[i];
    }

    if(sum_arr >= N)
      Console.Write(sum_arr-N);

    else
      Console.Write(1);
  }

  // Driver Code
  static public void Main (){
    int N = 4;
    int []arr = {8, 4, 6, 2};

    // Function Call
    minumumOperation(N, arr);
  }
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to calculate minimum
        // Number of operations
        function minumumOperation(N, arr) {

            // Storing sum of array arr[]
            let sum_arr = 0;
            for (let i = 0; i < N; i++) {
                sum_arr = sum_arr + arr[i];
            }

            if (sum_arr >= N)
                document.write(sum_arr - N + "<br>");

            else
                document.write(1 + "<br>");
        }

        // Driver Code

        let N = 4;
        let arr = [8, 4, 6, 2];

        // Function Call
        minumumOperation(N, arr);

// This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
16
```

***时间复杂度:*** O(N)
***辅助空间:*** O(1)