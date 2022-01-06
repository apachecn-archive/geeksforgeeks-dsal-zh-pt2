# 保证 M 个红苹果需要从树上采集的最少苹果数量

> 原文:[https://www . geeksforgeeks . org/从树上收集的最低数量的苹果-保证-m-red-apple/](https://www.geeksforgeeks.org/minimum-number-of-apples-to-be-collected-from-trees-to-guarantee-m-red-apples/)

在四个方向(东、西、北、南)有不同种类的苹果树，它们可以同时生长红苹果和绿苹果，使得每棵树都精确地生长 K 个苹果，其方式如下:

*   **N**–北边没有红苹果的树数。
*   **S**–南边没有青苹果的树数。
*   **W**–西部的树数有一些红苹果。
*   **E**–东部的树木数量有一些青苹果。

然而，苹果的颜色在屋外是分不清的。所以，任务是找到要从树上收集的最小数量的苹果，以保证 M 个红苹果。如果不可能，请打印-1。

**示例:**

> **输入:** M = 10，K = 15，N = 0，S = 1，W = 0，E = 0
> **输出:** 10
> **说明:**它只是从第一棵南树上得到 10 个苹果
> 
> **输入:** M = 10，K = 15，N = 3，S = 0，W = 1，E = 0
> **输出:** -1
> **说明:**南、北、东没有红苹果。但是在西方，至少有一个红苹果，总树数是 1，所以，保证红苹果的总数是 1 * 1 = 1，小于 m

**进场:**南方的每个苹果都保证是红色的。首先，拿一个南方的苹果。在东方和西方，每棵树上至少有一个红苹果。这就是为什么，为了保证，人们认为东西两边每棵树上只有一个红苹果。北方没有红苹果，所以，忽略这一点。按照以下步骤解决问题:

*   [如果](https://www.geeksforgeeks.org/python-if-else/) **M** 小于等于 **S*K** 则打印**M**
*   [否则如果](https://www.geeksforgeeks.org/python-if-else/) **M** 小于等于 **S*K+E+W** 则打印 **S*K + (M-S*K) * K**
*   [否则](https://www.geeksforgeeks.org/python-if-else/)打印 **-1。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to minimum no. of apples
int minApples(int M,int K,int N,int S,int W,int E){
    // If we get all required apple
    // from South
    if(M <= S * K)
        return M;

    // If we required trees at
    // East and West
    else if(M <= S * K + E + W)
        return S * K + (M-S * K) * K;

    // If we doesn't have enough
    // red apples
    else
        return -1;

}

// Driver Code
int main(){

    // No. of red apple for gift
    int M = 10;

    // No. of red apple in each tree
    int K = 15;

    // No. of tree in North
    int N = 0;

    // No. of tree in South
    int S = 1;

    // No. of tree in West
    int W = 0;

    // No. of tree in East
    int E = 0;

    // Function Call
    int ans = minApples(M,K,N,S,W,E);
    cout<<ans<<endl;

}

// This code is contributed by ipg2016107.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
class GFG {

// Function to minimum no. of apples
static int minApples(int M,int K,int N,int S,int W,int E)
{

    // If we get all required apple
    // from South
    if(M <= S * K)
        return M;

    // If we required trees at
    // East and West
    else if(M <= S * K + E + W)
        return S * K + (M-S * K) * K;

    // If we doesn't have enough
    // red apples
    else
        return -1;
}

// Driver code
public static void main(String[] args)
{
    // No. of red apple for gift
    int M = 10;

    // No. of red apple in each tree
    int K = 15;

    // No. of tree in North
    int N = 0;

    // No. of tree in South
    int S = 1;

    // No. of tree in West
    int W = 0;

    // No. of tree in East
    int E = 0;

    // Function Call
    int ans = minApples(M,K,N,S,W,E);
    System.out.println(ans);
}
}

// This code is contributed by code_hunt.
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to minimum no. of apples
def minApples():

    # If we get all required apple
    # from South
    if M <= S * K:
        return M

    # If we required trees at
    # East and West
    elif M <= S * K + E + W:
        return S * K + (M-S * K) * K

    # If we doesn't have enough
    # red apples
    else:
        return -1

# Driver Code
if __name__ == "__main__":

    # No. of red apple for gift
    M = 10

    # No. of red apple in each tree
    K = 15

    # No. of tree in North
    N = 0

    # No. of tree in South
    S = 1

    # No. of tree in West
    W = 0

    # No. of tree in East
    E = 0

    # Function Call
    ans = minApples()
    print(ans)
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to minimum no. of apples
static int minApples(int M, int K, int N,
                     int S, int W, int E)
{

    // If we get all required apple
    // from South
    if (M <= S * K)
        return M;

    // If we required trees at
    // East and West
    else if (M <= S * K + E + W)
        return S * K + (M - S * K) * K;

    // If we doesn't have enough
    // red apples
    else
        return -1;
}

// Driver code
public static void Main(String[] args)
{

    // No. of red apple for gift
    int M = 10;

    // No. of red apple in each tree
    int K = 15;

    // No. of tree in North
    int N = 0;

    // No. of tree in South
    int S = 1;

    // No. of tree in West
    int W = 0;

    // No. of tree in East
    int E = 0;

    // Function Call
    int ans = minApples(M, K, N, S, W, E);
    Console.Write(ans);
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

      // JavaScript program for the above approach;

      // Function to minimum no. of apples
      function minApples() {

          // If we get all required apple
          // from South
          if (M <= S * K)
              return M;

          // If we required trees at
          // East and West
          else if (M <= S * K + E + W)
              return S * K + (M - S * K) * K;

          // If we doesn't have enough
          // red apples
          else
              return -1;
      }

      // Driver Code

      // No. of red apple for gift
      M = 10

      // No. of red apple in each tree
      K = 15

      // No. of tree in North
      N = 0

      // No. of tree in South
      S = 1

      // No. of tree in West
      W = 0

      // No. of tree in East
      E = 0

      // Function Call
      ans = minApples()
      document.write(ans);

 // This code is contributed by Potta Lokesh
  </script>
```

**Output**

```
10
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)