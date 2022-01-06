# 1 到 N 范围内最小子阵列的长度，总和大于给定值

> 原文:[https://www . geeksforgeeks . org/1 至 n 范围内最小子阵列长度的和大于给定值/](https://www.geeksforgeeks.org/length-of-smallest-subarray-in-range-1-to-n-with-sum-greater-than-a-given-value/)

给定两个数字 **N** 和 **S** ，任务是找到范围 **(1，N)** 中最小子阵列的长度，使得这些选择的数字之和大于 **S** 。

**示例:**

> **输入:** N = 5，S = 11
> **输出:** 3
> **解释:**
> 最小子阵带和> 11 = {5，4，3}
> 
> **输入:** N = 4，S = 7
> **输出:** 3
> **解释:**
> 最小子阵带和> 7 = {4，3，2}

**天真法:**蛮力法是按照相反的顺序选择元素，直到所有选中元素的和小于或等于给定的个数。

下面是上述方法的实现。

## C++

```
// C++ implementation of the above implementation

#include <bits/stdc++.h>
using namespace std;

// Function to return the count
// of minimum elements such that
// the sum of those elements is > S.
int countNumber(int N, int S)
{
    int countElements = 0;
    // Initialize currentSum = 0

    int currSum = 0;

    // Loop from N to 1 to add the numbers
    // and check the condition.
    while (currSum <= S) {
        currSum += N;
        N--;
        countElements++;
    }

    return countElements;
}

// Driver code
int main()
{
    int N, S;
    N = 5;
    S = 11;

    int count = countNumber(N, S);

    cout << count << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above implementation
class GFG
{

    // Function to return the count
    // of minimum elements such that
    // the sum of those elements is > S.
    static int countNumber(int N, int S)
    {
        int countElements = 0;

        // Initialize currentSum = 0
        int currSum = 0;

        // Loop from N to 1 to add the numbers
        // and check the condition.
        while (currSum <= S)
        {
            currSum += N;
            N--;
            countElements++;
        }
        return countElements;
    }

    // Driver code
    public static void main (String[] args)
    {
        int N, S;
        N = 5;
        S = 11;

        int count = countNumber(N, S);

        System.out.println(count);
    }
}

// This code is contributed by AnkitRai01
```

## 计算机编程语言

```
# Python implementation of the above implementation

# Function to return the count
# of minimum elements such that
# the sum of those elements is > S.
def countNumber(N, S):

    countElements = 0;
    currentSum = 0

    currSum = 0;

    # Loop from N to 1 to add the numbers
    # and check the condition.
    while (currSum <= S) :
        currSum += N;
        N = N - 1;
        countElements=countElements + 1;

    return countElements;

# Driver code
N = 5;
S = 11;
count = countNumber(N, S);
print(count) ;

# This code is contributed by Shivi_Aggarwal
```

## C#

```
// C# implementation of the above implementation
using System;

class GFG
{

    // Function to return the count
    // of minimum elements such that
    // the sum of those elements is > S.
    static int countNumber(int N, int S)
    {
        int countElements = 0;

        // Initialize currentSum = 0
        int currSum = 0;

        // Loop from N to 1 to add the numbers
        // and check the condition.
        while (currSum <= S)
        {
            currSum += N;
            N--;
            countElements++;
        }
        return countElements;
    }

    // Driver code
    public static void Main()
    {
        int N, S;
        N = 5;
        S = 11;

        int count = countNumber(N, S);

        Console.WriteLine(count);
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// JavaScript implementation of the above implementation

// Function to return the count
// of minimum elements such that
// the sum of those elements is > S.
function countNumber(N, S)
{
    let countElements = 0;

    // Initialize currentSum = 0
    let currSum = 0;

    // Loop from N to 1 to add the numbers
    // and check the condition.
    while (currSum <= S)
    {
        currSum += N;
        N--;
        countElements++;
    }
    return countElements;
}

// Driver code
    let N, S;
    N = 5;
    S = 11;
    let count = countNumber(N, S);
    document.write(count + "<br>");

// This code is contributed by Surbhi Tyagi.
</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(N)

**高效途径:**思路是用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)概念解决问题。
从二分搜索法概念可知，当已知问题中存在顺序时，可以应用该概念。也就是说，对于每一次迭代，如果能够确定所需的答案是在前半部分还是后半部分(即，问题中存在一个模式)。
因此，二分搜索法可以通过以下方式申请靶场:

1.  初始化开始= 1，结束= N。
2.  找到 mid = start+(end–start)/2。
3.  如果从最后一个元素到中间元素的所有元素的总和小于或等于给定的总和，则 end = mid 否则 start = mid + 1。
4.  当开始小于结束时，重复步骤 2。

下面是上述方法的实现。

## C++

```
// C++ implementation of the above approach.

#include <iostream>
using namespace std;

// Function to do a binary search
// on a given range.
int usingBinarySearch(int start, int end,
                      int N, int S)
{
    if (start >= end)
        return start;
    int mid = start + (end - start) / 2;

    // Total sum is the sum of N numbers.
    int totalSum = (N * (N + 1)) / 2;

    // Sum until mid
    int midSum = (mid * (mid + 1)) / 2;

    // If remaining sum is < the required value,
    // then the required number is in the right half
    if ((totalSum - midSum) <= S) {

        return usingBinarySearch(start, mid, N, S);
    }
    return usingBinarySearch(mid + 1, end, N, S);
}

// Driver code
int main()
{
    int N, S;

    N = 5;
    S = 11;

    cout << (N - usingBinarySearch(1, N, N, S) + 1)
         << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach.
class GFG
{

    // Function to do a binary search
    // on a given range.
    static int usingBinarySearch(int start, int end,
                                int N, int S)
    {
        if (start >= end)
            return start;
        int mid = start + (end - start) / 2;

        // Total sum is the sum of N numbers.
        int totalSum = (N * (N + 1)) / 2;

        // Sum until mid
        int midSum = (mid * (mid + 1)) / 2;

        // If remaining sum is < the required value,
        // then the required number is in the right half
        if ((totalSum - midSum) <= S)
        {

            return usingBinarySearch(start, mid, N, S);
        }
        return usingBinarySearch(mid + 1, end, N, S);
    }

    // Driver code
    public static void main (String[] args)
    {
        int N, S;

        N = 5;
        S = 11;

        System.out.println(N - usingBinarySearch(1, N, N, S) + 1) ;
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the above approach.

# Function to do a binary search
# on a given range.
def usingBinarySearch(start, end, N, S) :

    if (start >= end) :
        return start;

    mid = start + (end - start) // 2;

    # Total sum is the sum of N numbers.
    totalSum = (N * (N + 1)) // 2;

    # Sum until mid
    midSum = (mid * (mid + 1)) // 2;

    # If remaining sum is < the required value,
    # then the required number is in the right half
    if ((totalSum - midSum) <= S) :

        return usingBinarySearch(start, mid, N, S);

    return usingBinarySearch(mid + 1, end, N, S);

# Driver code
if __name__ == "__main__" :

    N = 5;
    S = 11;

    print(N - usingBinarySearch(1, N, N, S) + 1) ;

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the above approach.
using System;

class GFG
{

    // Function to do a binary search
    // on a given range.
    static int usingBinarySearch(int start, int end,
                                int N, int S)
    {
        if (start >= end)
            return start;
        int mid = start + (end - start) / 2;

        // Total sum is the sum of N numbers.
        int totalSum = (N * (N + 1)) / 2;

        // Sum until mid
        int midSum = (mid * (mid + 1)) / 2;

        // If remaining sum is < the required value,
        // then the required number is in the right half
        if ((totalSum - midSum) <= S)
        {

            return usingBinarySearch(start, mid, N, S);
        }
        return usingBinarySearch(mid + 1, end, N, S);
    }

    // Driver code
    public static void Main()
    {
        int N, S;

        N = 5;
        S = 11;

        Console.WriteLine(N - usingBinarySearch(1, N, N, S) + 1) ;
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach.

// Function to do a binary search
// on a given range.
function usingBinarySearch(start, end, N, S)
{
    if (start >= end)
        return start;

    let mid = start + (end - start) / 2;

    // Total sum is the sum of N numbers.
    let totalSum = (N * (N + 1)) / 2;

    // Sum until mid
    let midSum = (mid * (mid + 1)) / 2;

    // If remaining sum is < the required value,
    // then the required number is in the right half
    if ((totalSum - midSum) <= S)
    {
        return usingBinarySearch(start, mid, N, S);
    }
    return usingBinarySearch(mid + 1, end, N, S);
}

// Driver code
let N, S;
N = 5;
S = 11;

document.write((N - usingBinarySearch(
      1, N, N, S) + 1) + "<br>");

// This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(log N)