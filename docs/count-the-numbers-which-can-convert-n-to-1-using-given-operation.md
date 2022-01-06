# 用给定的运算数出能把 N 转换成 1 的数字

> 原文:[https://www . geesforgeks . org/count-the-numbers-哪些可以使用给定操作将 n 转换为 1/](https://www.geeksforgeeks.org/count-the-numbers-which-can-convert-n-to-1-using-given-operation/)

给定一个正整数 **N (N ≥ 2)** ，任务是对范围【2，N】内的整数 **X** 的个数进行计数，使得 X 可以通过以下操作将 N 转换为 1:

*   如果 **N** 可以被 **X** 整除，那么将 N 的值更新为 **N / X** 。
*   否则，将 N 的值更新为**N–X**。

**示例:**

> **输入:** N = 6
> **输出:** 3
> **解释:**
> 以下整数可用于将 N 转换为 1:
> X = 2 =>N = 6->N = 3->N = 1
> X = 5 =>N = 6->N = 1
> X = 6 =>N = 6->N = 1
> 
> **输入:**N = 48
> T3】输出: 4

**天真法:**这个问题的天真法是把 2 到 N 的所有整数迭代一遍，统计一下能把 N 转换成 1 的整数个数。

下面是上述方法的实现:

## C++

```
// C++ program to count the numbers
// which can convert N to 1
// using the given operation

#include <bits/stdc++.h>
using namespace std;

// Function to count the numbers
// which can convert N to 1
// using the given operation
int countValues(int n)
{

    int answer = 0;

    // Iterate through all the integers
    for (int i = 2; i <= n; i++) {
        int k = n;

        // Check if N can be converted
        // to 1
        while (k >= i) {
            if (k % i == 0)
                k /= i;
            else
                k -= i;
        }

        // Incrementing the count if it can
        // be converted
        if (k == 1)
            answer++;
    }
    return answer;
}

// Driver code
int main()
{
    int N = 6;

    cout << countValues(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count the numbers
// which can convert N to 1
// using the given operation
import java.io.*;
import java.util.*;
class GFG{

// Function to count the numbers
// which can convert N to 1
// using the given operation
static int countValues(int n)
{
    int answer = 0;

    // Iterate through all the integers
    for (int i = 2; i <= n; i++)
    {
        int k = n;

        // Check if N can be converted
        // to 1
        while (k >= i)
        {
            if (k % i == 0)
                k /= i;
            else
                k -= i;
        }

        // Incrementing the count if it can
        // be converted
        if (k == 1)
            answer++;
    }
    return answer;
}

// Driver code
public static void main(String args[])
{
    int N = 6;

    System.out.print(countValues(N));
}
}

// This code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# Python3 program to count the numbers
# which can convert N to 1
# using the given operation

# Function to count the numbers
# which can convert N to 1
# using the given operation
def countValues(n):
    answer = 0

    # Iterate through all the integers
    for i in range(2, n + 1, 1):
        k = n

        # Check if N can be converted
        # to 1
        while (k >= i):
            if (k % i == 0):
                k //= i
            else:
                k -= i

        # Incrementing the count if it can
        # be converted
        if (k == 1):
            answer += 1
    return answer

# Driver code
if __name__ == '__main__':

    N = 6
    print(countValues(N))

# This code is contributed by Samarth
```

## C#

```
// C# program to count the numbers
// which can convert N to 1
// using the given operation
using System;
class GFG{

// Function to count the numbers
// which can convert N to 1
// using the given operation
static int countValues(int n)
{
    int answer = 0;

    // Iterate through all the integers
    for (int i = 2; i <= n; i++)
    {
        int k = n;

        // Check if N can be converted
        // to 1
        while (k >= i)
        {
            if (k % i == 0)
                k /= i;
            else
                k -= i;
        }

        // Incrementing the count if it can
        // be converted
        if (k == 1)
            answer++;
    }
    return answer;
}

// Driver code
public static void Main()
{
    int N = 6;

    Console.Write(countValues(N));
}
}

// This code is contributed by Nidhi_biet
```

## java 描述语言

```
<script>

    // Javascript program to count the numbers
    // which can convert N to 1
    // using the given operation

    // Function to count the numbers
    // which can convert N to 1
    // using the given operation
    function countValues(n)
    {

        let answer = 0;

        // Iterate through all the integers
        for (let i = 2; i <= n; i++) {
            let k = n;

            // Check if N can be converted
            // to 1
            while (k >= i) {
                if (k % i == 0)
                    k /= i;
                else
                    k -= i;
            }

            // Incrementing the count if it can
            // be converted
            if (k == 1)
                answer++;
        }
        return answer;
    }

    let N = 6;

    document.write(countValues(N));

</script>
```

**Output:** 

```
3
```

**时间复杂度:** *O(N)* ，其中 N 为给定数。

**辅助空间:** O(1)

**有效方法:**想法是观察如果 N 最初不能被 X 整除，那么只有减法会进行到底，因为每次减法后 N 仍然不能被 N 整除。此外，当 N ≤ X 时，这些操作将停止，N 的最终值将等于 **N mod X** 。

所以，对于从 2 到 N 的所有数字，只有两种可能的情况:

1.  **不发生除法运算:**对于所有这些数，最终值将等于 N mod X，只有当 N mod X = 1 时，N 最终才会变成 1。显然，对于 X = N–1，以及 N–1 的所有除数，N 模 X = 1 成立。
2.  **除法运算不止一次:**除法运算只会对 N 上的除数进行，对于 N 的每个除数，比如 d，执行除法运算直到 N mod d！= 0.如果最终 N mod d = 1，那么这将包含在答案中，否则不包含(使用从案例 1 中导出的属性)。

下面是上述方法的实现:

## C++

```
// C++ program to count the numbers
// which can convert N to 1
// using the given operation

#include <bits/stdc++.h>
using namespace std;

// Function to count the numbers
// which can convert N to 1
// using the given operation
int countValues(int N)
{

    vector<int> div;

    // Store all the divisors of N
    for (int i = 2; i * i <= N; i++) {

        // If i is a divisor
        if (N % i == 0) {
            div.push_back(i);

            // If i is not equal to N / i
            if (N != i * i) {
                div.push_back(N / i);
            }
        }
    }

    int answer = 0;

    // Iterate through all the divisors of
    // N - 1 and count them in answer
    for (int i = 1; i * i <= N - 1; i++) {

        // Check if N - 1 is a divisor
        // or not
        if ((N - 1) % i == 0) {
            if (i * i == N - 1)
                answer++;
            else
                answer += 2;
        }
    }

    // Iterate through all divisors and check
    // for N mod d = 1 or (N-1) mod d = 0
    for (auto d : div) {
        int K = N;
        while (K % d == 0)
            K /= d;
        if ((K - 1) % d == 0)
            answer++;
    }
    return answer;
}

// Driver code
int main()
{
    int N = 6;

    cout << countValues(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count the numbers
// which can convert N to 1
// using the given operation
import java.util.*;

class GFG{

// Function to count the numbers
// which can convert N to 1
// using the given operation
static int countValues(int N)
{
    Vector<Integer> div = new Vector<>();

    // Store all the divisors of N
    for(int i = 2; i * i <= N; i++)
    {

        // If i is a divisor
        if (N % i == 0)
        {
            div.add(i);

            // If i is not equal to N / i
            if (N != i * i)
            {
                div.add(N / i);
            }
        }
    }

    int answer = 0;

    // Iterate through all the divisors of
    // N - 1 and count them in answer
    for(int i = 1; i * i <= N - 1; i++)
    {

        // Check if N - 1 is a divisor
        // or not
        if ((N - 1) % i == 0)
        {
            if (i * i == N - 1)
                answer++;
            else
                answer += 2;
        }
    }

    // Iterate through all divisors and check
    // for N mod d = 1 or (N-1) mod d = 0
    for(int d : div)
    {
        int K = N;
        while (K % d == 0)
            K /= d;

        if ((K - 1) % d == 0)
            answer++;
    }
    return answer;
}

// Driver code
public static void main(String[] args)
{
    int N = 6;

    System.out.print(countValues(N));
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program to count the numbers
# which can convert N to 1
# using the given operation

# Function to count the numbers
# which can convert N to 1
# using the given operation
def countValues(N):

    div = []
    i = 2

    # Store all the divisors of N
    while ((i * i) <= N):

        # If i is a divisor
        if (N % i == 0):
            div.append(i)

            # If i is not equal to N / i
            if (N != i * i):
                div.append(N // i)

        i += 1 

    answer = 0
    i = 1

    # Iterate through all the divisors of
    # N - 1 and count them in answer
    while((i * i) <= N - 1):

        # Check if N - 1 is a divisor
        # or not
        if ((N - 1) % i == 0):
            if (i * i == N - 1):
                answer += 1
            else:
                answer += 2

        i += 1

    # Iterate through all divisors and check
    # for N mod d = 1 or (N-1) mod d = 0
    for d in div:
        K = N

        while (K % d == 0):
            K //= d
        if ((K - 1) % d == 0):
            answer += 1

    return answer

# Driver code
if __name__=="__main__":

    N = 6

    print(countValues(N))

# This code is contributed by rutvik_56
```

## C#

```
// C# program to count the numbers
// which can convert N to 1
// using the given operation
using System;
using System.Collections.Generic;

class GFG{

// Function to count the numbers
// which can convert N to 1
// using the given operation
static int countValues(int N)
{
    List<int> div = new List<int>();

    // Store all the divisors of N
    for(int i = 2; i * i <= N; i++)
    {

        // If i is a divisor
        if (N % i == 0)
        {
            div.Add(i);

            // If i is not equal to N / i
            if (N != i * i)
            {
                div.Add(N / i);
            }
        }
    }

    int answer = 0;

    // Iterate through all the divisors of
    // N - 1 and count them in answer
    for(int i = 1; i * i <= N - 1; i++)
    {

        // Check if N - 1 is a divisor
        // or not
        if ((N - 1) % i == 0)
        {
            if (i * i == N - 1)
                answer++;
            else
                answer += 2;
        }
    }

    // Iterate through all divisors and check
    // for N mod d = 1 or (N-1) mod d = 0
    foreach(int d in div)
    {
        int K = N;
        while (K % d == 0)
            K /= d;

        if ((K - 1) % d == 0)
            answer++;
    }
    return answer;
}

// Driver code
public static void Main(String[] args)
{
    int N = 6;

    Console.Write(countValues(N));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// JavaScript program to count the numbers
// which can convert N to 1
// using the given operation

// Function to count the numbers
// which can convert N to 1
// using the given operation
function countValues(N)
{

    var div = [];

    // Store all the divisors of N
    for (var i = 2; i * i <= N; i++) {

        // If i is a divisor
        if (N % i == 0) {
            div.push(i);

            // If i is not equal to N / i
            if (N != i * i) {
                div.push(N / i);
            }
        }
    }

    var answer = 0;

    // Iterate through all the divisors of
    // N - 1 and count them in answer
    for (var i = 1; i * i <= N - 1; i++) {

        // Check if N - 1 is a divisor
        // or not
        if ((N - 1) % i == 0) {
            if (i * i == N - 1)
                answer++;
            else
                answer += 2;
        }
    }

    // Iterate through all divisors and check
    // for N mod d = 1 or (N-1) mod d = 0
    div.forEach(d => {

        var K = N;
        while (K % d == 0)
            K /= d;
        if ((K - 1) % d == 0)
            answer++;
    });
    return answer;
}

// Driver code
var N = 6;
document.write( countValues(N));

</script>
```

**Output:** 

```
3
```

**时间复杂度:**

![O(\sqrt{N})        ](img/e8ced7241c755505395656503aedd6c7.png "Rendered by QuickLaTeX.com")

**辅助空间:** O(sqrt(N))