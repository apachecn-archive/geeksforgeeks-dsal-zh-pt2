# k 尺寸窗口中增加的子阵列和减少的子阵列数量之间的差异

> 原文:[https://www . geesforgeks . org/differences-number-递增-子数组-递减-子数组-k 大小-windows/](https://www.geeksforgeeks.org/differences-number-increasing-subarrays-decreasing-subarrays-k-sized-windows/)

给定一个整数和 k 的数组，找出大小为 k 的窗口中严格递增的子数组(大小大于 1)的数量和严格递减的子数组的数量之差。

**示例:**

```
Input : nums = {10, 20, 30, 15, 15}; 
           k = 3; 
Output : 3, 0, -1 
Explanation 
For the first window of [10, 20, 30], there are 
3 increasing subranges ([10, 20, 30], [10, 20], 
and [20, 30]) and 0 decreasing, so the answer 
is 3\. For the second window of [20, 30, 15], 
there is 1 increasing subrange and 1 decreasing, 
so the answer is 0\. For the third window of 
[20, 15, 15], there is 1 decreasing subrange 
and 0 increasing, so the answer is -1\. 
```

我们需要计算大小为 k 的每个窗口的递增和递减子阵列之间的差值。我们迭代数组，对于大小为 k 的每个窗口，我们计算递增和递减子阵列的数量，并将它们的差值插入输出数组。

1.  创建两个大小为 N 的数组，并将其初始化为零，然后创建输出数组。
2.  遍历数组
3.  计算递增子阵的数量
4.  计算递减子阵列
5.  在输出数组中插入递增和递减子数组的区别。

解的时间复杂度- O(n*k)
n =数组的大小
k =窗口大小

## C++

```
// CPP program to count the differences
#include <iostream>
#include <vector>
using namespace std;

// function to calculate the difference
vector<int> Diffs(vector<int> const& a, int k)
{
    vector<int> out;
    vector<int> inc, dec;

    // initializing inc and dec with 0 and resizing
    // equal to the size of main array
    inc.resize(a.size(), 0);
    dec.resize(a.size(), 0);

    int inc_sum = 0;
    int dec_sum = 0;

    // iterate through the array
    for (int i = 0; i < a.size(); ++i) {

        // finding number of increasing
        // subarrays in a window size k
        for (int j = i - 1; j >= 0 && j > i - k &&
                           a[j + 1] > a[j]; --j) {
            ++inc[j];
            ++inc_sum;
        }

        // Finding number of decreasing subarrays
        // in a window size k
        for (int j = i - 1; j >= 0 && j > i - k &&
                            a[j + 1] < a[j]; --j) {
            ++dec[j];
            ++dec_sum;
        }

        // calculate the difference
        if (i >= k - 1) {

            // if this is not the first window then
            // calculate inc_sum and dec_sum
            if (i >= k) {
                inc_sum -= inc[i - k];
                dec_sum -= dec[i - k];
            }

            // insert the difference in k size window
            // in the output vector
            out.push_back(inc_sum - dec_sum);
        }
    }
    return out;
}

// driver program
int main()
{
    vector<int> out = Diffs({ 10, 20, 30, 15, 15}, 3);
    for (int n : out)
        cout << n << ", ";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to count the differences
import java.util.*;

class GFG
{

// function to calculate the difference
static Vector<Integer> Diffs(int []a, int k)
{
    Vector<Integer> out = new Vector<Integer>();
    int [] inc, dec;

    // initializing inc and dec with 0 and resizing
    // equal to the size of main array
    inc = new int[a.length];
    dec = new int[a.length];

    int inc_sum = 0;
    int dec_sum = 0;

    // iterate through the array
    for (int i = 0; i < a.length; ++i)
    {

        // finding number of increasing
        // subarrays in a window size k
        for (int j = i - 1; j >= 0 && j > i - k &&
                        a[j + 1] > a[j]; --j)
        {
            ++inc[j];
            ++inc_sum;
        }

        // Finding number of decreasing subarrays
        // in a window size k
        for (int j = i - 1; j >= 0 && j > i - k &&
                            a[j + 1] < a[j]; --j)
        {
            ++dec[j];
            ++dec_sum;
        }

        // calculate the difference
        if (i >= k - 1)
        {

            // if this is not the first window then
            // calculate inc_sum and dec_sum
            if (i >= k)
            {
                inc_sum -= inc[i - k];
                dec_sum -= dec[i - k];
            }

            // insert the difference in k size window
            // in the output vector
            out.add(inc_sum - dec_sum);
        }
    }
    return out;
}

// Driver code
public static void main(String[] args)
{
    int []arr = { 10, 20, 30, 15, 15};
    Vector<Integer>out = Diffs(arr, 3);
    for (int n : out)
        System.out.print(n + ", ");
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to count the differences

# Function to calculate the difference
def Diffs(a, k):

    out, inc, dec = [], [0] * len(a), [0] * len(a)

    # Initializing inc and dec with 0 and
    # resizing equal to the size of main array
    inc_sum, dec_sum = 0, 0

    # Iterate through the array
    for i in range(0, len(a)):

        # Finding number of increasing
        # subarrays in a window size k
        j = i - 1
        while (j >= 0 and j > i - k and
                        a[j + 1] > a[j]):
            inc[j] += 1
            inc_sum += 1
            j -= 1

        # Finding number of decreasing
        # subarrays in a window size k
        j = i - 1
        while (j >= 0 and j > i - k and
                        a[j + 1] < a[j]):
            dec[j] += 1
            dec_sum += 1
            j -= 1

        # calculate the difference
        if i >= k - 1:

            # if this is not the first window then
            # calculate inc_sum and dec_sum
            if i >= k:
                inc_sum -= inc[i - k]
                dec_sum -= dec[i - k]

            # insert the difference in k size window
            # in the output vector
            out.append(inc_sum - dec_sum)

    return out

# Driver Code
if __name__ == "__main__":

    out = Diffs([10, 20, 30, 15, 15], 3)
    for n in out:
        print(n, end = ", ")

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to count the differences
using System;
using System.Collections.Generic;

class GFG
{

// function to calculate the difference
static List<int> Diffs(int []a, int k)
{
    List<int> Out = new List<int>();
    int [] inc, dec;

    // initializing inc and dec with 0 and resizing
    // equal to the size of main array
    inc = new int[a.Length];
    dec = new int[a.Length];

    int inc_sum = 0;
    int dec_sum = 0;

    // iterate through the array
    for (int i = 0; i < a.Length; ++i)
    {

        // finding number of increasing
        // subarrays in a window size k
        for (int j = i - 1; j >= 0 && j > i - k &&
                        a[j + 1] > a[j]; --j)
        {
            ++inc[j];
            ++inc_sum;
        }

        // Finding number of decreasing subarrays
        // in a window size k
        for (int j = i - 1; j >= 0 && j > i - k &&
                            a[j + 1] < a[j]; --j)
        {
            ++dec[j];
            ++dec_sum;
        }

        // calculate the difference
        if (i >= k - 1)
        {

            // if this is not the first window then
            // calculate inc_sum and dec_sum
            if (i >= k)
            {
                inc_sum -= inc[i - k];
                dec_sum -= dec[i - k];
            }

            // insert the difference in k size window
            // in the output vector
            Out.Add(inc_sum - dec_sum);
        }
    }
    return Out;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 10, 20, 30, 15, 15};
    List<int>Out = Diffs(arr, 3);
    foreach (int n in Out)
        Console.Write(n + ", ");
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Js program to count the differences

// function to calculate the difference
function Diffs( a, k)
{
    let out = [];
    let inc, dec;

    // initializing inc and dec with 0 and resizing
    // equal to the size of main array
    inc = [];
    dec = [];
    for(let i = 0;i<a.length;i++){
        inc.push(0);
        dec.push(0);
    }
    let inc_sum = 0;
    let dec_sum = 0;

    // iterate through the array
    for (let i = 0; i < a.length; ++i) {

        // finding number of increasing
        // subarrays in a window size k
        for (let j = i - 1; j >= 0 && j > i - k &&
                           a[j + 1] > a[j]; --j) {
            ++inc[j];
            ++inc_sum;
        }

        // Finding number of decreasing subarrays
        // in a window size k
        for (let j = i - 1; j >= 0 && j > i - k &&
                            a[j + 1] < a[j]; --j) {
            ++dec[j];
            ++dec_sum;
        }

        // calculate the difference
        if (i >= k - 1) {

            // if this is not the first window then
            // calculate inc_sum and dec_sum
            if (i >= k) {
                inc_sum -= inc[i - k];
                dec_sum -= dec[i - k];
            }

            // insert the difference in k size window
            // in the output vector
            out.push(inc_sum - dec_sum);
        }
    }
    return out;
}

// driver program
let out = Diffs([10, 20, 30, 15, 15], 3);
document.write(out)

// This code is contributed by rohitsingh07052.
</script>
```

**输出:**

```
3, 0, -1, 
```