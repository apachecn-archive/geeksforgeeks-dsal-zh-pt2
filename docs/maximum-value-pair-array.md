# 数组中一对的最大与值

> 原文:[https://www.geeksforgeeks.org/maximum-value-pair-array/](https://www.geeksforgeeks.org/maximum-value-pair-array/)

给我们一个 n 个正元素的数组。我们需要找到数组中任意一对元素产生的最大 AND 值。“与”是按位&运算符。

示例:

```
Input : arr[] = {4, 8, 12, 16}
Output : Maximum AND value = 8

Input : arr[] = {4, 8, 16, 2}
Output : Maximum AND value = 0
```

**天真法:**基本法与[最大异或值相同。](https://www.geeksforgeeks.org/minimum-xor-value-pair/)我们迭代所有可能的对，并计算所有对的“与”值。从中选出最大值。这个解决方案的时间复杂度是 O(n^2).

## C++

```
// CPP Program to find maximum XOR value of a pair
#include<bits/stdc++.h>
using namespace std;

// Function for finding maximum and value pair
int maxAND(int arr[], int n)
{
    int res = 0;
    for (int i=0; i<n; i++)
       for (int j=i+1; j<n; j++)
          res = max(res, arr[i] & arr[j]);

    return res;
}

// Driver function
int main()
{
    int arr[] = {4, 8, 6, 2};
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << "Maximum AND Value = " << maxAND(arr,n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find maximum
// XOR value of a pair
import java.util.*;
import java.lang.*;

public class GfG{

// Function for finding maximum
// and value pair
static int maxAND(int arr[], int n)
{
    int res = 0;
    for (int i = 0; i < n; i++)
    for (int j = i + 1; j < n; j++)
        res = res > ( arr[i] & arr[j]) ?
              res : ( arr[i] & arr[j]);

    return res;
}

// driver function
public static void main(String argc[])
{
    int arr[] = {4, 8, 6, 2};
    int n = arr.length;
    System.out.println("Maximum AND Value = " +
                       maxAND(arr,n));
}
}

// This code is contributed by Prerna Saini
```

## 蟒蛇 3

```
# Python3 Program to find maximum XOR
# value of a pair

# Function for finding maximum and value pair
def maxAND(arr, n) :
    res = 0

    for i in range(0, n) :
        for j in range(i + 1, n) :
            res = max(res, arr[i] & arr[j])

    return res

# Driver function
arr = [4, 8, 6, 2]
n = len(arr)
print("Maximum AND Value = ", maxAND(arr,n))

# This code is contributed by Nikita Tiwari. 
```

## C#

```
// C# Program to find maximum
// XOR value of a pair
using System;

public class GfG
{

// Function for finding maximum
// and value pair
static int maxAND(int []arr, int n)
{
    int res = 0;
    for (int i = 0; i < n; i++)
    for (int j = i + 1; j < n; j++)
        res = res > ( arr[i] & arr[j]) ?
              res : ( arr[i] & arr[j]);

    return res;
}

// Driver code
public static void Main()
{
    int []arr = {4, 8, 6, 2};
    int n = arr.Length;
    Console.WriteLine("Maximum AND Value = " +
                       maxAND(arr, n));
}
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find maximum
// XOR value of a pair

// Function for finding
// maximum and value pair
function maxAND($arr, $n)
{

    $res = 0;
    for ($i = 0; $i < $n; $i++)
    for ($j = $i + 1; $j < $n; $j++)
        $res = max($res, $arr[$i] &
                         $arr[$j]);

    return $res;
}

    // Driver Code
    $arr = array(4, 8, 6, 2);
    $n = count($arr);
    echo "Maximum AND Value = " , maxAND($arr, $n);

// This code is contributed by vt_m.
?>
```

## java 描述语言

```
<script>

// Javascript Program to find maximum XOR value of a pair

// Function for finding maximum and value pair
function maxAND(arr, n)
{
    var res = 0;
    for (var i=0; i<n; i++)
       for (var j=i+1; j<n; j++)
          res = Math.max(res, arr[i] & arr[j]);

    return res;
}

// Driver function
var arr = [4, 8, 6, 2];
var n = arr.length;
document.write( "Maximum AND Value = " + maxAND(arr,n));

</script>
```

输出:

```
Maximum AND Value = 4
```

**更好的方法:**思想基于 AND 算子的性质。如果两个位都是 1，则任意两个位的“与”运算得到 1。我们从 MSB 开始，检查数组中是否至少有两个元素具有设定值。如果是，那么该 MSB 将成为我们解决方案的一部分，并被添加到结果中，否则我们将丢弃该位。类似地，从 MSB 到 LSB (32 比 1)的位位置迭代，我们可以很容易地检查哪个位将是我们解决方案的一部分，并将继续将所有这样的位添加到我们的解决方案中。

**解释:**让我们考虑{4，8，12，16}的第一个例子:

> **第 1 步**:写入每个元素的位表示:
> 4 = 100，8 = 1000，12 = 1100，16 = 10000
> **第 2 步**:检查第一个 MSB，模式= 0 + 16 = 16。现在，16 中的第 5 位被设置，但没有其他元素有 5 位作为设置位，因此这不会增加我们的 RES，仍然是 RES = 0 和模式= 0
> **步骤 3:** 检查第 4 位，模式= 0 + 8 = 8。现在 8 和 12 都在第 4 位位置设置了位，这样在我们的解决方案中相加，RES = 8，pattern = 8
> **步骤 4:** 检查第 3 位，pattern = 8 + 4 = 12。现在只有 12 位同时设置了位(与模式相同)，所以我们将丢弃第 3 位，RES = 8，模式= 8
> **步骤 5:** 检查第 2 位，模式= 8 + 2 = 10。没有元素设置了与模式相同的位，因此我们将丢弃第二位，RES = 8，模式= 8
> **步骤 4:** 检查第一位，模式= 8 + 1 = 9。没有元素设置了与模式相同的位，因此我们将丢弃第一位，RES = 8 和模式= 8

## C++

```
// CPP Program to find maximum XOR value of a pair
#include<bits/stdc++.h>
using namespace std;

// Utility function to check number of elements
// having set msb as of pattern
int checkBit(int pattern, int arr[], int n)
{
    int count = 0;
    for (int i = 0; i < n; i++)
        if ((pattern & arr[i]) == pattern)
            count++;
    return count;
}

// Function for finding maximum and value pair
int maxAND (int arr[], int n)
{
    int res = 0, count;

    // iterate over total of 32bits from msb to lsb
    for (int bit = 31; bit >= 0; bit--)
    {
        // find the count of element having set  msb
        count = checkBit(res | (1 << bit),arr,n);

        // if count >= 2 set particular bit in result
        if ( count >= 2 )       
            res |= (1 << bit);       
    }

    return res;
}

// Driver function
int main()
{
    int arr[] = {4, 8, 6, 2};
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << "Maximum AND Value = " << maxAND(arr,n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find maximum
// XOR value of a pair
import java.util.*;
import java.lang.*;

public class GfG{

// Utility function to check number of elements
// having set msb as of pattern
static int checkBit(int pattern, int arr[], int n)
{
    int count = 0;
    for (int i = 0; i < n; i++)
        if ((pattern & arr[i]) == pattern)
            count++;
    return count;
}

// Function for finding maximum and value pair
static int maxAND (int arr[], int n)
{
    int res = 0, count;

    // iterate over total of 32bits
    // from msb to lsb
    for (int bit = 31; bit >= 0; bit--)
    {
        // find the count of element
        // having set msb
        count = checkBit(res | (1 << bit), arr, n);

        // if count >= 2 set particular
        // bit in result
        if ( count >= 2 )    
            res |= (1 << bit);    
    }

    return res;
}

// driver function
public static void main(String argc[])
{
    int arr[] = {4, 8, 6, 2};
    int n = arr.length;
    System.out.println("Maximum AND Value = " +
                       maxAND(arr, n));
}
}

// This code is contributed by Prerna Saini
```

## 蟒蛇 3

```
# Python3 Program to find maximum XOR
# value of a pair

# Utility function to check number of
# elements having set msb as of pattern
def checkBit(pattern,arr,  n) :
    count = 0

    for i in range(0, n) :
        if ((pattern & arr[i]) == pattern) :
            count = count + 1
    return count

# Function for finding maximum and
# value pair
def maxAND (arr,  n) :
    res = 0

    # iterate over total of 32bits
    # from msb to lsb
    for bit in range(31,-1,-1) :

        # find the count of element
        # having set  msb
        count = checkBit(res | (1 << bit), arr, n)

        # if count >= 2 set particular
        # bit in result
        if ( count >= 2 ) :
            res =res | (1 << bit)

    return res

# Driver function
arr = [4, 8, 6, 2]
n = len(arr)
print("Maximum AND Value = ", maxAND(arr, n))

# This code is contributed by Nikita Tiwari
```

## C#

```
// C# Program to find maximum
// XOR value of a pair
using System;

public class GfG
{

// Utility function to check
// number of elements having
// set msb as of pattern
static int checkBit(int pattern,
                    int []arr,
                    int n)
{
    int count = 0;
    for (int i = 0; i < n; i++)
        if ((pattern & arr[i]) == pattern)
            count++;
    return count;
}

// Function for finding maximum
// and value pair
static int maxAND (int []arr, int n)
{
    int res = 0, count;

    // iterate over total of 32bits
    // from msb to lsb
    for (int bit = 31; bit >= 0; bit--)
    {

        // find the count of element
        // having set msb
        count = checkBit(res | (1 << bit), arr, n);

        // if count >= 2 set particular
        // bit in result
        if (count >= 2)    
            res |= (1 << bit);    
    }

    return res;
}

// Driver Code
public static void Main()
{
    int []arr = {4, 8, 6, 2};
    int n = arr.Length;
    Console.WriteLine("Maximum AND Value = " +
                       maxAND(arr, n));
}
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find maximum
// XOR value of a pair

// Utility function to check
// number of elements having
// set msb as of pattern
function checkBit($pattern, $arr, $n)
{
    $count = 0;
    for ($i = 0; $i < $n; $i++)
        if (($pattern & $arr[$i]) == $pattern)
            $count++;
    return $count;
}

// Function for finding
// maximum and value pair
function maxAND ($arr, $n)
{
    $res = 0;$count;

    // iterate over total of
    // 32bits from msb to lsb
    for ($bit = 31; $bit >= 0; $bit--)
    {

        // find the count of element
        // having set msb
        $count = checkBit($res | (1 << $bit),
                                   $arr, $n);

        // if count >= 2 set particular
        // bit in result
        if ( $count >= 2 )
            $res |= (1 << $bit);
    }

    return $res;
}

    // Driver Code
    $arr = array(4, 8, 6, 2);
    $n = count($arr);
    echo "Maximum AND Value = " , maxAND($arr,$n);

// This code is contributed by vt_m.
?>
```

## java 描述语言

```
<script>
    // Javascript Program to find maximum XOR value of a pair

    // Utility function to check
    // number of elements having
    // set msb as of pattern
    function checkBit(pattern, arr, n)
    {
        let count = 0;
        for (let i = 0; i < n; i++)
            if ((pattern & arr[i]) == pattern)
                count++;
        return count;
    }

    // Function for finding maximum
    // and value pair
    function maxAND (arr, n)
    {
        let res = 0, count;

        // iterate over total of 32bits
        // from msb to lsb
        for (let bit = 31; bit >= 0; bit--)
        {

            // find the count of element
            // having set msb
            count = checkBit(res | (1 << bit), arr, n);

            // if count >= 2 set particular
            // bit in result
            if (count >= 2)   
                res |= (1 << bit);   
        }

        return res;
    }

    let arr = [4, 8, 6, 2];
    let n = arr.length;
    document.write("Maximum AND Value = " + maxAND(arr, n));

    // This code is contributed by divyesh072019.
</script>
```

输出:

```
Maximum AND Value = 4
```

时间复杂度:O(n * log(m))，其中 m 是数组中的最大元素，n 是数组的大小。