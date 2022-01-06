# 最大化跳跃大小，从给定的起点到达所有给定点

> 原文:[https://www . geesforgeks . org/maximum-jump-size-to-reach-all-给定点-从给定的起点/](https://www.geeksforgeeks.org/maximize-jump-size-to-reach-all-given-points-from-given-starting-point/)

给定一个数组，**arr【】**由代表数字线上坐标的 **N** 整数和一个 **S** 整数组成。如果起始位置是 **S** ，至少找到一次访问所有坐标所需的最大跳跃尺寸。此外，允许双向跳跃。

**示例:**

> **输入:** arr[]={1，7，3，9，5，11}，S=3
> **输出:** 2
> **说明:**大小 2 的跳跃能够访问线上的所有坐标，方式如下:
> 跳跃-2:从 3 到达 1。
> 跳+2:从 1 到 3。
> 跳+2:从 3 达到 5。
> 跳+2:从 5 到 7。
> 跳+2:从 7 到 9。
> 跳+2:从 9 达到 11。
> 
> **输入:** arr[]={33，105，57}，S = 81
> T3】输出: 24

**逼近:**看完题可以观察到，线上所有相邻两点之间的所有差的[最大公约数](https://www.geeksforgeeks.org/gcd-two-array-numbers/)就是访问所有点所需的 Jump 的最大大小。因此，要解决这个问题，请遵循以下步骤:

1.  插入 **S** ，在数组 **arr** 中，然后排序。
2.  求数组中所有相邻对的差之间的 gcd**arr**。
3.  返回最终的 gcd 作为这个问题的答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum size of jump
// to reach all the coordinates
int minJumpSize(vector<int>& arr, int S)
{

    // Pushing S into the line
    arr.push_back(S);

    // Sorting arr, to get coordinates in
    // a sorted way
    sort(arr.begin(), arr.end());

    // Finding gcd between the differences of
    // all adjacent pairs
    int gcd = arr[1] - arr[0];
    for (int i = 1; i < arr.size(); i++) {
        gcd = __gcd(gcd,
                    __gcd(gcd,
                          arr[i] - arr[i - 1]));
    }

    return gcd;
}

// Driver Code
int main()
{
    vector<int> arr = { 1, 7, 3, 9, 5, 11 };
    int S = 3;

    cout << minJumpSize(arr, S);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.ArrayList;
import java.util.Collections;

class GFG {

    public static int __gcd(int a, int b) {
        if (b == 0)
            return a;
        return __gcd(b, a % b);
    }

    // Function to find the maximum size of jump
    // to reach all the coordinates
    public static int minJumpSize(int[] t_arr, int S) {
        ArrayList<Integer> arr = new ArrayList<Integer>();

        for (int x : t_arr) {
            arr.add(x);
        }

        // Pushing S into the line
        arr.add(S);

        // Sorting arr, to get coordinates in
        // a sorted way
        Collections.sort(arr);

        // Finding gcd between the differences of
        // all adjacent pairs
        int gcd = arr.get(1) - arr.get(0);
        for (int i = 1; i < arr.size(); i++) {
            gcd = __gcd(gcd, __gcd(gcd, arr.get(i) - arr.get(i - 1)));
        }

        return gcd;
    }

    // Driver Code
    public static void main(String args[]) {
        int[] arr = { 1, 7, 3, 9, 5, 11 };
        int S = 3;

        System.out.println(minJumpSize(arr, S));
    }
}

// This code is contributed by saurabh_jaiswal.
```

## 蟒蛇 3

```
# python program for the above approach
import math

# Function to find the maximum size of jump
# to reach all the coordinates
def minJumpSize(arr, S):

    # Pushing S into the line
    arr.append(S)

    # Sorting arr, to get coordinates in
    # a sorted way
    arr.sort()

    # Finding gcd between the differences of
    # all adjacent pairs
    gcd = arr[1] - arr[0]
    for i in range(1, len(arr)):
        gcd = math.gcd(gcd, math.gcd(gcd, arr[i] - arr[i - 1]))

    return gcd

# Driver Code
if __name__ == "__main__":

    arr = [1, 7, 3, 9, 5, 11]
    S = 3

    print(minJumpSize(arr, S))

# This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

    public static int __gcd(int a, int b) {
        if (b == 0)
            return a;
        return __gcd(b, a % b);
    }

    // Function to find the maximum size of jump
    // to reach all the coordinates
    public static int minJumpSize(int[] t_arr, int S) {
        List<int> arr = new List<int>();

        foreach (int x in t_arr) {
            arr.Add(x);
        }

        // Pushing S into the line
        arr.Add(S);

        // Sorting arr, to get coordinates in
        // a sorted way
        arr.Sort();

        // Finding gcd between the differences of
        // all adjacent pairs
        int gcd = arr[1] - arr[0];
        for (int i = 1; i < arr.Count; i++) {
            gcd = __gcd(gcd, __gcd(gcd, arr[(i)] - arr[(i - 1)]));
        }

        return gcd;
    }

// Driver Code
public static void Main()
{
    int[] arr = { 1, 7, 3, 9, 5, 11 };
    int S = 3;

    Console.WriteLine(minJumpSize(arr, S));
}
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        function __gcd(a, b) {
            // Everything divides 0
            if (a == 0)
                return b;
            if (b == 0)
                return a;

            // base case
            if (a == b)
                return a;

            // a is greater
            if (a > b)
                return __gcd(a - b, b);
            return __gcd(a, b - a);
        }

        // Function to find the maximum size of jump
        // to reach all the coordinates
        function minJumpSize(arr, S) {

            // Pushing S into the line
            arr.push(S);

            // Sorting arr, to get coordinates in
            // a sorted way
            arr.sort(function (a, b) { return a - b })

            // Finding gcd between the differences of
            // all adjacent pairs
            let gcd = arr[1] - arr[0];
            for (let i = 1; i < arr.length; i++) {
                gcd = __gcd(gcd,
                    __gcd(gcd,
                        arr[i] - arr[i - 1]));
            }

            return gcd;
        }

        // Driver Code

        let arr = [1, 7, 3, 9, 5, 11];
        let S = 3;

        document.write(minJumpSize(arr, S))

// This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
2
```

**时间复杂度:**O(NlogN)
T3】辅助空间: O(1)。