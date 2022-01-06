# 给定 N 个航班中每个航班预订的座位数

> 原文:[https://www . geeksforgeeks . org/每架给定 n 次航班的预订座位数/](https://www.geeksforgeeks.org/count-of-seats-booked-on-each-of-the-given-n-flights/)

给定表示航班数量的整数 **N** 和表示从航班 **a** 到航班 **b** *预订的 **K** 座位的表格 **{a，b，K}** 的每一行，任务是找出 **N** 中预订座位数量的顺序*

**示例:**

> **输入:**预订[][] = {{1，2，10}，{2，3，20}，{2，5，25}}
> **输出:**10 55 45 25
> 25**解释:**
> 最初，任何航班都没有预订座位。所以最终的顺序是{0，0，0，0，0}
> 预订 1 到 2 次航班的 10 个座位。序列变成{10，10，0，0，0}。
> 预订 2 至 3 次航班 20 个座位。序列变成{10，30，20，0，0}。
> 预订 2 至 5 次航班 25 个座位。序列变成{10，55，45，25，25}。
> 
> **输入:**预订[][] = {{1，3，100}，{2，6，100}，{3，4，100}}
> **输出:** 100 200 300 200 100 100

**天真的方法:**按照下面的步骤，用最简单的方法解决问题:

*   初始化一个大小为 **N** 的数组 **seq[]** ，以存储每趟航班分配的座位数。
*   [穿越阵](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)T2【预约】。
*   对于每个查询 **{a，b，K}** ，从索引 **a** 到 **b** 添加数组**seq【】**中的元素 **K** 。
*   完成以上步骤后，打印数组 **seq[]** 作为结果。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*

**高效方法:**对上述方法进行优化，思路是使用[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)的概念。按照以下步骤解决问题:

*   初始化一个大小为 **(N + 2)** 的数组 **seq[]** ，以存储所有分配的座位。
*   [穿越阵](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)T2【预约】。
*   对于每个查询 **{a，b，K}** ，将索引**(a–1)**处的数组 **seq[]** 增加 **K** ，将索引 **(b + 1)** 处的元素减少 **K** 。
*   对于结果序列，[求数组的前缀和](https://www.geeksforgeeks.org/prefix-sum-array-python-using-accumulate-function/) **seq[]** 。
*   完成以上步骤后，打印数组 **seq[]** 作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the total of the
// seats booked in each of the flights
void corpFlightBookings(
    vector<vector<int> >& Bookings,
    int N)
{
    // Stores the resultant sequence
    vector<int> res(N, 0);

    // Traverse the array
    for (int i = 0;
         i < Bookings.size(); i++) {

        // Store the first booked flight
        int l = Bookings[i][0];

        // Store the last booked flight
        int r = Bookings[i][1];

        // Store the total number of
        // seats booked in flights [l, r]
        int K = Bookings[i][2];

        // Add K to the flight L
        res[l - 1] = res[l - 1] + K;

        // Subtract K from flight
        // number R + 1
        if (r <= res.size() - 1)
            res[r] = (-K) + res[r];
    }

    // Find the prefix sum of the array
    for (int i = 1; i < res.size(); i++)
        res[i] = res[i] + res[i - 1];

    // Print the total number of seats
    // booked in each flight
    for (int i = 0; i < res.size(); i++) {
        cout << res[i] << " ";
    }
}

// Driver Code
int main()
{
    // Given list of bookings
    vector<vector<int> > bookings{ { 1, 3, 100 },
                                   { 2, 6, 100 },
                                   { 3, 4, 100 } };
    int N = 6;

    // Function Call
    corpFlightBookings(bookings, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG
{

// Function to find the total of the
// seats booked in each of the flights
static void corpFlightBookings(int [][]Bookings,
                               int N)
{

    // Stores the resultant sequence
    int res[] = new int[N];

    // Traverse the array
    for (int i = 0;
         i < Bookings.length; i++)
    {

        // Store the first booked flight
        int l = Bookings[i][0];

        // Store the last booked flight
        int r = Bookings[i][1];

        // Store the total number of
        // seats booked in flights [l, r]
        int K = Bookings[i][2];

        // Add K to the flight L
        res[l - 1] = res[l - 1] + K;

        // Subtract K from flight
        // number R + 1
        if (r <= res.length - 1)
            res[r] = (-K) + res[r];
    }

    // Find the prefix sum of the array
    for (int i = 1; i < res.length; i++)
        res[i] = res[i] + res[i - 1];

    // Print the total number of seats
    // booked in each flight
    for (int i = 0; i < res.length; i++)
    {
        System.out.print(res[i] + " ");
    }
}

// Driver Code
public static void main(String[] args)
{

    // Given list of bookings
    int bookings[][] = { { 1, 3, 100 },
                        { 2, 6, 100 },
                        { 3, 4, 100 } };
    int N = 6;

    // Function Call
    corpFlightBookings(bookings, N);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the total of the
# seats booked in each of the flights
def corpFlightBookings(Bookings, N):

    # Stores the resultant sequence
    res = [0] * N

    # Traverse the array
    for i in range(len(Bookings)):

        # Store the first booked flight
        l = Bookings[i][0]

        # Store the last booked flight
        r = Bookings[i][1]

        # Store the total number of
        # seats booked in flights [l, r]
        K = Bookings[i][2]

        # Add K to the flight L
        res[l - 1] = res[l - 1] + K

        # Subtract K from flight
        # number R + 1
        if (r <= len(res) - 1):
            res[r] = (-K) + res[r]

    # Find the prefix sum of the array
    for i in range(1, len(res)):
        res[i] = res[i] + res[i - 1]

    # Print total number of seats
    # booked in each flight
    for i in range(len(res)):
        print(res[i], end = " ")

# Driver Code
if __name__ == '__main__':

    # Given list of bookings
    bookings = [ [ 1, 3, 100 ],
               [ 2, 6, 100 ],
               [ 3, 4, 100 ] ]
    N = 6

    # Function Call
    corpFlightBookings(bookings, N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

// Function to find the total of the
// seats booked in each of the flights
static void corpFlightBookings(int [,]Bookings,
                               int N)
{

    // Stores the resultant sequence
    int []res = new int[N];

    // Traverse the array
    for (int i = 0;
         i < Bookings.GetLength(0); i++)
    {

        // Store the first booked flight
        int l = Bookings[i,0];

        // Store the last booked flight
        int r = Bookings[i,1];

        // Store the total number of
        // seats booked in flights [l, r]
        int K = Bookings[i,2];

        // Add K to the flight L
        res[l - 1] = res[l - 1] + K;

        // Subtract K from flight
        // number R + 1
        if (r <= res.Length - 1)
            res[r] = (-K) + res[r];
    }

    // Find the prefix sum of the array
    for (int i = 1; i < res.Length; i++)
        res[i] = res[i] + res[i - 1];

    // Print the total number of seats
    // booked in each flight
    for (int i = 0; i < res.Length; i++)
    {
        Console.Write(res[i] + " ");
    }
}

// Driver Code
public static void Main(String[] args)
{

    // Given list of bookings
    int [,]bookings = { { 1, 3, 100 },
                        { 2, 6, 100 },
                        { 3, 4, 100 } };
    int N = 6;

    // Function Call
    corpFlightBookings(bookings, N);
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the total of the
// seats booked in each of the flights
function corpFlightBookings(Bookings, N)
{

    // Stores the resultant sequence
    let res = new Array(N).fill(0);

    // Traverse the array
    for(let i = 0;
            i < Bookings.length; i++)
    {

        // Store the first booked flight
        let l = Bookings[i][0];

        // Store the last booked flight
        let r = Bookings[i][1];

        // Store the total number of
        // seats booked in flights [l, r]
        let K = Bookings[i][2];

        // Add K to the flight L
        res[l - 1] = res[l - 1] + K;

        // Subtract K from flight
        // number R + 1
        if (r <= res.length - 1)
            res[r] = (-K) + res[r];
    }

    // Find the prefix sum of the array
    for(let i = 1; i < res.length; i++)
        res[i] = res[i] + res[i - 1];

    // Print the total number of seats
    // booked in each flight
    for(let i = 0; i < res.length; i++)
    {
        document.write(res[i] + " ");
    }
}

// Driver Code

// Given list of bookings
let bookings = [ [ 1, 3, 100 ],
                 [ 2, 6, 100 ],
                 [ 3, 4, 100 ] ];
let N = 6;

// Function Call
corpFlightBookings(bookings, N);

// This code is contributed by splevel62

</script>
```

**Output:** 

```
100 200 300 200 100 100
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)