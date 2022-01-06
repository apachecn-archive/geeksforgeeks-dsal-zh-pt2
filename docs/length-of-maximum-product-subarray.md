# 最大乘积子阵长度

> 原文:[https://www . geesforgeks . org/最大产品长度-subarray/](https://www.geeksforgeeks.org/length-of-maximum-product-subarray/)

给定一个大小为 **N** 的整数数组 **arr[]** ，任务是找到元素乘积为非零的最大长度子数组。。
**例:**

> **输入:**arr[]=【1，1，0，2，1，0，1，6，1】
> **输出:** 3
> **解释**
> 乘积不为零的可能子阵列有【1，1】、【2，1】和【1，6，1】
> 所以最大可能长度为 3。
> **输入:** arr[] = [0，1，2，1，3，0，0，1]
> **输出:** 4
> **解释**
> 乘积不为零的可能子阵列有【1，2，1，3】和【1】
> 所以最大可能长度为 4。

**进场:**

1.  保存输入数组中零的所有索引。
2.  最长的子阵列必须位于以下三个范围内:
    *   从零索引开始，在第一个零索引–1 处结束。
    *   位于两个零指数之间。
    *   从最后一个零索引+ 1 开始，到 N-1 结束。
3.  最后从所有情况中找出最大长度。

以下是上述方法的实现:

## C++

```
// C++ program to find maximum
// length subarray having non
// zero product
#include<bits/stdc++.h>
using namespace std;

// Function that returns the
// maximum length subarray
// having non zero product
void Maxlength(int arr[],int N)
{
    vector<int> zeroindex;
    int maxlen;

    // zeroindex list to store indexex
    // of zero
    for(int i = 0; i < N; i++)
    {
        if(arr[i] == 0)
            zeroindex.push_back(i);
    }

    if(zeroindex.size() == 0)
    {

        // If zeroindex list is empty
        // then Maxlength is as
        // size of array
        maxlen = N;
    }

    // If zeroindex list is not empty
    else
    {

        // for example list 1 1 0 0 1
        // is on indexex 0 1 2 3 4

        // first zero is on index 2
        // that means two numbers positive,
        // before index 2 so as
        // their product is positive to
        maxlen = zeroindex[0];

        // Checking for other indexex
        for(int i = 0;
                i < zeroindex.size() - 1; i++)
        {

            // If the difference is greater
            // than maxlen then maxlen
            // is updated
            if(zeroindex[i + 1]-
               zeroindex[i] - 1 > maxlen)
            {
                maxlen = zeroindex[i + 1] -
                         zeroindex[i] - 1;
            }
        }

        // To check the length of remaining
        // array after last zeroindex
        if(N - zeroindex[zeroindex.size() - 1] -
           1 > maxlen)
        {
            maxlen = N - zeroindex[
                         zeroindex.size() - 1] - 1;
        }
    }
    cout << maxlen << endl;
}

// Driver Code
int main()
{
    int N = 9;
    int arr[] = {7, 1, 0, 1, 2, 0, 9, 2, 1};

    Maxlength(arr, N);
}

// This code is contributed by Surendra_Gangwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum
// length subarray having non
// zero product
import java.util.*;

class GFG{

// Function that returns the
// maximum length subarray
// having non zero product
static void Maxlength(int arr[],int N)
{
    Vector<Integer> zeroindex = new Vector<Integer>();

    int maxlen;

    // zeroindex list to store indexex
    // of zero
    for(int i = 0; i < N; i++)
    {
        if (arr[i] == 0)
            zeroindex.add (i);
    }

    if (zeroindex.size() == 0)
    {

        // If zeroindex list is empty
        // then Maxlength is as
        // size of array
        maxlen = N;
    }

    // If zeroindex list is not empty
    else
    {

        // for example list 1 1 0 0 1
        // is on indexex 0 1 2 3 4

        // first zero is on index 2
        // that means two numbers positive,
        // before index 2 so as
        // their product is positive to
        maxlen = (int)zeroindex.get(0);

        // Checking for other indexex
        for(int i = 0;
                i < zeroindex.size() - 1; i++)
        {

            // If the difference is greater
            // than maxlen then maxlen
            // is updated
            if ((int)zeroindex.get(i + 1) -
                (int)zeroindex.get(i) - 1 > maxlen)
            {
                maxlen = (int)zeroindex.get(i + 1) -
                         (int)zeroindex.get(i) - 1;
            }
        }

        // To check the length of remaining
        // array after last zeroindex
        if (N - (int)zeroindex.get(
                     zeroindex.size() - 1) -
                                    1 > maxlen)
        {
            maxlen = N - (int)zeroindex.get(
                              zeroindex.size() - 1) - 1;
        }
    }
    System.out.println(maxlen);
}

// Driver code
public static void main(String args[])
{
    int N = 9;
    int arr[] = { 7, 1, 0, 1, 2, 0, 9, 2, 1 };

    Maxlength(arr, N);
}
}

// This code is contributed by amreshkumar3
```

## 蟒蛇 3

```
# Python3 program to find
# maximum length subarray
# having non zero product

# function that returns the
# maximum length subarray
# having non zero product
def Maxlength(arr, N):

    zeroindex =[]

    # zeroindex list to store indexex
    # of zero
    for i in range(N):
        if(arr[i] == 0):
            zeroindex.append(i)

    if(len(zeroindex) == 0):
        # if zeroindex list is empty
        # then Maxlength is as
        # size of array
        maxlen = N
    # if zeroindex list is not empty
    else:
        # for example list 1 1 0 0 1
        # is on indexex 0 1 2 3 4

        # first zero is on index 2
        # that means two numbers positive,
        # before index 2 so as
        # their product is positive to

        maxlen = zeroindex[0]

        # checking for other indexex
        for i in range(0, len(zeroindex)-1):

            # if the difference is greater
            # than maxlen then maxlen
            # is updated
            if(zeroindex[i + 1]\
               - zeroindex[i] - 1\
               > maxlen):
                maxlen = zeroindex[i + 1]\
                         - zeroindex[i] - 1

        # to check the length of remaining
        # array after last zeroindex
        if(N - zeroindex[len(zeroindex) - 1]\
                                 - 1 > maxlen):
            maxlen = N\
             - zeroindex[len(zeroindex) - 1] - 1

    print(maxlen)

# Driver Code
if __name__ == "__main__":
    N = 9
    arr = [7, 1, 0, 1, 2, 0, 9, 2, 1]
    Maxlength(arr, N)
```

## C#

```
// C# program to find maximum
// length subarray having non
// zero product
using System;
using System.Collections.Generic;

class GFG{

// Function that returns the
// maximum length subarray
// having non zero product
static void Maxlength(int []arr,int N)
{
    int[] zeroindex = new int[20000];
    int maxlen;

    // zeroindex list to store indexex
    // of zero
    int size = 0;
    for(int i = 0; i < N; i++)
    {
        if (arr[i] == 0)
            zeroindex[size++] = i;
    }

    if (size == 0)
    {

        // If zeroindex list is empty
        // then Maxlength is as
        // size of array
        maxlen = N;
    }

    // If zeroindex list is not empty
    else
    {

        // for example list 1 1 0 0 1
        // is on indexex 0 1 2 3 4

        // first zero is on index 2
        // that means two numbers positive,
        // before index 2 so as
        // their product is positive to
        maxlen = zeroindex[0];

        // Checking for other indexex
        for(int i = 0; i < size; i++)
        {

            // If the difference is greater
            // than maxlen then maxlen
            // is updated
            if (zeroindex[i + 1]-
                zeroindex[i] - 1 > maxlen)
            {
                maxlen = zeroindex[i + 1] -
                         zeroindex[i] - 1;
            }
        }

        // To check the length of remaining
        // array after last zeroindex
        if (N - zeroindex[size - 1] - 1 > maxlen)
        {
            maxlen = N - zeroindex[size - 1] - 1;
        }
    }
    Console.WriteLine(maxlen);
}

// Driver code
public static void Main()
{
    int N = 9;
    int []arr = { 7, 1, 0, 1, 2, 0, 9, 2, 1 };

    Maxlength(arr, N);
}
}

// This code is contributed by amreshkumar3
```

## java 描述语言

```
<script>
// Javascript program to find maximum
// length subarray having non
// zero product

// Function that returns the
// maximum length subarray
// having non zero product
function Maxlength(arr, N)
{
    let zeroindex = Array.from({length: 20000}, (_, i) => 0);
    let maxlen;

    // zeroindex list to store indexex
    // of zero
    let size = 0;
    for(let i = 0; i < N; i++)
    {
        if (arr[i] == 0)
            zeroindex[size++] = i;
    }

    if (size == 0)
    {

        // If zeroindex list is empty
        // then Maxlength is as
        // size of array
        maxlen = N;
    }

    // If zeroindex list is not empty
    else
    {

        // for example list 1 1 0 0 1
        // is on indexex 0 1 2 3 4

        // first zero is on index 2
        // that means two numbers positive,
        // before index 2 so as
        // their product is positive to
        maxlen = zeroindex[0];

        // Checking for other indexex
        for(let i = 0; i < size; i++)
        {

            // If the difference is greater
            // than maxlen then maxlen
            // is updated
            if (zeroindex[i + 1]-
                zeroindex[i] - 1 > maxlen)
            {
                maxlen = zeroindex[i + 1] -
                         zeroindex[i] - 1;
            }
        }

        // To check the length of remaining
        // array after last zeroindex
        if (N - zeroindex[size - 1] - 1 > maxlen)
        {
            maxlen = N - zeroindex[size - 1] - 1;
        }
    }
    document.write(maxlen);
}

  // Driver Code

    let N = 9;
    let arr = [ 7, 1, 0, 1, 2, 0, 9, 2, 1 ];

    Maxlength(arr, N);

</script>
```

**Output:** 

```
3
```

**时间复杂度:**O(N)
T3】辅助空间: O (N)