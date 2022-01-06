# 元二分搜索法|一边倒的二分搜索法

> 原文:[https://www . geesforgeks . org/meta-binary-search-单侧-binary-search/](https://www.geeksforgeeks.org/meta-binary-search-one-sided-binary-search/)

Meta 二分搜索法(Steven Skiena 在第 134 页的算法设计手册中也称单侧二分搜索法)是二分搜索法的一种修改形式，它递增地构造数组中目标值的索引。像正常的二分搜索法一样，元二分搜索法需要 O(log n)时间。

**示例:**

```
Input: [-10, -5, 4, 6, 8, 10, 11], key_to_search = 10
Output: 5

Input: [-2, 10, 100, 250, 32315], key_to_search = -2
Output: 0
```

具体实现各不相同，但基本算法有两个部分:

1.  计算出需要多少位来存储最大的数组索引。
2.  通过确定索引中的每个位应该设置为 1 还是 0，以增量方式构造数组中目标值的索引。

**进场:**

1.  存储表示变量 lg 中最大数组索引的位数。
2.  使用 lg 以 for 循环开始搜索。
3.  如果找到元素，返回位置。
4.  否则，增量构造一个索引以达到 for 循环中的目标值。
5.  如果找到元素，返回位置-1。

以下是上述方法的实现:

## C++

```
// C++ implementation of above approach

#include <iostream>
#include <cmath>
#include <vector>
using namespace std;

// Function to show the working of Meta binary search
int bsearch(vector<int> A, int key_to_search)
{
    int n = (int)A.size();
    // Set number of bits to represent largest array index
    int lg = log2(n-1)+1; 

    //while ((1 << lg) < n - 1)
        //lg += 1;

    int pos = 0;
    for (int i = lg ; i >= 0; i--) {
        if (A[pos] == key_to_search)
            return pos;

        // Incrementally construct the
        // index of the target value
        int new_pos = pos | (1 << i);

        // find the element in one
        // direction and update position
        if ((new_pos < n) && (A[new_pos] <= key_to_search))
            pos = new_pos;
    }

    // if element found return pos otherwise -1
    return ((A[pos] == key_to_search) ? pos : -1);
}

// Driver code
int main(void)
{

    vector<int> A = { -2, 10, 100, 250, 32315 };
    cout << bsearch(A, 10) << endl;

    return 0;
}

// This implementation was improved by Tanin
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java implementation of above approach 
import java.util.Vector;
import com.google.common.math.BigIntegerMath;
import java.math.*;

class GFG {

// Function to show the working of Meta binary search 
    static int bsearch(Vector<Integer> A, int key_to_search) {
        int n = (int) A.size();
        // Set number of bits to represent largest array index
        int lg = BigIntegerMath.log2(BigInteger.valueOf(n-1),RoundingMode.UNNECESSARY) + 1;

        //while ((1 << lg) < n - 1) {
        //    lg += 1;
        //}

        int pos = 0;
        for (int i = lg - 1; i >= 0; i--) {
            if (A.get(pos) == key_to_search) {
                return pos;
            }

            // Incrementally construct the 
            // index of the target value 
            int new_pos = pos | (1 << i);

            // find the element in one 
            // direction and update position 
            if ((new_pos < n) && (A.get(new_pos) <= key_to_search)) {
                pos = new_pos;
            }
        }

        // if element found return pos otherwise -1 
        return ((A.get(pos) == key_to_search) ? pos : -1);
    }

// Driver code 
    static public void main(String[] args) {
        Vector<Integer> A = new Vector<Integer>();
        int[] arr = {-2, 10, 100, 250, 32315};
        for (int i = 0; i < arr.length; i++) {
            A.add(arr[i]);
        }
        System.out.println(bsearch(A, 10));
    }
}

// This code is contributed by 29AjayKumar
// This implementation was improved by Tanin
```

## 蟒蛇 3

```
# Python 3 implementation of 
# above approach

# Function to show the working
# of Meta binary search
import math
def bsearch(A, key_to_search):

    n = len(A)
    # Set number of bits to represent
    lg = int(math.log2(n-1)) + 1;

    # largest array index
    #while ((1 << lg) < n - 1):
        #lg += 1

    pos = 0
    for i in range(lg - 1, -1, -1) :
        if (A[pos] == key_to_search):
            return pos

        # Incrementally construct the
        # index of the target value
        new_pos = pos | (1 << i)

        # find the element in one
        # direction and update position
        if ((new_pos < n) and 
            (A[new_pos] <= key_to_search)):
            pos = new_pos

    # if element found return
    # pos otherwise -1
    return (pos if(A[pos] == key_to_search) else -1)

# Driver code
if __name__ == "__main__":

    A = [ -2, 10, 100, 250, 32315 ]
    print( bsearch(A, 10))

# This implementation was improved by Tanin

# This code is contributed
# by ChitraNayal
```

## C#

```
//C# implementation of above approach 
using System;
using System.Collections.Generic;

class GFG 
{

    // Function to show the working of Meta binary search 
    static int bsearch(List<int> A, int key_to_search)
    {
        int n = (int) A.Count;
        //int lg = 0;
        // Set number of bits to represent largest array index 
        int lg = (int)Math.Log(n-1, 2.0) + 1;

        // This is redundant and will cause error
        //while ((1 << lg) < n - 1)
        //{
        //    lg += 1;
        //}

        int pos = 0;
        for (int i = lg - 1; i >= 0; i--)
        {
            if (A[pos] == key_to_search)
            {
                return pos;
            }

            // Incrementally construct the 
            // index of the target value 
            int new_pos = pos | (1 << i);

            // find the element in one 
            // direction and update position 
            if ((new_pos < n) && (A[new_pos] <= key_to_search))
            {
                pos = new_pos;
            }
        }

        // if element found return pos otherwise -1 
        return ((A[pos] == key_to_search) ? pos : -1);
    }

    // Driver code 
    static public void Main()
    {
        List<int> A = new List<int>();
        int[] arr = {-2, 10, 100, 250, 32315};
        for (int i = 0; i < arr.Length; i++) 
        {
            A.Add(arr[i]);
        }
        Console.WriteLine(bsearch(A, 10));
    }
}

// This code is contributed by Rajput-Ji
// This implementation was improved by Tanin
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Function to show the working of 
// Meta binary search
function bsearch($A, $key_to_search, $n)
{
    // Set number of bits to represent
    $lg = log($n-1, 2) + 1;

    // largest array index
     // This is redundant and will cause error for some case
    //while ((1 << $lg) < $n - 1)
        //$lg += 1;

    $pos = 0;
    for ($i = $lg - 1; $i >= 0; $i--) 
    {
        if ($A[$pos] == $key_to_search)
            return $pos;

        // Incrementally construct the
        // index of the target value
        $new_pos = $pos | (1 << $i);

        // find the element in one
        // direction and update $position
        if (($new_pos < $n) && 
            ($A[$new_pos] <= $key_to_search))
            $pos = $new_pos;
    }

    // if element found return $pos 
    // otherwise -1
    return (($A[$pos] == $key_to_search) ? 
                              $pos : -1);
}

// Driver code
$A = [ -2, 10, 100, 250, 32315 ];
$ans = bsearch($A, 10, 5);
echo $ans;

// This code is contributed by AdeshSingh1
// This implementation was improved by Tanin
?>
```

## java 描述语言

```
<script>
// Javascript implementation of above approach

// Function to show the working of Meta binary search
function bsearch(A, key_to_search)
{
    let n = A.length;
    // Set number of bits to represent largest array index
    let lg = parseInt(Math.log(n-1) / Math.log(2)) + 1; 

    //while ((1 << lg) < n - 1)
        //lg += 1;

    let pos = 0;
    for (let i = lg ; i >= 0; i--) {
        if (A[pos] == key_to_search)
            return pos;

        // Incrementally construct the
        // index of the target value
        let new_pos = pos | (1 << i);

        // find the element in one
        // direction and update position
        if ((new_pos < n) && (A[new_pos] <= key_to_search))
            pos = new_pos;
    }

    // if element found return pos otherwise -1
    return ((A[pos] == key_to_search) ? pos : -1);
}

// Driver code

    let A = [ -2, 10, 100, 250, 32315 ];
    document.write(bsearch(A, 10));

</script>
```

**Output:** 

```
1
```

**参考:**T2】https://www.quora.com/What-is-meta-binary-search