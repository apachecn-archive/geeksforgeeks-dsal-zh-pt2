# 表示二进制数的最大 N 个整数的计数

> 原文:[https://www . geesforgeks . org/整数计数-最多 n-代表二进制数/](https://www.geeksforgeeks.org/count-of-integers-up-to-n-which-represent-a-binary-number/)

给定一个整数 **N** ，任务是计算从 1 到 **N** (包括两者)的每个数字 **i** ，使得 **i** 是某个整数的二进制表示，其中 **N** 可以是范围**【1，10<sup>9</sup>**内的任何值

**示例:**

> **输入:** N = 100
> **输出:** 4
> **说明:**有效整数为 1、10、11、100
> 
> **输入:** N = 20
> **输出:** 3
> **说明:**有效整数为 1、10、11

**天真的做法:**由于 **N** 中的最大位数可以是 10，所以存储每一个 10 位数的二进制组合，然后使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)或[上限](https://www.geeksforgeeks.org/upper_bound-in-cpp/)来检查 **N** 给定范围内的最大整数。
***时间复杂度:** O(MAX + log(MAX))其中 MAX = 1024 (2 <sup>10</sup> )*

**有效方法:**我们可以观察到，对于任何 N 值，这种可能表示的最大数量是**2<sup>N 的位数</sup>–1**。因此，我们需要遵循以下步骤:

*   从右向左提取 N 个数字，并将当前数字的位置存储在变量**ctrl**中。
*   如果当前数字超过 1，则意味着可以获得使用**ctrl**数字的最大可能表示。因此，将答案设置为等于 2**<sup>ctrl</sup>–1**。
*   否则，如果当前数字为 1，则在目前获得的答案上加上**2<sup>ctrl–1</sup>**。
*   遍历所有数字后得到的最终值给出了答案。

下面是上述方法的实现:

## C++

```
// C++ Program to count the
// number of integers upto N
// which are of the form of
// binary representations

#include <bits/stdc++.h>
using namespace std;

// Function to return the count
int countBinaries(int N)
{

    int ctr = 1;
    int ans = 0;
    while (N > 0) {

        // If the current last
        // digit is 1
        if (N % 10 == 1) {

            // Add 2^(ctr - 1) possible
            // integers to the answer
            ans += pow(2, ctr - 1);
        }

        // If the current digit exceeds 1
        else if (N % 10 > 1) {

            // Set answer as 2^ctr - 1
            // as all possible binary
            // integers with ctr number
            // of digits can be obtained
            ans = pow(2, ctr) - 1;
        }

        ctr++;
        N /= 10;
    }

    return ans;
}
// Driver Code
int main()
{

    int N = 20;
    cout << countBinaries(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count the number
// of integers upto N which are of
// the form of binary representations
import java.util.*;
class GFG{

// Function to return the count
static int countBinaries(int N)
{
    int ctr = 1;
    int ans = 0;
    while (N > 0)
    {

        // If the current last
        // digit is 1
        if (N % 10 == 1)
        {

            // Add 2^(ctr - 1) possible
            // integers to the answer
            ans += Math.pow(2, ctr - 1);
        }

        // If the current digit exceeds 1
        else if (N % 10 > 1)
        {

            // Set answer as 2^ctr - 1
            // as all possible binary
            // integers with ctr number
            // of digits can be obtained
            ans = (int) (Math.pow(2, ctr) - 1);
        }
        ctr++;
        N /= 10;
    }
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int N = 20;
    System.out.print(countBinaries(N));
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 program to count the
# number of integers upto N
# which are of the form of
# binary representations
from math import *

# Function to return the count
def countBinaries(N):

    ctr = 1
    ans = 0

    while (N > 0):

        # If the current last
        # digit is 1
        if (N % 10 == 1):

            # Add 2^(ctr - 1) possible
            # integers to the answer
            ans += pow(2, ctr - 1)

        # If the current digit exceeds 1
        elif (N % 10 > 1):

            # Set answer as 2^ctr - 1
            # as all possible binary
            # integers with ctr number
            # of digits can be obtained
            ans = pow(2, ctr) - 1

        ctr += 1
        N //= 10

    return ans

# Driver Code
if __name__ == '__main__':

    N = 20

    print(int(countBinaries(N)))

# This code is contributed by Bhupendra_Singh
```

## C#

```
// C# program to count the number
// of integers upto N which are of
// the form of binary representations
using System;

class GFG{

// Function to return the count
static int countBinaries(int N)
{
    int ctr = 1;
    int ans = 0;
    while (N > 0)
    {

        // If the current last
        // digit is 1
        if (N % 10 == 1)
        {

            // Add 2^(ctr - 1) possible
            // integers to the answer
            ans += (int)Math.Pow(2, ctr - 1);
        }

        // If the current digit exceeds 1
        else if (N % 10 > 1)
        {

            // Set answer as 2^ctr - 1
            // as all possible binary
            // integers with ctr number
            // of digits can be obtained
            ans = (int)(Math.Pow(2, ctr) - 1);
        }
        ctr++;
        N /= 10;
    }
    return ans;
}

// Driver Code
public static void Main(String[] args)
{
    int N = 20;
    Console.Write(countBinaries(N));
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>

    // Javascript Program to count the
    // number of integers upto N
    // which are of the form of
    // binary representations

    // Function to return the count
    function countBinaries(N)
    {

        let ctr = 1;
        let ans = 0;
        while (N > 0) {

            // If the current last
            // digit is 1
            if (N % 10 == 1) {

                // Add 2^(ctr - 1) possible
                // integers to the answer
                ans += Math.pow(2, ctr - 1);
            }

            // If the current digit exceeds 1
            else if (N % 10 > 1) {

                // Set answer as 2^ctr - 1
                // as all possible binary
                // integers with ctr number
                // of digits can be obtained
                ans = Math.pow(2, ctr) - 1;
            }

            ctr++;
            N /= 10;
        }

        return ans;
    }

    let N = 20;
    document.write(countBinaries(N));

    // This code is contributed by divyesh072019.

</script>
```

**Output:** 

```
3
```

**时间复杂度:** *O(M <sup>2</sup> )* 其中 M 是 N
**辅助空间的位数:** *O(1)*

**优化:**上述方法可以通过借助前缀积数组预先计算 2 的[次方到 M(N 的位数到 M)来优化。](https://www.geeksforgeeks.org/powers-2-required-sum/)

以下是优化解决方案的实施情况:

## C++

```
// C++ Program to count the
// number of integers upto N
// which are of the form of
// binary representations

#include <bits/stdc++.h>
using namespace std;

// Function to return the count
int countBinaries(int N)
{
    // PreCompute and store
    // the powers of 2
    vector<int> powersOfTwo(11);

    powersOfTwo[0] = 1;
    for (int i = 1; i < 11; i++) {
        powersOfTwo[i]
= powersOfTwo[i - 1]
* 2;
    }

    int ctr = 1;
    int ans = 0;
    while (N > 0) {

        // If the current last
        // digit is 1
        if (N % 10 == 1) {

            // Add 2^(ctr - 1) possible
            // integers to the answer
            ans += powersOfTwo[ctr - 1];
        }

        // If the current digit exceeds 1
        else if (N % 10 > 1) {

            // Set answer as 2^ctr - 1
            // as all possible binary
            // integers with ctr number
            // of digits can be obtained
            ans = powersOfTwo[ctr] - 1;
        }

        ctr++;
        N /= 10;
    }

    return ans;
}
// Driver Code
int main()
{

    int N = 20;
    cout << countBinaries(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count the number of
// integers upto N which are of the
// form of binary representations
import java.util.*;

class GFG{

// Function to return the count
static int countBinaries(int N)
{

    // PreCompute and store
    // the powers of 2
    Vector<Integer> powersOfTwo = new Vector<Integer>(11);
    powersOfTwo.add(1);

    for(int i = 1; i < 11; i++)
    {
       powersOfTwo.add(powersOfTwo.get(i - 1) * 2);
    }

    int ctr = 1;
    int ans = 0;
    while (N > 0)
    {

        // If the current last
        // digit is 1
        if (N % 10 == 1)
        {

            // Add 2^(ctr - 1) possible
            // integers to the answer
            ans += powersOfTwo.get(ctr - 1);
        }

        // If the current digit exceeds 1
        else if (N % 10 > 1)
        {

            // Set answer as 2^ctr - 1
            // as all possible binary
            // integers with ctr number
            // of digits can be obtained
            ans = powersOfTwo.get(ctr) - 1;
        }
        ctr++;
        N /= 10;
    }
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int N = 20;
    System.out.print(countBinaries(N));
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 program to count the
# number of integers upto N
# which are of the form of
# binary representations

# Function to return the count
def countBinaries(N):

    # PreCompute and store
    # the powers of 2
    powersOfTwo = [0] * 11

    powersOfTwo[0] = 1

    for i in range(1, 11):
        powersOfTwo[i] = powersOfTwo[i - 1] * 2

    ctr = 1
    ans = 0

    while (N > 0):

        # If the current last
        # digit is 1
        if (N % 10 == 1):

            # Add 2^(ctr - 1) possible
            # integers to the answer
            ans += powersOfTwo[ctr - 1]

        # If the current digit exceeds 1
        elif (N % 10 > 1):

            # Set answer as 2^ctr - 1
            # as all possible binary
            # integers with ctr number
            # of digits can be obtained
            ans = powersOfTwo[ctr] - 1

        ctr += 1
        N = N // 10

    return ans

# Driver code
N = 20

print(countBinaries(N))

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program to count the number of
// integers upto N which are of the
// form of binary representations
using System;
using System.Collections.Generic;
class GFG{

// Function to return the count
static int countBinaries(int N)
{

    // PreCompute and store
    // the powers of 2
    List<int> powersOfTwo = new List<int>();
    powersOfTwo.Add(1);

    for(int i = 1; i < 11; i++)
    {
        powersOfTwo.Add(powersOfTwo[i - 1] * 2);
    }

    int ctr = 1;
    int ans = 0;
    while (N > 0)
    {

        // If the current last
        // digit is 1
        if (N % 10 == 1)
        {

            // Add 2^(ctr - 1) possible
            // integers to the answer
            ans += powersOfTwo[ctr - 1];
        }

        // If the current digit exceeds 1
        else if (N % 10 > 1)
        {

            // Set answer as 2^ctr - 1
            // as all possible binary
            // integers with ctr number
            // of digits can be obtained
            ans = powersOfTwo[ctr] - 1;
        }
        ctr++;
        N /= 10;
    }
    return ans;
}

// Driver Code
static public void Main ()
{
    int N = 20;
    Console.Write(countBinaries(N));
}
}

// This code is contributed by ShubhamCoder
```

## java 描述语言

```
<script>
    // Javascript program to count the number of
    // integers upto N which are of the
    // form of binary representations

    // Function to return the count
    function countBinaries(N)
    {

        // PreCompute and store
        // the powers of 2
        let powersOfTwo = [];
        powersOfTwo.push(1);

        for(let i = 1; i < 11; i++)
        {
            powersOfTwo.push(powersOfTwo[i - 1] * 2);
        }

        let ctr = 1;
        let ans = 0;
        while (N > 0)
        {

            // If the current last
            // digit is 1
            if (N % 10 == 1)
            {

                // Add 2^(ctr - 1) possible
                // integers to the answer
                ans += powersOfTwo[ctr - 1];
            }

            // If the current digit exceeds 1
            else if (N % 10 > 1)
            {

                // Set answer as 2^ctr - 1
                // as all possible binary
                // integers with ctr number
                // of digits can be obtained
                ans = powersOfTwo[ctr] - 1;
            }
            ctr++;
            N /= 10;
        }
        return ans;
    }

    let N = 20;
    document.write(countBinaries(N));
</script>
```

**Output:** 

```
3
```

**时间复杂度:***O(M)*
T5】辅助空间: *O(M)*