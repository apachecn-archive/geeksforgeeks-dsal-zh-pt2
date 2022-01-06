# 计算给定值所处的区间数

> 原文:[https://www . geeksforgeeks . org/count-给定值所在的区间数/](https://www.geeksforgeeks.org/count-the-number-of-intervals-in-which-a-given-value-lies/)

给定一个由整数间隔和 T2 组成的 2D 数组。每隔一段时间**【l】<sub>I</sub>，r<sub>I</sub>**，任务是检查 **V** 是否在 **li** 和 **ri** 之间，包括两者。任务是打印满足此条件的间隔计数。
**注:**1<= l<sub>I</sub><= r<sub>I</sub>
**例:**

> **输入** : arr[][] = {{1，10}、{5，10}、{15，25}、{7，12}、{20，25}}，V = 7
> **输出** : 3
> 对于 V = 7，它位于区间【1，10】、【5，10】和【7，12】中。所以，V 所在的区间数是 3。
> **输入** : arr[][] = {{3，7}，{2，2}，{2，8}，{7，11}}，V = 2
> **输出** : 2
> 对于 V = 2，它位于区间【2，2】和【2，8】之间。所以，V 所在的区间数是 2。

**方法-1:** 遍历整个数组检查每个区间**【里，日】**，如果 **V** 是否在区间内。如果是，则增加计数。
以下是上述方法的实现:

## C++

```
// CPP program to count the
// number of intervals in which
// a given value lies

#include<bits/stdc++.h>
using namespace std;

    // Function to count the
    // number of intervals in which
    // a given value lies
    int countIntervals(int arr[][2], int V, int N)
    {
        // Variable to store the count of intervals
        int count = 0;

        // Variables to store start and end of an interval
        int li, ri;

        for (int i = 0; i < N; i++)
       {
            li = arr[i][0];
            ri = arr[i][1];

            // Implies V lies in the interval
            // so increase count
            if (V >= li && V <= ri)
                count++;
        }
        return count;
    }

    // Driver code
    int main()
    {
        int arr[][2] = { { 1, 10 }, { 5, 10 },{ 15, 25 }, { 7, 12 }, { 20, 25 } };

        int V = 7;

        // length of the array
        int N = sizeof(arr)/sizeof(arr[0]);
        cout<<(countIntervals(arr, V, N))<<endl;
    }
//This code is contributed by
// Surendra_Gangywar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count the
// number of intervals in which
// a given value lies

import java.io.*;
import java.util.*;
import java.lang.*;

class GFG {

    // Function to count the
    // number of intervals in which
    // a given value lies
    static int countIntervals(int[][] arr, int V, int N)
    {
        // Variable to store the count of intervals
        int count = 0;

        // Variables to store start and end of an interval
        int li, ri;

        for (int i = 0; i < N; i++) {
            li = arr[i][0];
            ri = arr[i][1];

            // Implies V lies in the interval
            // so increase count
            if (V >= li && V <= ri)
                count++;
        }
        return count;
    }

    // Driver code
    public static void main(String args[])
    {
        int[][] arr = { { 1, 10 }, { 5, 10 },
         { 15, 25 }, { 7, 12 }, { 20, 25 } };

        int V = 7;

        // length of the array
        int N = arr.length;

        System.out.println(countIntervals(arr, V, N));
    }
}
```

## 蟒蛇 3

```
# Python 3 program to count the
# number of intervals in which
# a given value lies

# Function to count the
# number of intervals in which
# a given value lies
def countIntervals(arr, V, N) :

    # Variable to store the
    # count of intervals
    count = 0

    # Variables to store start and
    # end of an interval
    for i in range(N) :

        # Variables to store start and
        # end of an interval
        li = arr[i][0]
        ri = arr[i][1]

        # Implies V lies in the interval
        # so increase count
        if (V >= li and V <= ri) :
            count += 1

    return count;

# Driver Code
if __name__ == "__main__" :

    arr = [ [ 1, 10 ], [ 5, 10 ],
            [ 15, 25 ], [ 7, 12 ],
            [ 20, 25 ] ]

    V = 7

    # length of the array
    N = len(arr)

    print((countIntervals(arr, V, N)))

# This code is contributed by Ryuga
```

## C#

```
// C# program to count the
// number of intervals in which
// a given value lies
using System;

class GFG
{

// Function to count the
// number of intervals in which
// a given value lies
static int countIntervals(int[,] arr, int V, int N)
{
    // Variable to store the count of intervals
    int count = 0;

    // Variables to store start and end of an interval
    int li, ri;

    for (int i = 0; i < N ; i++)
    {
        li = arr[i, 0];
        ri = arr[i, 1];

        // Implies V lies in the interval
        // so increase count
        if (V >= li && V <= ri)
            count++;
    }
    return count;
}

// Driver code
public static void Main()
{
    int[,] arr = new int[,]{ { 1, 10 }, { 5, 10 },
    { 15, 25 }, { 7, 12 }, { 20, 25 } };

    int V = 7;

    // length of the array
    int N = arr.GetLength(0);

    Console.WriteLine(countIntervals(arr, V, N));
}
}

// This code is contributed by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count the number of
// intervals in which a given value lies

// Function to count the number of
// intervals in which a given value lies
function countIntervals($arr, $V, $N)
{
    // Variable to store the
    // count of intervals
    $count = 0;

    // Variables to store start
    // and end of an interval
    for ($i = 0; $i < $N; $i++)
    {
        $li = $arr[$i][0];
        $ri = $arr[$i][1];

        // Implies V lies in the interval
        // so increase count
        if ($V >= $li && $V <= $ri)
            $count++;
    }
    return $count;
}

// Driver code
$arr = array(array(1, 10),
             array(5, 10),
             array(15, 25),
             array(7, 12),
             array(20, 25));

$V = 7;

// length of the array
$N = sizeof($arr);

echo countIntervals($arr, $V, $N);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>
    // Javascript program to count the
    // number of intervals in which
    // a given value lies

    // Function to count the
    // number of intervals in which
    // a given value lies
    function countIntervals(arr, V, N)
    {

        // Variable to store the count of intervals
        let count = 0;

        // Variables to store start and end of an interval
        let li, ri;

        for (let i = 0; i < N; i++) {
            li = arr[i][0];
            ri = arr[i][1];

            // Implies V lies in the interval
            // so increase count
            if (V >= li && V <= ri)
                count++;
        }
        return count;
    }

    let arr = [ [ 1, 10 ], [ 5, 10 ],
                 [ 15, 25 ], [ 7, 12 ], [ 20, 25 ] ];

    let V = 7;

    // length of the array
    let N = arr.length;

    document.write(countIntervals(arr, V, N));

    // This code is contributed by decode2207.
</script>
```

**Output:** 

```
3
```

**方法-2(对查询有效):**使用一个频率数组来跟踪一个元素位于多少个给定的区间中。

1.  对于每个间隔[L，R]，将 freq[L]设为 freq[L] + 1，将 freq[R+1]设为 freq[R+1]–1，表示间隔的开始和结束。
2.  记录总的最小和最大间隔。
3.  从最小值到最大值，从其先前的元素构建频率阵列，即
    freq[I]= freq[I]+freq[I–1]。
4.  所需的间隔计数由 freq[V]给出。

以下是上述方法的实现:

## C++

```
// C++ program to count the
// number of intervals in which
// a given value lies
#include<bits/stdc++.h>
using namespace std;

const int MAX_VAL = 200000;

// Function to count the
// number of intervals in which
// a given value lies
int countIntervals(int arr[][2], int V, int N)
{
    // Variables to store overall minimum and
    // maximum of the intervals
    int min = INT_MAX;
    int max = INT_MIN;

    // Variables to store start and
    // end of an interval
    int li, ri;

    // Frequency array to keep track of
    // how many of the given intervals
    // an element lies in
    int freq[MAX_VAL];

    for (int i = 0; i < N; i++)
    {
        li = arr[i][0];
        freq[li] = freq[li] + 1;
        ri = arr[i][1];
        freq[ri + 1] = freq[ri + 1] - 1;

        if (li < min)
            min = li;
        if (ri > max)
            max = ri;
    }

    // Constructing the frequency array
    for (int i = min; i <= max; i++)
        freq[i] = freq[i] + freq[i - 1];

    return freq[V];
}

// Driver code
int main()
{
    int arr[5][2] = { { 1, 10 }, { 5, 10 },
                      { 15, 25 }, { 7, 12 },
                      { 20, 25 } };

    int V = 7;

    // length of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << (countIntervals(arr, V, N));
}

// This code is contributed by
// Surendra_Gangwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count the
// number of intervals in which
// a given value lies

import java.io.*;
import java.util.*;
import java.lang.*;

class GFG {

    static final int MAX_VAL = 200000;

    // Function to count the
    // number of intervals in which
    // a given value lies
    static int countIntervals(int[][] arr, int V, int N)
    {
        // Variables to store overall minimum and
        // maximum of the intervals
        int min = Integer.MAX_VALUE, max = Integer.MIN_VALUE;

        // Variables to store start and end of an interval
        int li, ri;

        // Frequency array to keep track of
        // how many of the given intervals an element lies in
        int[] freq = new int[MAX_VAL];

        for (int i = 0; i < N; i++) {
            li = arr[i][0];
            freq[li] = freq[li] + 1;
            ri = arr[i][1];
            freq[ri + 1] = freq[ri + 1] - 1;

            if (li < min)
                min = li;
            if (ri > max)
                max = ri;
        }

        // Constructing the frequency array
        for (int i = min; i <= max; i++)
            freq[i] = freq[i] + freq[i - 1];

        return freq[V];
    }

    // Driver code
    public static void main(String args[])
    {
        int[][] arr = { { 1, 10 }, { 5, 10 },
         { 15, 25 }, { 7, 12 }, { 20, 25 } };

        int V = 7;

        // length of the array
        int N = arr.length;

        System.out.println(countIntervals(arr, V, N));
    }
}
```

## 蟒蛇 3

```
# Python3 program to count the number of
# intervals in which a given value lies
MAX_VAL = 200000

# Function to count the number of
# intervals in which a given value lies
def countIntervals(arr, V, N):

    # Variables to store overall minimumimum
    # and maximumimum of the intervals
    minimum = float("inf")
    maximum = 0

    # Frequency array to keep track of
    # how many of the given intervals
    # an element lies in
    freq = [0] * (MAX_VAL)

    for i in range(0, N):
        li = arr[i][0]
        freq[li] = freq[li] + 1
        ri = arr[i][1]
        freq[ri + 1] = freq[ri + 1] - 1

        if li < minimum:
            minimum = li

        if ri > maximum:
            maximum = ri

    # Constructing the frequency array
    for i in range(minimum, maximum + 1):
        freq[i] = freq[i] + freq[i - 1]

    return freq[V]

# Driver Code
if __name__ == "__main__":

    arr = [[1, 10], [5, 10], [15, 25],
           [7, 12], [20, 25]]

    V = 7

    # length of the array
    N = len(arr)

    print(countIntervals(arr, V, N))

# This code is contributed
# by Rituraj Jain
```

## C#

```
// C# program to count the
// number of intervals in which
// a given value lies
using System;

class GFG {

    static  int MAX_VAL = 200000;

    // Function to count the
    // number of intervals in which
    // a given value lies
    static int countIntervals(int[,] arr, int V, int N)
    {
        // Variables to store overall minimum and
        // maximum of the intervals
        int min = int.MaxValue, max = int.MinValue;

        // Variables to store start and end of an interval
        int li, ri;

        // Frequency array to keep track of
        // how many of the given intervals an element lies in
        int[] freq = new int[MAX_VAL];

        for (int i = 0; i < N; i++) {
            li = arr[i,0];
            freq[li] = freq[li] + 1;
            ri = arr[i,1];
            freq[ri + 1] = freq[ri + 1] - 1;

            if (li < min)
                min = li;
            if (ri > max)
                max = ri;
        }

        // Constructing the frequency array
        for (int i = min; i <= max; i++)
            freq[i] = freq[i] + freq[i - 1];

        return freq[V];
    }

    // Driver code
    public static void Main()
    {
        int[,] arr = new int[,]{ { 1, 10 }, { 5, 10 },
        { 15, 25 }, { 7, 12 }, { 20, 25 } };

        int V = 7;

        // length of the array
        int N = arr.Length/arr.Rank;

        Console.WriteLine(countIntervals(arr, V, N));
    }
}
// this code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count the number of
// intervals in which a given value lies

$MAX_VAL = 200000;

// Function to count the number of
// intervals in which a given value lies
function countIntervals($arr, $V, $N)
{
    global $MAX_VAL;

    // Variables to store overall minimum
    // and maximum of the intervals
    $min = PHP_INT_MAX;
    $max = 0;

    // Variables to store start and
    // end of an interval
    $li = 0;
    $ri = 0;

    // Frequency array to keep track of
    // how many of the given intervals
    // an element lies in
    $freq = array_fill(0, $MAX_VAL, 0);

    for ($i = 0; $i < $N; $i++)
    {
        $li = $arr[$i][0];
        $freq[$li] = $freq[$li] + 1;
        $ri = $arr[$i][1];
        $freq[$ri + 1] = $freq[$ri + 1] - 1;

        if ($li < $min)
            $min = $li;
        if ($ri > $max)
            $max = $ri;
    }

    // Constructing the frequency array
    for ($i = $min; $i <= $max; $i++)
        $freq[$i] = $freq[$i] + $freq[$i - 1];

    return $freq[$V];
}

// Driver code
$arr = array(array( 1, 10 ),
             array( 5, 10 ),
             array( 15, 25 ),
             array( 7, 12 ),
             array( 20, 25 ));

$V = 7;

// length of the array
$N = count($arr);

echo (countIntervals($arr, $V, $N));

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
    // Javascript program to count the
    // number of intervals in which
    // a given value lies

    let MAX_VAL = 200000;

    // Function to count the
    // number of intervals in which
    // a given value lies
    function countIntervals(arr, V, N)
    {
        // Variables to store overall minimum and
        // maximum of the intervals
        let min = Number.MAX_VALUE, max = Number.MIN_VALUE;

        // Variables to store start and end of an interval
        let li, ri;

        // Frequency array to keep track of
        // how many of the given intervals an element lies in
        let freq = new Array(MAX_VAL);
        freq.fill(0);

        for (let i = 0; i < N; i++) {
            li = arr[i][0];
            freq[li] = freq[li] + 1;
            ri = arr[i][1];
            freq[ri + 1] = freq[ri + 1] - 1;

            if (li < min)
                min = li;
            if (ri > max)
                max = ri;
        }

        // Constructing the frequency array
        for (let i = min; i <= max; i++)
            freq[i] = freq[i] + freq[i - 1];

        return freq[V];
    }

    let arr = [ [ 1, 10 ], [ 5, 10 ],
                [ 15, 25 ], [ 7, 12 ], [ 20, 25 ] ];

    let V = 7;

    // length of the array
    let N = arr.length;

    document.write(countIntervals(arr, V, N));

// This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
3
```