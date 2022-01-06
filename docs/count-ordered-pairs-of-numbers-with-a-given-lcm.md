# 用给定的 LCM 对有序的数字对进行计数

> 原文:[https://www . geeksforgeeks . org/count-ordered-numbers-pairs-with-给定-lcm/](https://www.geeksforgeeks.org/count-ordered-pairs-of-numbers-with-a-given-lcm/)

给定一个整数 **N** ，任务是统计有序对的总数，使得每对的 [LCM](https://www.geeksforgeeks.org/program-to-find-lcm-of-two-numbers/) 等于 **N** 。

**示例:**

> **输入:** N = 6
> **输出:** 9
> **说明:**
> LCM 等于 N(= 6)的对为{(1，6)，(2，6)，(2，3)，(3，6)，(6，6)，(6，3)，(3，2)，(6，2)，(6，2)，(6，1)}
> 因此输出为 9。
> 
> **输入:**N = 36
> T3】输出: 25

**方法:**根据以下观察结果可以解决问题:

> 考虑一个有序对(X，Y)。
> X = P<sub>1</sub><sup>a1</sup>* P<sub>2</sub>T7】a2* P<sub>3</sub><sup>a3</sup>*…..* Pn<sup>an</sup>T15】Y = P<sub>1</sub>T18】B1* P<sub>2</sub>T22】B2* P<sub>3</sub>T26】B3*…..* Pn<sup>bn</sup>T30 这里，P <sub>1</sub> ，P <sub>2</sub> ，…..，P <sub>n</sub> 是 X 和 Y 的素因子，
> LCM(X，Y)= P<sub>1</sub>T40】max(a1，b1) * P2 <sup>max(a2，b2)</sup> *……。*Pn <sup>max(an，bn)</sup>
> 因此，LCM(X，Y)= N = P<sub>1</sub>T49】mT51<sup>1</sup>T54】P * P<sub>2</sub>T57】mT59<sup>2</sup>T62<sup>T64】P<sub>3</sub>T67】m【..* Pn<sup>m</sup>T77<sup>n</sup>T80】</sup>
> 
> 因此，有序对总数(X，Y)
> = {(m<sub>1</sub>+1)<sup>2</sup>–m<sub>1</sub>T7】2} * {(m<sub>2</sub>+1)<sup>2</sup>–m<sub>2</sub>T15】2} *……{(m<sub>n</sub>+1)<sup>2</sup>..* (2*m <sub>n</sub> +1)。

按照以下步骤解决问题:

1.  初始化一个变量，比如 **countPower** ，存储**N**T5】所有质因数的[幂。](https://www.geeksforgeeks.org/print-all-prime-factors-and-their-powers/)
2.  计算 **N** 所有质因数的[次幂。](https://www.geeksforgeeks.org/print-all-prime-factors-and-their-powers/)
3.  最后，使用上述公式打印有序对(X，Y)的计数。

以下是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count the number of
// ordered pairs with given LCM
int CtOrderedPairs(int N)
{
    // Stores count of
    // ordered pairs
    int res = 1;

    // Calculate power of all
    // prime factors of N
    for (int i = 2; i * i <= N; i++) {

        // Store the power of
        // prime factors
        int countPower = 0;
        while (N % i == 0) {
            countPower++;
            N /= i;
        }

        res = res * (2 * countPower
                     + 1);
    }

    if (N > 1) {
        res = res * (2 * 1 + 1);
    }
    return res;
}

// Driver Code
int main()
{
    int N = 36;
    cout << CtOrderedPairs(N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach

class GFG{

// Function to count the number of
// ordered pairs with given LCM
static int CtOrderedPairs(int N)
{

    // Stores count of
    // ordered pairs
    int res = 1;

    // Calculate power of all
    // prime factors of N
    for(int i = 2; i * i <= N; i++)
    {

        // Store the power of
        // prime factors
        int countPower = 0;

        while (N % i == 0)
        {
            countPower++;
            N /= i;
        }
        res = res * (2 * countPower + 1);
    }

    if (N > 1)
    {
        res = res * (2 * 1 + 1);
    }
    return res;
}

// Driver Code
public static void main(String[] args)
{
    int N = 36;

    System.out.println(CtOrderedPairs(N));
}
}

// This code is contributed by aimformohan
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to count the number of
# ordered pairs with given LCM
def CtOrderedPairs(N):

    # Stores count of
    # ordered pairs
    res = 1

    # Calculate power of all
    # prime factors of N
    i = 2
    while(i * i <= N):

        # Store the power of
        # prime factors
        countPower = 0
        while (N % i == 0):
            countPower += 1
            N //= i

        res = res * (2 * countPower + 1)
        i += 1

    if (N > 1):
        res = res * (2 * 1 + 1)

    return res

# Driver Code
N = 36

print(CtOrderedPairs(N))

# This code is contributed by code_hunt
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to count the number of
// ordered pairs with given LCM
static int CtOrderedPairs(int N)
{

    // Stores count of
    // ordered pairs
    int res = 1;

    // Calculate power of all
    // prime factors of N
    for(int i = 2; i * i <= N; i++)
    {

        // Store the power of
        // prime factors
        int countPower = 0;

        while (N % i == 0)
        {
            countPower++;
            N /= i;
        }
        res = res * (2 * countPower + 1);
    }

    if (N > 1)
    {
        res = res * (2 * 1 + 1);
    }
    return res;
}

// Driver Code
public static void Main()
{
    int N = 36;

    Console.WriteLine(CtOrderedPairs(N));
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to count the number of
// ordered pairs with given LCM
function CtOrderedPairs(N)
{

    // Stores count of
    // ordered pairs
    let res = 1;

    // Calculate power of all
    // prime factors of N
    for(let i = 2; i * i <= N; i++)
    {

        // Store the power of
        // prime factors
        let countPower = 0;

        while (N % i == 0)
        {
            countPower++;
            N /= i;
        }
        res = res * (2 * countPower + 1);
    }

    if (N > 1)
    {
        res = res * (2 * 1 + 1);
    }
    return res;
}

// Driver Code

    let N = 36;

    document.write(CtOrderedPairs(N));

</script>
```

**Output:** 

```
25
```

***时间复杂度:** O(√N)*
***辅助空间:** O(1)*