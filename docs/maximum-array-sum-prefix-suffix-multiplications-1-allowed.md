# 允许前缀和后缀相乘的最大数组和为-1

> 原文:[https://www . geesforgeks . org/maximum-array-sum-prefix-后缀-乘法-1-允许/](https://www.geeksforgeeks.org/maximum-array-sum-prefix-suffix-multiplications-1-allowed/)

给定 N 个元素(正的和负的)。求最大和，前提是第一个操作是取序列的某个前缀，并将这个前缀中的所有数字乘以-1。第二个操作是取一些后缀，将其中的所有数字乘以-1。所选前缀和后缀可能相交。通过应用所描述的操作，可以获得序列的最大总和是多少？

**示例:**

```
Input : -1 -2 -3
Output : 6 
Explanation: Multiply prefix {-1, -2} with -1.
Multiply suffix {-3} with -1\. We get total 
sum as 1 + 2 + 3 = 6

Input : -1 10 -5 10 -2
Output : 18
Explanation: Multiply -1 with prefix {-1} and
multiply -1 with suffix {-2}. Elements after 
multiplying {1, 10, -5, 10, 2} and sum is
1 + 10 -5 + 10 + 2 = 18.

Input: -4 2 0 5 0
Output:  11 
Explanation: Multiply {-4} with -1\. Do not
multiply anything in the suffix, so we get 
{4, 2, 0, 5, 0} to get sum as 11\. 
```

如果期望的前缀和后缀相交，那么它们的公共部分仍然是初始符号，因此，这种情况相当于我们取相同的后缀和前缀，但没有它们的公共部分的情况。
我们从左向右遍历，通过乘以-1 看看 sum 或-sum 在任何一步是否更多，并在任何一个索引处存储 pre_sum 和-pre_sum 的最大值，对所有元素继续这个过程。
然后我们从头到尾遍历，检查谁的和比我们得到的(该索引处的前缀和+负和)或之前的最大值大，如果我们发现在任何索引处，该索引处的负和+前缀和在任何步骤都比它大，那么我们将 ans 替换为 sum *(1)+pre _ sum。

## C++

```
// CPP program to find maximum array sum
// with multiplications of a prefix and a
// suffix with -1 allowed.
#include <iostream>
using namespace std;

// function to maximize the sum
int maximize(int a[], int n)
{  
    // stores the pre sum
    int presum[n];

    // to store sum from 0 to i
    int sum = 0;

    // stores the maximum sum with
    // prefix multiplication with -1.
    int max_sum = 0;

    // traverse from 0 to n
    for (int i = 0; i<n ; i++)
    {
        // calculate the presum
        presum[i] = max_sum ;

        // calculate sum
        max_sum  += a[i];
        sum += a[i]; 

        max_sum  = max(max_sum, -sum);
    }

    // Initialize answer.
    int ans = max(sum, max_sum);   

    // traverse from back to start
    int g = 0;
    for (int i = n-1; i >= 0; --i)
    {
        // stores the sum multiplied by (-1)
        g -= a[i];

        // stores the max of ans and
        // presum + (-1*negative sum);
        ans = max(ans, g + presum[i]);
    }

    // returns answer
    return ans;
}

// driver program to test the above function
int main() {

    int a[] = {-4, 2, 0, 5, 0};
    int n = sizeof(a)/sizeof(a[0]);
    cout << maximize(a, n);    
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to find maximum array sum
// with multiplications of a prefix and a
// suffix with -1 allowed.

import java.math.*;
class GFG {

    // function to maximize the sum
    static int maximize(int a[], int n)
    {  
        // stores the pre sum
        int presum[] =new int[n];

        // to store sum from 0 to i
        int sum = 0;

        // stores the maximum sum with
        // prefix multiplication with -1.
        int max_sum = 0;

        // traverse from 0 to n
        for (int i = 0; i<n ; i++)
        {
            // calculate the presum
            presum[i] = max_sum ;

            // calculate sum
            max_sum  += a[i];
            sum += a[i]; 

            max_sum  = Math.max(max_sum, -sum);
        }

        // Initialize answer.
        int ans = Math.max(sum, max_sum);   

        // traverse from back to start
        int g = 0;
        for (int i = n-1; i >= 0; --i)
        {
            // stores the sum multiplied by (-1)
            g -= a[i];

            // stores the max of ans and
            // presum + (-1*negative sum);
            ans = Math.max(ans, g + presum[i]);
        }

        // returns answer
        return ans;
    }

    // driver program to test the above function
    public static void main(String args[]) {

        int a[] = {-4, 2, 0, 5, 0};
        int n = a.length;
        System.out.println(maximize(a, n));    
    }
}

/*This code is contributed by Nikita Tiwari.*/
```

## 蟒蛇 3

```
# Python 3 program to find maximum array
# sum with multiplications of a prefix
# and a suffix with -1 allowed.

# function to maximize the sum
def maximize(a,n) :

    # stores the pre sum
    presum = [0] * n

    # to store sum from 0 to i
    sm = 0

    # stores the maximum sum with
    # prefix multiplication with -1.
    max_sum = 0

    # traverse from 0 to n
    for i in range(0,n) :

        # calculate the presum
        presum[i] = max_sum

        # calculate sum
        max_sum  =max_sum + a[i]
        sm = sm + a[i]

        max_sum  = max(max_sum, -sm)

    # Initialize answer.
    ans = max(sm, max_sum)

    # traverse from back to start
    g = 0
    for i in range(n-1,-1,-1) :
        # stores the sum multiplied by (-1)
        g = g - a[i]

        # stores the max of ans and
        # presum + (-1*negative sum);
        ans = max(ans, g + presum[i])

    # returns answer
    return ans

# driver program to test the above function
a = [-4, 2, 0, 5, 0]
n = len(a)
print(maximize(a, n))

#This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to find maximum array sum
// with multiplications of a prefix and a
// suffix with -1 allowed.
using System;

class GFG
{

    // function to maximize the sum
    static int maximize(int []a, int n)
    {
        // stores the pre sum
        int []presum =new int[n];

        // to store sum from 0 to i
        int sum = 0;

        // stores the maximum sum with
        // prefix multiplication with -1.
        int max_sum = 0;

        // traverse from 0 to n
        for (int i = 0; i < n ; i++)
        {
            // calculate the presum
            presum[i] = max_sum ;

            // calculate sum
            max_sum += a[i];
            sum += a[i];

            max_sum = Math.Max(max_sum,
                               -sum);
        }

        // Initialize answer.
        int ans = Math.Max(sum, max_sum);

        // traverse from back to start
        int g = 0;
        for (int i = n - 1; i >= 0; --i)
        {
            // stores the sum multiplied by (-1)
            g -= a[i];

            // stores the max of ans and
            // presum + (-1*negative sum);
            ans = Math.Max(ans, g + presum[i]);
        }

        // returns answer
        return ans;
    }

    // Driver Code
    public static void Main()
    {

        int []a = {-4, 2, 0, 5, 0};
        int n = a.Length;
        Console.WriteLine(maximize(a, n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find maximum array sum
// with multiplications of a prefix and a
// suffix with -1 allowed.

// function to maximize the sum
function maximize($a, $n)
{

    // stores the pre sum
    $presum = array();

    // to store sum
    // from 0 to i
    $sum = 0;

    // stores the maximum
    // sum with prefix
    // multiplication with -1.
    $max_sum = 0;

    // traverse from 0 to n
    for ($i = 0; $i < $n ; $i++)
    {

        // calculate the presum
        $presum[$i] = $max_sum ;

        // calculate sum
        $max_sum += $a[$i];
        $sum += $a[$i];

        $max_sum = max($max_sum, -$sum);
    }

    // Initialize answer.
    $ans = max($sum, $max_sum);

    // traverse from
    // back to start
    $g = 0;
    for ($i = $n - 1; $i >= 0; --$i)
    {

        // stores the sum
        // multiplied by (-1)
        $g -= $a[$i];

        // stores the max of ans and
        // presum + (-1*negative sum);
        $ans = max($ans, $g + $presum[$i]);
    }

    // returns answer
    return $ans;
}

    // Driver Code
    $a = array(-4, 2, 0, 5, 0);
    $n = count($a);
    echo maximize($a, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
// javascript program to find maximum array sum
// with multiplications of a prefix and a
// suffix with -1 allowed.

    // function to maximize the sum
    function maximize(a , n) {
        // stores the pre sum
        var presum = Array(n).fill(0);

        // to store sum from 0 to i
        var sum = 0;

        // stores the maximum sum with
        // prefix multiplication with -1.
        var max_sum = 0;

        // traverse from 0 to n
        for (i = 0; i < n; i++) {
            // calculate the presum
            presum[i] = max_sum;

            // calculate sum
            max_sum += a[i];
            sum += a[i];

            max_sum = Math.max(max_sum, -sum);
        }

        // Initialize answer.
        var ans = Math.max(sum, max_sum);

        // traverse from back to start
        var g = 0;
        for (i = n - 1; i >= 0; --i) {
            // stores the sum multiplied by (-1)
            g -= a[i];

            // stores the max of ans and
            // presum + (-1*negative sum);
            ans = Math.max(ans, g + presum[i]);
        }

        // returns answer
        return ans;
    }

    // driver program to test the above function

        var a = [ -4, 2, 0, 5, 0 ];
        var n = a.length;
        document.write(maximize(a, n));

// This code is contributed by todaysgaurav
</script>
```

**输出:**

```
11
```

**时间复杂度:** O(n)