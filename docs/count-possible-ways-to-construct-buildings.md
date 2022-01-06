# 计算建造建筑物的可能方式

> 原文:[https://www . geesforgeks . org/count-可能的建筑建造方式/](https://www.geeksforgeeks.org/count-possible-ways-to-construct-buildings/)

给定一个输入的路段数，并且每个路段在道路两侧都有 2 个地块。找到所有可能的方法在地块内建造建筑，使任何两个建筑之间都有一个空间。

**示例:**

```
N = 1
Output = 4
Place a building on one side.
Place a building on other side
Do not place any building.
Place a building on both sides.

N = 3 
Output = 25
3 sections, which means possible ways for one side are 
BSS, BSB, SSS, SBS, SSB where B represents a building 
and S represents an empty space
Total possible ways are 25, because a way to place on 
one side can correspond to any of 5 ways on other side.

N = 4 
Output = 64
```

> [https://practice . geesforgeks . org/problems/count-可能的建造方式-buildings5007/1](https://practice.geeksforgeeks.org/problems/count-possible-ways-to-construct-buildings5007/1)

**我们强烈建议尽量减少你的浏览器，先自己试试这个**
我们可以把问题简化为先只计算一面。如果我们知道一方的结果，我们总是可以做结果的平方，得到双方的结果。

一个新的建筑可以放在一个剖面上，如果剖面刚好在它有空间之前的话。一个空间可以放在任何地方(前一段有没有建筑并不重要)。

```
Let countB(i) be count of possible ways with i sections
              ending with a building.
    countS(i) be count of possible ways with i sections
              ending with a space.

// A space can be added after a building or after a space.
countS(N) = countB(N-1) + countS(N-1)

// A building can only be added after a space.
countB[N] = countS(N-1)

// Result for one side is sum of the above two counts.
result1(N) = countS(N) + countB(N)

// Result for two sides is square of result1(N)
result2(N) = result1(N) * result1(N) 
```

以下是上述想法的实现。

## C++

```
// C++ program to count all possible way to construct buildings
#include<iostream>
using namespace std;

// Returns count of possible ways for N sections
int countWays(int N)
{
    // Base case
    if (N == 1)
        return 4;  // 2 for one side and 4 for two sides

    // countB is count of ways with a building at the end
    // countS is count of ways with a space at the end
    // prev_countB and prev_countS are previous values of
    // countB and countS respectively.

    // Initialize countB and countS for one side
    int countB=1, countS=1, prev_countB, prev_countS;

    // Use the above recursive formula for calculating
    // countB and countS using previous values
    for (int i=2; i<=N; i++)
    {
        prev_countB = countB;
        prev_countS = countS;

        countS = prev_countB + prev_countS;
        countB = prev_countS;
    }

    // Result for one side is sum of ways ending with building
    // and ending with space
    int result = countS + countB;

    // Result for 2 sides is square of result for one side
    return (result*result);
}

// Driver program
int main()
{
    int N = 3;
    cout << "Count of ways for " << N
         << " sections is " << countWays(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
class Building
{
    // Returns count of possible ways for N sections
    static int countWays(int N)
    {
        // Base case
        if (N == 1)
            return 4;  // 2 for one side and 4 for two sides

        // countB is count of ways with a building at the end
        // countS is count of ways with a space at the end
        // prev_countB and prev_countS are previous values of
        // countB and countS respectively.

        // Initialize countB and countS for one side
        int countB=1, countS=1, prev_countB, prev_countS;

        // Use the above recursive formula for calculating
        // countB and countS using previous values
        for (int i=2; i<=N; i++)
        {
            prev_countB = countB;
            prev_countS = countS;

            countS = prev_countB + prev_countS;
            countB = prev_countS;
        }

        // Result for one side is sum of ways ending with building
        // and ending with space
        int result = countS + countB;

        // Result for 2 sides is square of result for one side
        return (result*result);
    }

    public static void main(String args[])
    {
        int N = 3;
        System.out.println("Count of ways for "+ N+" sections is "
                                                        +countWays(N));
    }

}/* This code is contributed by Rajat Mishra */
```

## 蟒蛇 3

```
# Python 3 program to count all possible
# way to construct buildings

# Returns count of possible ways
# for N sections
def countWays(N) :

    # Base case
    if (N == 1) :
        # 2 for one side and 4
        # for two sides
        return 4

    # countB is count of ways with a
    # building at the end
    # countS is count of ways with a
    # space at the end
    # prev_countB and prev_countS are
    # previous values of
    # countB and countS respectively.

    # Initialize countB and countS
    # for one side
    countB=1
    countS=1

    # Use the above recursive formula
    # for calculating
    # countB and countS using previous values
    for i in range(2,N+1) :

        prev_countB = countB
        prev_countS = countS

        countS = prev_countB + prev_countS
        countB = prev_countS

    # Result for one side is sum of ways
    # ending with building
    # and ending with space
    result = countS + countB

    # Result for 2 sides is square of
    # result for one side
    return (result*result)

# Driver program
if __name__ == "__main__":

    N = 3
    print ("Count of ways for ", N
        ," sections is " ,countWays(N))

# This code is contributed by
# ChitraNayal
```

## C#

```
// C# program to count all
// possible way to construct
// buildings
using System;

class GFG
{
    // Returns count of possible
    // ways for N sections
    static int countWays(int N)
    {
        // Base case
        if (N == 1)

            // 2 for one side and
            // 4 for two sides
            return 4;

        // countB is count of ways
        // with a building at the
        // end, countS is count of
        // ways with a space at the
        // end, prev_countB and
        // prev_countS are previous
        // values of countB and countS
        // respectively.

        // Initialize countB and
        // countS for one side
        int countB = 1, countS = 1,
            prev_countB, prev_countS;

        // Use the above recursive
        // formula for calculating
        // countB and countS using
        // previous values
        for (int i = 2; i <= N; i++)
        {
            prev_countB = countB;
            prev_countS = countS;

            countS = prev_countB +
                     prev_countS;
            countB = prev_countS;
        }

        // Result for one side is sum
        // of ways ending with building
        // and ending with space
        int result = countS + countB;

        // Result for 2 sides is
        // square of result for
        // one side
        return (result * result);
    }

    // Driver Code
    public static void Main()
    {
        int N = 3;
        Console.Write(countWays(N));
    }

}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count all possible
// way to construct buildings

// Returns count of possible
// ways for N sections
function countWays( $N)
{

    // Base case
    if ($N == 1)

        // 2 for one side and
        // 4 for two sides
        return 4;

    // countB is count of ways
    // with a building at the end
    // countS is count of ways
    // with a space at the end
    // prev_countB and prev_countS
    // are previous values of
    // countB and countS respectively.

    // Initialize countB and
    // countS for one side
    $countB = 1; $countS = 1;
    $prev_countB; $prev_countS;

    // Use the above recursive
    // formula for calculating
    // countB and countS using
    // previous values
    for ($i = 2; $i <= $N; $i++)
    {
        $prev_countB = $countB;
        $prev_countS = $countS;

        $countS = $prev_countB +
                  $prev_countS;
        $countB = $prev_countS;
    }

    // Result for one side is
    // sum of ways ending with
    // building and ending with
    // space
    $result = $countS + $countB;

    // Result for 2 sides is square
    // of result for one side
    return ($result*$result);
}

    // Driver Code
    $N = 3;
    echo "Count of ways for " , $N
          , " sections is " , countWays($N);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
// Javascript program to count all
// possible way to construct buildings  

// Returns count of possible ways for N sections
function countWays(N)
{
    // Base case
    if (N == 1)

        // 2 for one side and
        // 4 for two sides
        return 4; 

    // countB is count of ways with a building at the end
    // countS is count of ways with a space at the end
    // prev_countB and prev_countS are previous values of
    // countB and countS respectively.

    // Initialize countB and countS for one side
    let countB = 1, countS = 1, prev_countB, prev_countS;

    // Use the above recursive formula for calculating
    // countB and countS using previous values
    for(let i = 2; i <= N; i++)
    {
        prev_countB = countB;
        prev_countS = countS;

        countS = prev_countB + prev_countS;
        countB = prev_countS;
    }

    // Result for one side is sum of
    // ways ending with building
    // and ending with space
    let result = countS + countB;

    // Result for 2 sides is square
    // of result for one side
    return (result*result);
}

// Driver code
N = 3;

document.write("Count of ways for " + N +
               " sections is " + countWays(N));

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output**

```
Count of ways for 3 sections is 25
```

**输出:**

```
Count of ways for 3 sections is 25
```

时间复杂度:O(N)
辅助空间:O(1)
算法范式:动态规划

**另一种思维方式:**(只在一边，因为对另一边来说是一样的)

让我们把建筑物想象成 **N** 的序列(因为两边有 N 个地块)**长度二进制字符串**(每个数字 0 或 1)，其中:

```
1 => Represents building has been made on the ith plot
0 => Represents building has not been made on the ith plot  
```

现在，如问题所述，我们必须找到在地块上没有连续建筑物的路的数量，在二进制字符串中，它可以被解释为，**我们需要找到在二进制字符串中没有连续 1 的路的数量(因为 1 代表正在建造的建筑物)**

**示例:**

```
N = 3 
Total Combinations = 2n = 23 = 8
This will contain some combination in there will be consecutive building, so we have to reject that

000 (No building) (Possible)
001 (Building on 3rd plot) (Possible)
010 (Building on 2nd plot) (Possible)
011 (Building on 2nd and 3rd plot) (Not Possible as there are consecutive buildings)
100 (Building on 1st plot) (Possible)
101 (Building on 1st and 3rd plot) (Possible)
110 (Building on 1st and 2nd plot) (Not Possible as there are consecutive buildings)
111 (Building on 1st, 2nd, 3rd plot) (Not Possible as there are consecutive buildings)

Total Possible Ways = 5 
These are only on one side, on other side it will also be same as there are N plots and same condition, so 

Answer = Total Possible Ways * Total Possible Ways = 25 
```

所以现在我们的问题简化为找到表示 N 长度二进制字符串的[种方法，这样它就没有连续的 1](https://www.geeksforgeeks.org/count-number-binary-strings-without-consecutive-1s/) ，这是一个非常标准的问题

**优化解:**
注意，以上解可以进一步优化。如果我们仔细观察结果，对于不同的值，我们可以注意到两边的结果是[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)的平方。
N = 1，结果= 4【一侧结果= 2】
N = 2，结果= 9【一侧结果= 3】
N = 3，结果= 25【一侧结果= 5】
N = 4，结果= 64【一侧结果= 8】
N = 5，结果= 169【一侧结果= 13】
…………。
…………………。
总的来说，我们可以说

```
  result(N) = fib(N+2)2

  fib(N) is a function that returns N'th 
 Fibonacci Number. 

```

因此，我们可以使用斐波那契数的 [O(LogN)实现来找到 O(LogN)时间内的路数。
本文由 **GOPINATH** 供稿。如果您发现任何不正确的地方，请写评论，或者您想分享更多关于上面讨论的主题的信息](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)