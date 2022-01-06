# 计数数组中的总设置位

> 原文:[https://www . geesforgeks . org/count-total-set-bit in a array/](https://www.geeksforgeeks.org/count-total-set-bits-in-an-array/)

给定一个数组 **arr** ，任务是计算该数组 **arr** 的所有数字中的设置位的总数。

**示例:**

> **输入:** arr[] = {1，2，5，7}
> **输出:** 7
> **说明:**在{1，2，5，7}中设置的位数分别为{1，1，2，3}
> 
> **输入:** arr[] = {0，4，9，8}
> **输出:** 4

**方法:**按照以下步骤解决这个问题:

1.  创建一个变量 **cnt** 来存储答案，并用 **0** 初始化。
2.  遍历数组的每个元素 **arr** 。
3.  现在对于每个元素，假设 **x** ，当它大于 **0** 时运行一个循环。
4.  使用 **(x & 1)** 提取 **x** 的最后一位，然后右移 **x** 一位。
5.  返回 **cnt** 作为这个问题的答案。

下面是上述方法的实现:

## C++

```
// C++ code for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count the total number of set bits
// in an array of integers
int totalSetBits(vector<int>& arr)
{
    int cnt = 0;
    for (auto x : arr) {

        // While x is greater than 0
        while (x > 0) {

            // Adding last bit to cnt
            cnt += (x & 1);

            // Right shifting x by a single bit
            x >>= 1;
        }
    }
    return cnt;
}

// Driver Code
int main()
{
    vector<int> arr = { 1, 2, 5, 7 };
    cout << totalSetBits(arr);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
import java.util.*;

class GFG{

// Function to count the total number of set bits
// in an array of integers
static int totalSetBits(int[] arr)
{
    int cnt = 0;
    for (int x : arr) {

        // While x is greater than 0
        while (x > 0) {

            // Adding last bit to cnt
            cnt += (x & 1);

            // Right shifting x by a single bit
            x >>= 1;
        }
    }
    return cnt;
}

// Driver Code
public static void main(String[] args)
{
    int[] arr = { 1, 2, 5, 7 };
    System.out.print(totalSetBits(arr));
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# python code for the above approach

# Function to count the total number of set bits
# in an array of integers
def totalSetBits(arr):

    cnt = 0
    for x in arr:

        # While x is greater than 0
        while (x > 0):

            # Adding last bit to cnt
            cnt += (x & 1)

            # Right shifting x by a single bit
            x >>= 1
    return cnt

# Driver Code
if __name__ == "__main__":

    arr = [1, 2, 5, 7]
    print(totalSetBits(arr))

# This code is contributed by rakeshsahni
```

## C#

```
// C# code for the above approach
using System;

class GFG {

    // Function to count the total number of set bits
    // in an array of integers
    static int totalSetBits(int[] arr)
    {
        int cnt = 0;
        for (int x = 0; x < arr.Length; x++) {

            // While x is greater than 0
            while (arr[x] > 0) {

                // Adding last bit to cnt
                cnt += (arr[x] & 1);

                // Right shifting x by a single bit
                arr[x] >>= 1;
            }
        }
        return cnt;
    }

    // Driver Code
    public static void Main(string[] args)
    {
        int[] arr = { 1, 2, 5, 7 };
        Console.WriteLine(totalSetBits(arr));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

// JavaScript code for the above approach

// Function to count the total number of set bits
// in an array of integers
function totalSetBits(arr)
{
    let cnt = 0;
    for(let x of arr)
    {

        // While x is greater than 0
        while (x > 0)
        {

            // Adding last bit to cnt
            cnt += (x & 1);

            // Right shifting x by a single bit
            x >>= 1;
        }
    }
    return cnt;
}

// Driver Code
let arr = [ 1, 2, 5, 7 ];

document.write(totalSetBits(arr));

// This code is contributed by Potta Lokesh

</script>
```

**Output**

```
7
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)