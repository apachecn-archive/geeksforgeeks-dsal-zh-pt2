# 满足给定条件的子序列计数

> 原文:[https://www . geesforgeks . org/满足给定条件的子序列计数/](https://www.geeksforgeeks.org/count-of-sub-sequences-which-satisfy-the-given-condition/)

给定一个由数字组成的字符串 **str** ，任务是找到可能的 4 位子序列的数量，这些子序列的形式为 **(x，x，x + 1，x + 1)** ，其中 x 可以来自范围**【0，8】**。
**举例:**

> **输入:** str = "1122"
> **输出:** 1
> 只有一个子序列有效，即整个字符串本身。
> **输入:** str = "13134422"
> **输出:** 2
> 存在两个有效子序列“1122”和“3344”。

**进场:**

*   我们将找出从 0 到 8 的每个可能 x 的可能子序列的总数。
*   对于每个 x，从字符串中删除除 x 和 x+1 之外的所有其他数字，因为它们不会影响答案。
*   保留一个前缀 Sum 数组来计算 x+1 位数，直到字符串中的第一个索引。
*   现在，对于每个数字俱乐部，比如大小为 K(x)，我们可以用 KC2 的方式选择两个数字。最后两个数字可以是所有数字(x+1)中的任意两个数字，这些数字跟在那个数字俱乐部(计数是使用前缀和数组确定的)后面，比如大小 L，所以有 LC2 种方法可以选择。总途径= KC2 * LC2。
*   直到现在，我们可以认为 x 来自同一个俱乐部，但也可以来自多个俱乐部。因此，我们必须考虑所有可能的球杆对，并将其大小相乘，以获得选择前两个数字的方法数。对于最后两个数字，方式将保持不变。
*   为了防止步骤 5 中的过度计数问题。只有包括考虑中的当前俱乐部的可能方式才会被选择，因为在计算以前的俱乐部时已经考虑了其他方式。
*   将所有可能的 x 值相加，取模。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
#define ll long long int
#define MOD 1000000007
using namespace std;

// Function to return the total
// required sub-sequences
int solve(string test)
{
    int size = test.size();
    int total = 0;

    // Find ways for all values of x
    for (int i = 0; i <= 8; i++) {
        int x = i;

        // x+1
        int y = i + 1;
        string newtest;

        // Removing all unnecessary digits
        for (int j = 0; j < size; j++) {
            if (test[j] == x + 48 || test[j] == y + 48) {
                newtest += test[j];
            }
        }

        if (newtest.size() > 0) {
            int size1 = newtest.size();

            // Prefix Sum Array for X+1 digit
            int prefix[size1] = { 0 };
            for (int j = 0; j < size1; j++) {
                if (newtest[j] == y + 48) {
                    prefix[j]++;
                }
            }

            for (int j = 1; j < size1; j++) {
                prefix[j] += prefix[j - 1];
            }

            int count = 0;
            int firstcount = 0;

            // Sum of squares
            int ss = 0;

            // Previous sum of all possible pairs
            int prev = 0;

            for (int j = 0; j < size1; j++) {
                if (newtest[j] == x + 48) {
                    count++;
                    firstcount++;
                }
                else {

                    ss += count * count;

                    // To find sum of multiplication of all
                    // possible pairs
                    int pairsum = (firstcount * firstcount - ss) / 2;
                    int temp = pairsum;

                    // To prevent overcounting
                    pairsum -= prev;
                    prev = temp;

                    int secondway = prefix[size1 - 1];
                    if (j != 0)
                        secondway -= prefix[j - 1];

                    int answer = count * (count - 1)
                                 * secondway * (secondway - 1);
                    answer /= 4;
                    answer += (pairsum * secondway
                               * (secondway - 1)) / 2;

                    // Adding ways for all possible x
                    total += answer;
                    count = 0;
                }
            }
        }
    }

    return total;
}

// Driver code
int main()
{
    string test = "13134422";
    cout << solve(test) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Implementation of above approach
import java.io.*;

class GFG
{

// Function to return the total
// required sub-sequences
static int solve(String test, int MOD)
{
    int size = test.length();
    int total = 0;

    // Find ways for all values of x
    for (int i = 0; i <= 8; i++)
    {
        int x = i;

        // x+1
        int y = i + 1;
        String newtest = "";

        // Removing all unnecessary digits
        for (int j = 0; j < size; j++)
        {
            if (test.charAt(j) == x + 48 || test.charAt(j) == y + 48)
            {
                newtest += test.charAt(j);
            }
        }

        if (newtest.length() > 0) {
            int size1 = newtest.length();

            // Prefix Sum Array for X+1 digit
            int []prefix = new int[size1];
            for (int j = 0; j < size1; j++)
            {
                prefix[j] = 0;
                if (newtest.charAt(j) == y + 48)
                {
                    prefix[j]++;
                }
            }

            for (int j = 1; j < size1; j++)
            {
                prefix[j] += prefix[j - 1];
            }

            int count = 0;
            int firstcount = 0;

            // Sum of squares
            int ss = 0;

            // Previous sum of all possible pairs
            int prev = 0;

            for (int j = 0; j < size1; j++)
            {
                if (newtest.charAt(j) == x + 48)
                {
                    count++;
                    firstcount++;
                }
                else
                {

                    ss += count * count;

                    // To find sum of multiplication of all
                    // possible pairs
                    int pairsum = (firstcount * firstcount - ss) / 2;
                    int temp = pairsum;

                    // To prevent overcounting
                    pairsum -= prev;
                    prev = temp;

                    int secondway = prefix[size1 - 1];
                    if (j != 0)
                        secondway -= prefix[j - 1];

                    int answer = count * (count - 1)
                                * secondway * (secondway - 1);
                    answer /= 4;
                    answer += (pairsum * secondway
                            * (secondway - 1)) / 2;

                    // Adding ways for all possible x
                    total += answer;
                    count = 0;
                }
            }
        }
    }

    return total;
}

// Driver code
public static void main (String[] args)
{
    String test = "13134422";
    int MOD = 1000000007;
    System.out.println(solve(test,MOD));

}
}

// This code is contributed by krikti..
```

## 蟒蛇 3

```
# Python3 implementation of the approach

MOD= 1000000007

# Function to return the total
# required sub-sequences
def solve(test):

    size = len(test)
    total = 0

    # Find ways for all values of x
    for i in range(9):
        x = i

        # x+1
        y = i + 1
        newtest=""

        # Removing all unnecessary digits
        for j in range(size):
            if (ord(test[j]) == x + 48 or ord(test[j]) == y + 48):
                newtest += test[j]

        if (len(newtest) > 0):
            size1 = len(newtest)

            # Prefix Sum Array for X+1 digit
            prefix=[0 for i in range(size1)]

            for j in range(size1):
                if (ord(newtest[j]) == y + 48):
                    prefix[j]+=1

            for j in range(1,size1):
                prefix[j] += prefix[j - 1]

            count = 0
            firstcount = 0

            # Sum of squares
            ss = 0

            # Previous sum of all possible pairs
            prev = 0

            for j in range(size1):
                if (ord(newtest[j]) == x + 48):
                    count+=1
                    firstcount+=1

                else:

                    ss += count * count

                    # To find sum of multiplication of all
                    # possible pairs
                    pairsum = (firstcount * firstcount - ss) // 2
                    temp = pairsum

                    # To prevent overcounting
                    pairsum -= prev
                    prev = temp

                    secondway = prefix[size1 - 1]
                    if (j != 0):
                        secondway -= prefix[j - 1]

                    answer = count * (count - 1)* secondway * (secondway - 1)
                    answer //= 4
                    answer += (pairsum * secondway * (secondway - 1)) // 2

                    # Adding ways for all possible x
                    total += answer
                    count = 0

    return total

# Driver code
test = "13134422"
print(solve(test))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# Implementation of above approach

using System;

class GFG
{

    // Function to return the total
    // required sub-sequences
    static int solve(string test, int MOD)
    {
        int size = test.Length;
        int total = 0;

        // Find ways for all values of x
        for (int i = 0; i <= 8; i++)
        {
            int x = i;

            // x+1
            int y = i + 1;
            string newtest = "";

            // Removing all unnecessary digits
            for (int j = 0; j < size; j++)
            {
                if (test[j] == x + 48 || test[j] == y + 48)
                {
                    newtest += test[j];
                }
            }

            if (newtest.Length > 0) {
                int size1 = newtest.Length;

                // Prefix Sum Array for X+1 digit
                int []prefix = new int[size1];
                for (int j = 0; j < size1; j++)
                {
                    prefix[j] = 0;
                    if (newtest[j] == y + 48)
                    {
                        prefix[j]++;
                    }
                }

                for (int j = 1; j < size1; j++)
                {
                    prefix[j] += prefix[j - 1];
                }

                int count = 0;
                int firstcount = 0;

                // Sum of squares
                int ss = 0;

                // Previous sum of all possible pairs
                int prev = 0;

                for (int j = 0; j < size1; j++)
                {
                    if (newtest[j] == x + 48)
                    {
                        count++;
                        firstcount++;
                    }
                    else
                    {

                        ss += count * count;

                        // To find sum of multiplication of all
                        // possible pairs
                        int pairsum = (firstcount * firstcount - ss) / 2;
                        int temp = pairsum;

                        // To prevent overcounting
                        pairsum -= prev;
                        prev = temp;

                        int secondway = prefix[size1 - 1];
                        if (j != 0)
                            secondway -= prefix[j - 1];

                        int answer = count * (count - 1)
                                    * secondway * (secondway - 1);
                        answer /= 4;
                        answer += (pairsum * secondway
                                * (secondway - 1)) / 2;

                        // Adding ways for all possible x
                        total += answer;
                        count = 0;
                    }
                }
            }
        }

        return total;
    }

    // Driver code
    public static void Main ()
    {
        string test = "13134422";
        int MOD = 1000000007;
        Console.WriteLine(solve(test,MOD));

    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// JavaScript Implementation of above approach

    // Function to return the total
   // required sub-sequences
    function solve(test,MOD)
    {
        let size = test.length;
    let total = 0;

    // Find ways for all values of x
    for (let i = 0; i <= 8; i++)
    {
        let x = i;

        // x+1
        let y = i + 1;
        let newtest = "";

        // Removing all unnecessary digits
        for (let j = 0; j < size; j++)
        {
            if (test[j].charCodeAt(0) == x + 48 ||
                test[j].charCodeAt(0) == y + 48)
            {
                newtest += test[j];
            }
        }

        if (newtest.length > 0) {
            let size1 = newtest.length;

            // Prefix Sum Array for X+1 digit
            let prefix = new Array(size1);
            for (let j = 0; j < size1; j++)
            {
                prefix[j] = 0;
                if (newtest[j].charCodeAt(0) == y + 48)
                {
                    prefix[j]++;
                }
            }

            for (let j = 1; j < size1; j++)
            {
                prefix[j] += prefix[j - 1];
            }

            let count = 0;
            let firstcount = 0;

            // Sum of squares
            let ss = 0;

            // Previous sum of all possible pairs
            let prev = 0;

            for (let j = 0; j < size1; j++)
            {
                if (newtest[j].charCodeAt(0) == x + 48)
                {
                    count++;
                    firstcount++;
                }
                else
                {

                    ss += count * count;

                    // To find sum of multiplication of all
                    // possible pairs
                    let pairsum =
            Math.floor((firstcount * firstcount - ss) / 2);
                    let temp = pairsum;

                    // To prevent overcounting
                    pairsum -= prev;
                    prev = temp;

                    let secondway = prefix[size1 - 1];
                    if (j != 0)
                        secondway -= prefix[j - 1];

                    let answer = count * (count - 1)
                                * secondway * (secondway - 1);
                    answer = Math.floor(answer/4);
                    answer += Math.floor((pairsum * secondway
                            * (secondway - 1)) / 2);

                    // Adding ways for all possible x
                    total += answer;
                    count = 0;
                }
            }
        }
    }

    return total;
    }

    // Driver code
    let test = "13134422";
    let MOD = 1000000007;
    document.write(solve(test,MOD));

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
2
```