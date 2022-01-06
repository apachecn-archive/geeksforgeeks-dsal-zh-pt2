# 出现在给定范围内的次数至少为-K 次

> 原文:[https://www . geesforgeks . org/出现在给定范围内的数字计数-至少 k 次/](https://www.geeksforgeeks.org/count-of-numbers-appearing-in-the-given-ranges-at-least-k-times/)

给定 N 个范围和一个数字 K，任务是找出在给定范围内出现至少 K 次的数字的总数。

**示例**:

> **输入:**
> N = 3，K = 2
> 范围 1:【91，94】
> 范围 2:【92，97】
> 范围 3:【97，99】
> **输出:** 4
> **说明:**范围为 91 到 94，92 到 97，97 到 99，至少出现 2 次的数字为 92，93，94，97。
> 
> **输入:**
> N = 2，K = 3
> 范围 1 =【1，4】
> 范围 2 =【5，9】
> **输出:** 0
> **说明:**给定范围内无元素出现 3 次。

[Recommended: Please try your approach on ***<u>{IDE}</u>*** first, before moving on to the solution.](https://ide.geeksforgeeks.org/)

**天真方法**:天真的方法是遍历每个范围，增加每个元素的计数，最后检查每个元素的计数是否满足要求的值。
以下是上述办法的实施情况:

## C++

```
// C++ brute-force program to find count of
// numbers appearing in the given
// ranges at-least K times
#include <bits/stdc++.h>
using namespace std;

// Function to find the no of occurrence
int countNumbers(int n, int k, int rangeLvalue[],
                              int rangeRvalue[])
{
    int count = 0;

    // Map to store frequency of elements
    // in the range
    map<int, int> freq;

    for (int i = 0; i < n; i++) {

        // increment the value of the elements
        // in all of the ranges
        for (int j = rangeLvalue[i]; j <= rangeRvalue[i]; j++)
        {
            if (freq.find(j) == freq.end())
                freq.insert(make_pair(j, 1));
            else
                freq[j]++;
        }
    }

    // Traverse the map to check the frequency
    // of numbers greater than equals to k
    for (auto itr = freq.begin(); itr != freq.end(); itr++)
    {

        // check if a number appears atleast k times
        if ((*itr).second >= k) {

            // increase the counter
            // if condition satisfies
            count++;
        }
    }

    // return the result
    return count;
}

// Driver Code
int main()
{
    int n = 3, k = 2;
    int rangeLvalue[] = { 91, 92, 97 };
    int rangeRvalue[] = { 94, 97, 99 };
    cout << countNumbers(n, k, rangeLvalue, rangeRvalue);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java brute-force program to find count of
// numbers appearing in the given
// ranges at-least K times
import java.io.*;
import java.util.*;

class GFG
{

    // Function to find the no of occurrence
    static int countNumbers(int n, int k, int[] rangeLvalue,
                                            int[] rangeRvalue)
    {
        int count = 0;

        // Map to store frequency of elements
        // in the range
        HashMap<Integer, Integer> freq = new HashMap<>();

        // increment the value of the elements
        // in all of the ranges
        for (int i = 0; i < n; i++)
        {
            for (int j = rangeLvalue[i]; j <= rangeRvalue[i]; j++)
            {
                if (!freq.containsKey(j))
                    freq.put(j, 1);
                else
                    freq.put(j, freq.get(j) + 1);
            }
        }

        // Traverse the map to check the frequency
        // of numbers greater than equals to k
        for (HashMap.Entry<Integer, Integer> entry : freq.entrySet())
        {

            // check if a number appears atleast k times
            if (entry.getValue() >= k)

                // increase the counter
                // if condition satisfies
                count++;
        }

        // return the result
        return count;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 3, k = 2;
        int[] rangeLvalue = {91, 92, 97};
        int[] rangeRvalue = {94, 97, 99};
        System.out.println(countNumbers(n, k, rangeLvalue, rangeRvalue));
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 brute-force program to find
# count of numbers appearing in the
# given ranges at-least K times

# Function to find the no of occurrence
def countNumbers(n, k, rangeLvalue,    
                       rangeRvalue):

    count = 0

    # Map to store frequency of elements
    # in the range
    freq = dict()

    for i in range(n):

        # increment the value of the elements
        # in all of the ranges
        for j in range(rangeLvalue[i],
                       rangeRvalue[i] + 1):
            freq[j] = freq.get(j, 0) + 1

    # Traverse the map to check the frequency
    # of numbers greater than equals to k
    for itr in freq:

        # check if a number appears
        # atleast k times
        if (freq[itr] >= k):

            # increase the counter
            # if condition satisfies
            count += 1

    # return the result
    return count

# Driver Code
n, k = 3, 2
rangeLvalue = [91, 92, 97]
rangeRvalue = [94, 97, 99]
print(countNumbers(n, k, rangeLvalue,
                         rangeRvalue))

# This code is contributed by mohit kumar
```

## C#

```
// C# brute-force program to find count of
// numbers appearing in the given
// ranges at-least K times
using System;
using System.Collections.Generic;

class GFG
{

    // Function to find the no of occurrence
    static int countNumbers(int n, int k, int[] rangeLvalue,
                                            int[] rangeRvalue)
    {
        int count = 0;

        // Map to store frequency of elements
        // in the range
        Dictionary<int, int> freq = new Dictionary<int, int>();

        // increment the value of the elements
        // in all of the ranges
        for (int i = 0; i < n; i++)
        {
            for (int j = rangeLvalue[i]; j <= rangeRvalue[i]; j++)
            {
                if (!freq.ContainsKey(j))
                    freq.Add(j, 1);
                else
                    freq[j] = freq[j] + 1;
            }
        }

        // Traverse the map to check the frequency
        // of numbers greater than equals to k
        foreach(KeyValuePair<int, int> entry in freq)
        {

            // check if a number appears atleast k times
            if (entry.Value >= k)

                // increase the counter
                // if condition satisfies
                count++;
        }

        // return the result
        return count;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int n = 3, k = 2;
        int[] rangeLvalue = {91, 92, 97};
        int[] rangeRvalue = {94, 97, 99};
        Console.WriteLine(countNumbers(n, k, rangeLvalue, rangeRvalue));
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript brute-force program to find count of
// numbers appearing in the given
// ranges at-least K times

    // Function to find the no of occurrence
    function countNumbers(n,k,rangeLvalue,rangeRvalue)
    {
        let count = 0;

        // Map to store frequency of elements
        // in the range
        let freq = new Map();

        // increment the value of the elements
        // in all of the ranges
        for (let i = 0; i < n; i++)
        {
            for (let j = rangeLvalue[i];
            j <= rangeRvalue[i]; j++)
            {
                if (!freq.has(j))
                    freq.set(j, 1);
                else
                    freq.set(j, freq.get(j) + 1);
            }
        }

        // Traverse the map to check the frequency
        // of numbers greater than equals to k
        for (let [key, value] of freq.entries())
        {

            // check if a number appears atleast k times
            if (value >= k)

                // increase the counter
                // if condition satisfies
                count++;
        }

        // return the result
        return count;
    }

     // Driver Code
    let n = 3, k = 2;
    let rangeLvalue=[91, 92, 97];
    let rangeRvalue =[94, 97, 99];

    document.write(countNumbers(n, k, rangeLvalue,
    rangeRvalue));

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
4
```

**高效解决方案**:更好的解决方案是通过递增范围最左边元素的值和递减计数器数组中给定范围最右边元素的下一个元素来跟踪范围。对所有范围都这样做。这样做是因为它给出了一个数在给定范围内进行预求和的次数。
以下是上述办法的实施情况。

## C++

```
// C++ efficient program to find count of
// numbers appearing in the given
// ranges at-least K times
#include <bits/stdc++.h>
using namespace std;

// Function to find the no of occurrence
int countNumbers(int n, int k, int rangeLvalue[],
                              int rangeRvalue[])
{
    int count = 0;

    // maximum value of the range
    int maxn = INT_MIN;
    for (int i = 0; i < n; i++)
        if (rangeRvalue[i] > maxn)
            maxn = rangeRvalue[i];

    // counter array
    int preSum[maxn + 5] = { 0 };

    // incrementing and decrementing the
    // leftmost and next value of rightmost value
    // of each range by 1 respectively
    for (int i = 0; i < n; i++) {
        preSum[rangeLvalue[i]]++;
        preSum[rangeRvalue[i] + 1]--;
    }

    // presum gives the no of occurrence of
    // each element
    for (int i = 1; i <= maxn; i++) {
        preSum[i] += preSum[i - 1];
    }

    for (int i = 1; i <= maxn; i++) {

        // check if the number appears atleast k times
        if (preSum[i] >= k) {

            // increase the counter if
            // condition satisfies
            count++;
        }
    }

    // return the result
    return count;
}

// Driver Code
int main()
{
    int n = 3, k = 2;

    int rangeLvalue[] = { 91, 92, 97 };
    int rangeRvalue[] = { 94, 97, 99 };

    cout << countNumbers(n, k, rangeLvalue, rangeRvalue);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java efficient program to find count of
// numbers appearing in the given
// ranges at-least K times
class Geeks {

// Function to find the no of occurrence
static int countNumbers(int n, int k, int rangeLvalue[],
                                     int rangeRvalue[])
{
    int count = 0;

    // maximum value of the range
    int maxn = Integer.MIN_VALUE;
    for (int i = 0; i < n; i++)
        if (rangeRvalue[i] > maxn)
            maxn = rangeRvalue[i];

    // counter array
    int preSum[] = new int[maxn + 5];
    for(int i = 0; i < (maxn + 5); i++)
    preSum[i] = 0;

    // incrementing and decrementing the
    // leftmost and next value of rightmost value
    // of each range by 1 respectively
    for (int i = 0; i < n; i++)
    {
        preSum[rangeLvalue[i]]++;
        preSum[rangeRvalue[i] + 1]--;
    }

    // presum gives the no of occurrence of
    // each element
    for (int i = 1; i <= maxn; i++) {
        preSum[i] += preSum[i - 1];
    }

    for (int i = 1; i <= maxn; i++) {

        // check if the number appears atleast k times
        if (preSum[i] >= k) {

            // increase the counter if
            // condition satisfies
            count++;
        }
    }

    // return the result
    return count;
}

// Driver Code
public static void main(String args[])
{
    int n = 3, k = 2;

    int rangeLvalue[] = { 91, 92, 97 };
    int rangeRvalue[] = { 94, 97, 99 };

    System.out.println(countNumbers(n, k, rangeLvalue,
                                        rangeRvalue));

}
}

// This code is contributed by ankita_saini
```

## 计算机编程语言

```
# Python efficient program to find count of
# numbers appearing in the given
# ranges at-least K times

# Function to find the no of occurrence
def countNumbers(n, k, rangeLvalue, rangeRvalue):
    count = 0

    # maximum value of the range
    maxn = -float('inf')
    for i in range(n):
        if rangeRvalue[i] > maxn:
            maxn = rangeRvalue[i]

    # counter array
    preSum = [0]*(maxn + 5)

    # incrementing and decrementing the
    # leftmost and next value of rightmost value
    # of each range by 1 respectively
    for i in range(n):
        preSum[rangeLvalue[i]] += 1
        preSum[rangeRvalue[i] + 1] -= 1

    # presum gives the no of occurrence of
    # each element
    for i in range(1, maxn+1):
        preSum[i] += preSum[i - 1]

    for i in range(1, maxn+1):

        # check if the number appears atleast k times
        if preSum[i] >= k:

            # increase the counter if
            # condition satisfies
            count += 1

    # return the result
    return count

# Driver Code
n = 3
k = 2

rangeLvalue = [91, 92, 97]
rangeRvalue = [94, 97, 99]

print(countNumbers(n, k, rangeLvalue, rangeRvalue))

# This code is contributed by ankush_953
```

## C#

```
// C# efficient program to
// find count of numbers
// appearing in the given
// ranges at-least K times
using System;

class GFG
{

// Function to find the
// no of occurrence
static int countNumbers(int n, int k,
                        int []rangeLvalue,
                        int []rangeRvalue)
{
    int count = 0;

    // maximum value of the range
    int maxn = Int32.MinValue;
    for (int i = 0; i < n; i++)
        if (rangeRvalue[i] > maxn)
            maxn = rangeRvalue[i];

    // counter array
    int []preSum = new int[maxn + 5];
    for(int i = 0; i < (maxn + 5); i++)
    preSum[i] = 0;

    // incrementing and decrementing
    // the leftmost and next value
    // of rightmost value of each
    // range by 1 respectively
    for (int i = 0; i < n; i++)
    {
        preSum[rangeLvalue[i]]++;
        preSum[rangeRvalue[i] + 1]--;
    }

    // presum gives the no of
    // occurrence of each element
    for (int i = 1; i <= maxn; i++)
    {
        preSum[i] += preSum[i - 1];
    }

    for (int i = 1; i <= maxn; i++)
    {

        // check if the number
        // appears atleast k times
        if (preSum[i] >= k)
        {

            // increase the counter if
            // condition satisfies
            count++;
        }
    }

    // return the result
    return count;
}

// Driver Code
public static void Main(String []args)
{
    int n = 3, k = 2;

    int []rangeLvalue = { 91, 92, 97 };
    int []rangeRvalue = { 94, 97, 99 };

    Console.WriteLine(countNumbers(n, k, rangeLvalue,
                                        rangeRvalue));
}
}

// This code is contributed
// by ankita_saini
```

## java 描述语言

```
<script>

// Javascript efficient program to find count of
// numbers appearing in the given
// ranges at-least K times

// Function to find the no of occurrence
function countNumbers(n, k, rangeLvalue, rangeRvalue)
{
    var count = 0;

    // maximum value of the range
    var maxn = -1000000000;
    for (var i = 0; i < n; i++)
        if (rangeRvalue[i] > maxn)
            maxn = rangeRvalue[i];

    // counter array
    var preSum = Array(maxn +5).fill(0);

    // incrementing and decrementing the
    // leftmost and next value of rightmost value
    // of each range by 1 respectively
    for (var i = 0; i < n; i++) {
        preSum[rangeLvalue[i]]++;
        preSum[rangeRvalue[i] + 1]--;
    }

    // presum gives the no of occurrence of
    // each element
    for (var i = 1; i <= maxn; i++) {
        preSum[i] += preSum[i - 1];
    }

    for (var i = 1; i <= maxn; i++) {

        // check if the number appears atleast k times
        if (preSum[i] >= k) {

            // increase the counter if
            // condition satisfies
            count++;
        }
    }

    // return the result
    return count;
}

// Driver Code
var n = 3, k = 2;
var rangeLvalue = [91, 92, 97];
var rangeRvalue = [94, 97, 99];
document.write( countNumbers(n, k, rangeLvalue, rangeRvalue));

</script>
```

**Output:** 

```
4
```

**时间-复杂度**:O(N+max(rangeRvalue[])
**辅助-空间** : O(N)