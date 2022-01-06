# 长度为 N 的不同排列的计数，没有相似的相邻字符

> 原文:[https://www . geeksforgeeks . org/count-of-distinct-置换-length-n-无相似相邻字符/](https://www.geeksforgeeks.org/count-of-distinct-permutations-of-length-n-having-no-similar-adjacent-characters/)

给定一个整数 N，任务是计算长度 **N** 的不同排列的总数，仅由字母‘a’、‘b’和‘c’组成，允许重复，这样没有两个相邻的字符是相同的。

> **输入:** N = 3
> **输出:** 12
> **解释:**
> 满足要求条件的可能排列为{aba、abc、aca、acb、bac、bab、bca、bcb、cac、cab、cba、cbc}
> **输入:** N = 5
> **输出:** 48

**方法:**
需要进行以下观察来解决给定的问题:

1.  让我们把第一个字母固定为**‘a’**。
2.  现在，第二个<sup>字母可以是**【b】**也可以是**【c】**，这样就剩下两种方式来填充第二个字母。</sup>
3.  同样，第三个字母也可以用两种方式填充。如果 2 <sup>和</sup>位置的字符是‘b’，那么第三个字符可以是‘a’或‘c’。如果第二个<sup>和第三个</sup>位置的字符是“c”，第三个字符可以是“a”或“b”。
4.  同样，对于所有剩余的位置，取决于前一个位置的角色，总会有两种可能性。因此，如果‘a’占据第一个位置，可能排列的总数是**1 * 2 * 2 * 2…* 2 = 1 * 2<sup>N–1</sup>**。
5.  因此，考虑到第一个字符也可以是“b”或“c”，排列总数为**3 * 2<sup>N–1</sup>**。

以下是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the number of
// permutations possible
int countofPermutations(int N)
{
    return int(3 * pow(2, N - 1));
}

// Driver Code
int main()
{
    int N = 5;
    cout << countofPermutations(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
class GFG{

// Function to print the number of
// permutations possible
static int countofPermutations(int N)
{
    return (int)(3 * Math.pow(2, N - 1));
}

// Driver Code
public static void main(String[] args)
{
    int N = 5;
    System.out.print(countofPermutations(N));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to print the number of
# permutations possible
def countofPermutations(N):

    return int((3 * pow(2, N - 1)));

# Driver Code
if __name__ == '__main__':

    N = 5;
    print(countofPermutations(N));

# This code is contributed by amal kumar choubey
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to print the number of
// permutations possible
static int countofPermutations(int N)
{
    return (int)(3 * Math.Pow(2, N - 1));
}

// Driver Code
public static void Main(String[] args)
{
    int N = 5;

    Console.Write(countofPermutations(N));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript Program to implement
// the above approach

// Function to print the number of
// permutations possible
function countofPermutations(N)
{
    return parseInt(3 * Math.pow(2, N - 1));
}

// Driver Code
var N = 5;
document.write( countofPermutations(N));

</script>
```

**Output:** 

```
48
```

***时间复杂度:** O(logN)*
***辅助空间:** O(1)*