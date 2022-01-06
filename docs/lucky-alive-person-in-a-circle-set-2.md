# 幸运的活着的人在一个圈里|集合–2

> 原文:[https://www . geesforgeks . org/lucky-living-圈里人-set-2/](https://www.geeksforgeeks.org/lucky-alive-person-in-a-circle-set-2/)

假设有 N 个人(从 1 到 N)站着形成一个圆。他们手里都拿着枪，枪指向他们最左边的搭档。

每个人都这样投篮，1 投 2 中，3 投 4 中，5 投 6 中。(N-1)芽 N(如果 N 是偶数，则芽 N 为 1)。
同样在第二次迭代中，他们按照上面提到的逻辑拍摄剩余的遗骸(现在对于 n 为偶数，1 将拍摄到 3，5 将拍摄到 7，以此类推)。

任务是找到哪个人最幸运(没死)？

**示例**:

> **输入:** N = 3
> **输出:** 3
> 当 N = 3 时，1 将拍 2，3 将拍 1，因此 3 是最幸运的人。
> 
> **输入:** N = 8
> **输出:** 1
> 这里作为 N = 8，1 拍 1，3 拍 4，5 拍 6，7 拍 8，再一次 1 拍 3，5 拍 7，再一次 1 拍 5，因此 1 是最幸运的人。

这个问题已经在[幸运活一圈人|剑谜代码解](https://www.geeksforgeeks.org/lucky-alive-person-circle/)中讨论过了。在这篇文章中，讨论了一种不同的方法。

**进场:**

1.  取 n 的二进制等价物
2.  找到它的 1 的补数，并转换成相等的十进制数 n `。
3.  查找| N–N ` |。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to convert string to number
int stringToNum(string s)
{

    // object from the class stringstream
    stringstream geek(s);

    // The object has the value 12345 and stream
    // it to the integer x
    int x = 0;
    geek >> x;

    return x;
}

// Function to convert binary to decimal
int binaryToDecimal(string n)
{
    int num = stringToNum(n);
    int dec_value = 0;

    // Initializing base value to 1, i.e 2^0
    int base = 1;

    int temp = num;
    while (temp) {
        int last_digit = temp % 10;
        temp = temp / 10;

        dec_value += last_digit * base;

        base = base * 2;
    }

    return dec_value;
}

string itoa(int num, string str, int base)
{
    int i = 0;
    bool isNegative = false;

    /* Handle 0 explicitly, otherwise
    empty string is printed for 0 */
    if (num == 0) {
        str[i++] = '0';
        return str;
    }

    // In standard itoa(), negative numbers
    // are handled only with base 10.
    // Otherwise numbers are considered unsigned.
    if (num < 0 && base == 10) {
        isNegative = true;
        num = -num;
    }

    // Process individual digits
    while (num != 0) {
        int rem = num % base;
        str[i++] = (rem > 9) ? (rem - 10) + 'a' : rem + '0';
        num = num / base;
    }

    // If the number is negative, append '-'
    if (isNegative)
        str[i++] = '-';

    // Reverse the string
    reverse(str.begin(), str.end());

    return str;
}

char flip(char c)
{
    return (c == '0') ? '1' : '0';
}

// Function to find the ones complement
string onesComplement(string bin)
{
    int n = bin.length(), i;

    string ones = "";

    // for ones complement flip every bit
    for (i = 0; i < n; i++)
        ones += flip(bin[i]);

    return ones;
}

// Driver code
int main()
{
    // Taking the number of a person
    // standing in a circle.
    int N = 3;
    string arr = "";

    // Storing the binary equivalent in a string.
    string ans(itoa(N, arr, 2));

    // taking one's compelement and
    // convert it to decimal value
    int N_dash = binaryToDecimal(onesComplement(ans));

    int luckiest_person = N - N_dash;

    cout << luckiest_person;

    return 0;
}
```

**Output**

```
3
```

**交替较短实现:**
这里使用的方法是相同的。

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

int luckiest_person(int n)
{
    // to calculate the number of bits in
    // the binary equivalent of n
    int len = log2(n) + 1;

    // Finding complement by inverting the
    // bits one by one from last
    int n2 = n;
    for (int i = 0; i < len; i++) {

        // XOR of n2 with (1<<i) to flip
        // the last (i+1)th bit of binary equivalent of n2
        n2 = n2 ^ (1 << i);
    }

    // n2 will be the one's complement of n
    return abs(n - n2);
}
int main()
{
    int N = 3;
    int lucky_p = luckiest_person(N);
    cout << lucky_p;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.io.*;

class GFG {

    static int luckiest_person(int n)
    {

        // To calculate the number of bits in
        // the binary equivalent of n
        int len = (int)(Math.log(n) / Math.log(2)) + 1;

        // Finding complement by inverting the
        // bits one by one from last
        int n2 = n;
        for (int i = 0; i < len; i++) {

            // XOR of n2 with (1<<i) to flip the last
            // (i+1)th bit of binary equivalent of n2
            n2 = n2 ^ (1 << i);
        }

        // n2 will be the one's complement of n
        return Math.abs(n - n2);
    }

    // Driver code
    public static void main(String[] args)
    {
        int N = 3;
        int lucky_p = luckiest_person(N);

        System.out.println(lucky_p);
    }
}

// This code is contributed by rishavmahato348
```

## C#

```
// C# implementation of the above approach
using System;

class GFG {

    static int luckiest_person(int n)
    {

        // To calculate the number of bits in
        // the binary equivalent of n
        int len = (int)(Math.Log(n) / Math.Log(2)) + 1;

        // Finding complement by inverting the
        // bits one by one from last
        int n2 = n;
        for (int i = 0; i < len; i++) {

            // XOR of n2 with (1<<i) to flip the last
            // (i+1)th bit of binary equivalent of n2
            n2 = n2 ^ (1 << i);
        }

        // n2 will be the one's complement of n
        return Math.Abs(n - n2);
    }

    // Driver code
    public static void Main()
    {
        int N = 3;
        int lucky_p = luckiest_person(N);

        Console.Write(lucky_p);
    }
}

// This code is contributed by subhammahato348
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach

function luckiest_person(n)
{
    // to calculate the number of bits in
    // the binary equivalent of n
    let len = parseInt(Math.log(n) / Math.log(2)) + 1;

    // Finding complement by inverting the
    // bits one by one from last
    let n2 = n;
    for (let i = 0; i < len; i++) {

        // XOR of n2 with (1<<i) to flip
        // the last (i+1)th bit of binary equivalent of n2
        n2 = n2 ^ (1 << i);
    }

    // n2 will be the one's complement of n
    return Math.abs(n - n2);
}

// Driver Code
    let N = 3;
    let lucky_p = luckiest_person(N);
    document.write(lucky_p);

</script>
```

**Output**

```
3
```

O(1)中的替代实现:这里使用的方法是相同的，但是使用的操作是恒定时间的。

## C++

```
// Here is a O(1) solution for this problem
// it will work for 32 bit integers]
#include <bits/stdc++.h>
using namespace std;

// function to find the highest power of 2
// which is less than n
int setBitNumber(int n)
{
    // Below steps set bits after
    // MSB (including MSB)

    // Suppose n is 273 (binary
    // is 100010001). It does following
    // 100010001 | 010001000 = 110011001
    n |= n >> 1;

    // This makes sure 4 bits
    // (From MSB and including MSB)
    // are set. It does following
    // 110011001 | 001100110 = 111111111
    n |= n >> 2;

    n |= n >> 4;
    n |= n >> 8;
    n |= n >> 16;

    // Increment n by 1 so that
    // there is only one set bit
    // which is just before original
    // MSB. n now becomes 1000000000
    n = n + 1;

    // Return original MSB after shifting.
    // n now becomes 100000000
    return (n >> 1);
}

int luckiest_person(int n)
{
    // to calculate the highest number which
    // is power of 2 and less than n
    int nearestPower = setBitNumber(n);

    // return the correct answer as per the
    // approach in above article
    return 2 * (n - nearestPower) + 1;
}
int main()
{
    int N = 8;
    int lucky_p = luckiest_person(N);
    cout << lucky_p;
    return 0;
}

// This code is contributed by Ujesh Maurya
```

## C#

```
// Here is a O(1) solution for this problem
// it will work for 32 bit integers]
using System;

class GFG {

    // function to find the highest power of 2
    // which is less than n
    static int setBitNumber(int n)
    {
        // Below steps set bits after
        // MSB (including MSB)

        // Suppose n is 273 (binary
        // is 100010001). It does following
        // 100010001 | 010001000 = 110011001
        n |= n >> 1;

        // This makes sure 4 bits
        // (From MSB and including MSB)
        // are set. It does following
        // 110011001 | 001100110 = 111111111
        n |= n >> 2;

        n |= n >> 4;
        n |= n >> 8;
        n |= n >> 16;

        // Increment n by 1 so that
        // there is only one set bit
        // which is just before original
        // MSB. n now becomes 1000000000
        n = n + 1;

        // Return original MSB after shifting.
        // n now becomes 100000000
        return (n >> 1);
    }

    static int luckiest_person(int n)
    {

        // to calculate the highest number which
        // is power of 2 and less than n
        int nearestPower = setBitNumber(n);

        // return the correct answer as per the
        // approach in above article
        return 2 * (n - nearestPower) + 1;
    }

    // Driver code
    public static void Main()
    {
        int N = 8;
        int lucky_p = luckiest_person(N);

        Console.Write(lucky_p);
    }
}

// This code is contributed by Ujesh Maurya
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */

import java.io.*;

// Here is a O(1) solution for this problem
// it will work for 32 bit integers]
class GFG {
    static int setBitNumber(int n)
    {

        // Below steps set bits after
        // MSB (including MSB)

        // Suppose n is 273 (binary
        // is 100010001). It does following
        // 100010001 | 010001000 = 110011001
        n |= n >> 1;

        // This makes sure 4 bits
        // (From MSB and including MSB)
        // are set. It does following
        // 110011001 | 001100110 = 111111111
        n |= n >> 2;

        n |= n >> 4;
        n |= n >> 8;
        n |= n >> 16;

        // Increment n by 1 so that
        // there is only one set bit
        // which is just before original
        // MSB. n now becomes 1000000000
        n = n + 1;

        // Return original MSB after shifting.
        // n now becomes 100000000
        return (n >> 1);
    }

    static int luckiest_person(int n)
    {
        // to calculate the highest number which
        // is power of 2 and less than n
        int nearestPower = setBitNumber(n);

        // return the correct answer as per the
        // approach in above article
        return 2 * (n - nearestPower) + 1;
    }
    // Driver Code
    public static void main(String[] args)
    {
        int N = 8;
        int lucky_p = luckiest_person(N);

        System.out.print(lucky_p);
    }
}

// This code is contributed by Ujesh Maurya
```

**Output**

```
1
```

O(1)中的另一种方法:基于给定问题中形成的模式，如下表所示。

<figure class="table">

| **n** |   | one |   | Two | three |   | four | five | six | seven |   | eight | nine | Ten | Eleven | Twelve | Thirteen | Fourteen | Fifteen |   | Sixteen |
|   |   | one |   | one | three |   | one | three | five | seven |   | one | three | five | seven | nine | Eleven | Thirteen | Fifteen |   | one |

## C++

```
#include <bits/stdc++.h>
#include <iostream>
using namespace std;

// Driven code
int find(int n)
{
    // Obtain number less n in 2's power
    int twospower = pow(2, (int)log2(n));

    // Find p-position of odd number, in odd series
    int diff = n - twospower + 1;

    // Value of pth odd number
    int diffthodd = (2 * diff) - 1;

    return diffthodd;
}
// Driver code
int main()
{
    int n = 5;
    cout << find(n);
    return 0;
}

// This code is contributed by Dharmik Parmar
```

**Output**

```
3
```

</figure>