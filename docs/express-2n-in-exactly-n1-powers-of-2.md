# 用 2 的 N+1 次方

表示 2^N

> 原文:[https://www . geesforgeks . org/express-2n-in-just-n1-2 次方/](https://www.geeksforgeeks.org/express-2n-in-exactly-n1-powers-of-2/)

给定一个正整数 **N** ，任务是将 **2^N** 用 **2** 和**T7】的幂之和精确地用 **N+1** 表示。打印那些 **N+1** 术语。**

**示例:**

> **输入** : N = 4
> **输出** : 1 1 2 4 8
> **解释**:2^4 = 2^0+2^0+2^1+2^2+2^3 = 1+1+2+4+8
> 
> **输入** : N = 5
> **输出** : 1 1 2 4 8 16

**方法:**我们知道:

> 2^0 + 2^1 +….2^(N-1) = 2^N -1

因此，在 **2** 的幂级数的开头加上 **1** 将会产生正好是 **N+1** 项的 **2^N** 。

> 1 + 2^0 + 2^1 +….2^(N-1) = 2^N

下面是上述方法的实现

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find exactly N + 1 terms
// of powers of 2 series,  whose sum is 2^N
void powerOf2(long long N)
{
    cout << 1 << ' ';
    for (int i = 0; i < N; ++i) {
        cout << (long long)pow(2, i) << ' ';
    }
}

// Driver Code
int main()
{
    long long N = 5;

    powerOf2(N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class GFG
{
// Function to find exactly N + 1 terms
// of powers of 2 series,  whose sum is 2^N
static void powerOf2(long N)
{
    System.out.print(1);
    for (int i = 0; i < N; ++i) {
        System.out.print(" " + (long)Math.pow(2, i));
    }
}

// Driver Code
public static void main(String args[])
{
    long N = 5;
    powerOf2(N);
}
}
// This code is contributed by Samim Hossain Mondal
```

## C#

```
// C# program for the above approach
using System;
class GFG
{
// Function to find exactly N + 1 terms
// of powers of 2 series,  whose sum is 2^N
static void powerOf2(long N)
{
    Console.Write(1);
    for (int i = 0; i < N; ++i) {
        Console.Write(" " + (long)Math.Pow(2, i));
    }
}

// Driver Code
public static void Main()
{
    long N = 5;
    powerOf2(N);
}
}
// This code is contributed by Samim Hossain Mondal
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math

# Function to find exactly N + 1 terms
# of powers of 2 series,  whose sum is 2^N
def powerOf2(N) :

    print(1,end= ' ');
    for i in range(N) :
        print(int(math.pow(2, i)),end = ' ');

# Driver Code
if __name__ == "__main__" :

    N = 5;

    powerOf2(N);

    # This code is contributed by AnkThon
```

## java 描述语言

```
<script>
// JavaScript program for the above approach

// Function to find exactly N + 1 terms
// of powers of 2 series,  whose sum is 2^N
function powerOf2(N)
{
    document.write(1 + ' ');
    for (var i = 0; i < N; ++i) {
        document.write(Math.pow(2, i) + ' ');
    }
}

// Driver Code
N = 5;
powerOf2(N);

// This code is contributed by AnkThon
</script>
```

**Output**

```
1 1 2 4 8 16 
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)