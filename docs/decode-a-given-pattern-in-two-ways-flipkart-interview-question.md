# 用两种方式解码给定的模式(Flipkart 面试问题)

> 原文:[https://www . geesforgeks . org/decode-双向给定模式-flipkart-面试-问题/](https://www.geeksforgeeks.org/decode-a-given-pattern-in-two-ways-flipkart-interview-question/)

发送方向接收方发送一个二进制字符串，同时对数字进行加密。给你一个加密形式的字符串。现在，接收器需要解码字符串，解码时有两种方法。

让加密的二进制字符串为 P[]，实际字符串为 S[]。

```
First, receiver starts with first character as 0; 
S[0] = 0 // First decoded bit is 1
Remaining bits or S[i]s are decoded using following formulas.
P[1] = S[1] + S[0] 
P[2] = S[2] + S[1] + S[0] 
P[3] = S[3] + S[2] + S[1] 
and so on ...

Second, Receiver starts with first character as 1; 
S[0] = 1 // First decoded bit is 1
Remaining bits or S[i]s are decoded using following formulas.
P[1] = S[1] + S[0]  
P[2] = S[2] + S[1] + S[0] 
P[3] = S[3] + S[2] + S[1] 
and so on ...
```

您需要打印两个字符串，这两个字符串是使用第一种和第二种技术的两个不同的求值结果生成的。如果任何字符串包含其他二进制数，则需要打印 NONE。

```
Input1; 0123210
Output: 0111000, NONE

Explanation for first output
S[0] = 0, 
P[1] = S[1] + S[0], S[1] = 1
P[2] = S[2] + S[1] + S[0], S[2] = 1
P[3] = S[3] + S[2] + S[1], S[3] = 1
P[4] = S[4] + S[3] + S[2], S[4] = 0 
P[5] = S[5] + S[4] + S[3], S[5] = 0
P[6] = S[6] + S[5] + S[4], S[6] = 0

Explanation for second output 
S[0] = 1,
P[1] = S[1] + S[0], S[1] = 0
P[2] = s[2] + S[1] + S[0], S[2] = 1
P[3] = S[3] + S[2] + S[1], S[3] = 2, not a binary character so NONE.
```

来源: [Flipkart 访谈|第 9 集(校内)](https://www.geeksforgeeks.org/flipkart-interview-set-9-campus/)
解决这个问题的思路很简单，我们跟踪最后两个解码位。当前位 S[i]总是可以通过从 P[i]中减去最后两个解码位来计算。

以下是上述想法的实现。我们将最后两个解码位存储在“第一”和“第二”中。

## C++

```
#include<iostream>
using namespace std;

// This function prints decoding of P[] with first decoded
// number as 'first'. If the decoded numbers contain anything
// other than 0, then "NONE" is printed
void decodeUtil(int P[], int n, int first)
{
    int S[n];  // array to store decoded bit pattern
    S[0] = first;  // The first number is always the given number

    int second = 0;  // Initialize second

    // Calculate all bits starting from second
    for (int i = 1; i < n; i++)
    {
        S[i] = P[i] -  first - second;
        if (S[i] != 1 && S[i] != 0)
        {
            cout << "NONE\n";
            return;
        }
        second = first;
        first = S[i];
    }

    // Print the output array
    for (int i = 0; i < n; i++)
       cout << S[i];
    cout << endl;
}

// This function decodes P[] using two techniques
// 1) Starts with 0 as first number 2) Starts 1 as first number
void decode(int P[], int n)
{
    decodeUtil(P, n, 0);
    decodeUtil(P, n, 1);
}

int main()
{
    int P[] = {0, 1, 2, 3, 2, 1, 0};
    int n = sizeof(P)/sizeof(P[0]);
    decode(P, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
class GFG{

// This function prints decoding of P[]
// with first decoded number as 'first'.
// If the decoded numbers contain anything
// other than 0, then "NONE" is printed
public static void decodeUtil(int P[], int n,
                              int first)
{
    // Array to store decoded bit pattern
    int S[] = new int[n];

    // The first number is always
    // the given number
    S[0] = first; 

    // Initialize second
    int second = 0; 

    // Calculate all bits starting
    // from second
    for(int i = 1; i < n; i++)
    {
        S[i] = P[i] - first-second;

        if (S[i] != 1 && S[i] != 0)
        {
            System.out.println("NONE");
            return;
        }
        second = first;
        first = S[i];
    }

    // Print the output array
    for(int i = 0; i < n; i++)
    {
        System.out.print(S[i]);
    }
    System.out.println();
}

// Driver code
public static void main(String []args)
{
    int P[] = { 0, 1, 2, 3, 2, 1, 0 };
    int n = P.length;

    // This function decodes P[] using
    // two techniques 1) Starts with 0
    // as first number 2) Starts 1 as
    // first number
    decodeUtil(P, n, 0);
    decodeUtil(P, n, 1);
}
}

// This code is contributed by avanitrachhadiya2155
```

## 蟒蛇 3

```
# This function prints decoding of P[] with
# first decoded number as 'first'. If the
# decoded numbers contain anything other
# than 0, then "NONE" is printed
def decodeUtil(P, n, first):
    S = [0 for i in range(n)]

    # array to store decoded bit pattern
    S[0] = first # The first number is
                 # always the given number

    second = 0

    # Initialize second

    # Calculate all bits starting from second
    for i in range(1, n, 1):
        S[i] = P[i] - first - second
        if (S[i] != 1 and S[i] != 0):
            print("NONE")
            return

        second = first
        first = S[i]

    # Print the output array
    for i in range(0, n, 1):
        print(S[i], end = "")
    print("\n", end = "")

# This function decodes P[] using
# two techniques
# 1) Starts with 0 as first number
# 2) Starts 1 as first number
def decode(P, n):
    decodeUtil(P, n, 0)
    decodeUtil(P, n, 1)

# Driver Code
if __name__ == '__main__':
    P = [0, 1, 2, 3, 2, 1, 0]
    n = len(P)
    decode(P, n)

# This code is contributed by
# Shashank_Sharma
```

## C#

```
using System;

class GFG{

// This function prints decoding of P[]
// with first decoded number as 'first'.
// If the decoded numbers contain anything
// other than 0, then "NONE" is printed
static void decodeUtil(int[] P, int n, int first)
{

    // Array to store decoded bit pattern
    int[] S = new int[n];

    // The first number is always
    // the given number
    S[0] = first;

    // Initialize second
    int second = 0; 

    // Calculate all bits starting
    // from second
    for(int i = 1; i < n; i++)
    {
        S[i] = P[i] - first - second;

        if (S[i] != 1 && S[i] != 0)
        {
            Console.WriteLine("NONE");
            return;
        }
        second = first;
        first = S[i];
    }

    // Print the output array
    for(int i = 0; i < n; i++)
    {
        Console.Write(S[i]);
    }
    Console.WriteLine();
}

// Driver code
static public void Main()
{
    int[] P = { 0, 1, 2, 3, 2, 1, 0 };
    int n = P.Length;

    // This function decodes P[] using
    // two techniques 1) Starts with 0
    // as first number 2) Starts 1 as
    // first number
    decodeUtil(P, n, 0);
    decodeUtil(P, n, 1);
}
}

// This code is contributed by rag2127
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php

// This function prints decoding
// of P[] with first decoded
// number as 'first'. If the
// decoded numbers contain anything
// other than 0, then "NONE" is printed
function decodeUtil($P, $n, $first)
{

    // The first number is always
    // the given number
    $S[0] = $first;

    // Initialize second
    $second = 0;

    // Calculate all bits starting
    // from second
    for ($i = 1; $i < $n; $i++)
    {
        $S[$i] = $P[$i] - $first - $second;
        if ($S[$i] != 1 && $S[$i] != 0)
        {
            echo "NONE\n";
            return;
        }
        $second = $first;
        $first = $S[$i];
    }

    // Print the output array
    for ($i = 0; $i < $n; $i++)
    echo $S[$i];
    echo "\n";
}

// This function decodes P[]
// using two techniques
// 1) Starts with 0 as first number
// 2) Starts 1 as first number
function decode($P, $n)
{
    decodeUtil($P, $n, 0);
    decodeUtil($P, $n, 1);
}

    // Driver Code
    $P=array (0, 1, 2, 3, 2, 1, 0);
    $n = sizeof($P);
    decode($P, $n);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
    // This function prints decoding of P[]
    // with first decoded number as 'first'.
    // If the decoded numbers contain anything
    // other than 0, then "NONE" is printed
    function decodeUtil(P, n, first)
    {

        // Array to store decoded bit pattern
        let S = new Array(n);

        // The first number is always
        // the given number
        S[0] = first;

        // Initialize second
        let second = 0;

        // Calculate all bits starting
        // from second
        for(let i = 1; i < n; i++)
        {
            S[i] = P[i] - first - second;

            if (S[i] != 1 && S[i] != 0)
            {
                document.write("NONE" + "</br>");
                return;
            }
            second = first;
            first = S[i];
        }

        // Print the output array
        for(let i = 0; i < n; i++)
        {
            document.write(S[i]);
        }
        document.write("</br>");
    }

    let P = [ 0, 1, 2, 3, 2, 1, 0 ];
    let n = P.length;

    // This function decodes P[] using
    // two techniques 1) Starts with 0
    // as first number 2) Starts 1 as
    // first number
    decodeUtil(P, n, 0);
    decodeUtil(P, n, 1);

</script>
```

**输出:**

```
0111000
NONE
```

时间复杂度:0(n)

本文由 **Abhishek** 供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。