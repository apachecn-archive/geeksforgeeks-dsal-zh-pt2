# 修改数组以使相邻元素的奇偶性不同所需的最小操作

> 原文:[https://www . geeksforgeeks . org/修改数组所需的最小操作数，以便相邻元素的奇偶校验不同/](https://www.geeksforgeeks.org/minimum-operations-required-to-modify-the-array-such-that-parity-of-adjacent-elements-is-different/)

给定一个数组 **A[]** ，任务是找到将该数组转换为 **B[]** 所需的最小操作数，以便对于 B 中的每个索引(除了最后一个)**奇偶校验(b[i])！=奇偶校验(b[i + 1])** 其中**奇偶校验(x) = x % 3** 。

下面是要执行的操作:

> 集合 **{1，2}** 中的任何元素都可以添加到数组的任何元素中。

**例:**

> **输入:** A[] = {2，1，3，0}
> **输出:** 1
> 1 可以一次操作加 0，数组变成{2，1，3，1}。
> **输入:** A[] = {2，2，2，2}
> **输出:** 2

**方法:**一种最佳方法是更新位于两个其他元素之间的元素，以便可以更新该元素，从而使其奇偶性在单次操作中可以不同于它之前的元素和它旁边的元素(因为操作的数量需要最小化)。
因此，开始遍历数组从 **A[1]** 到**A[n–2]**并且对于每个元素 **A[i]** ，使得**奇偶性(A[i]) ==奇偶性(A[I–1])**或**奇偶性(A[i]) ==奇偶性(A[i + 1])** ，更新 **A[i]** 使得其奇偶性不同于两者最后打印计数。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the parity of a number
int parity(int a)
{
    return a % 3;
}

// Function to return the minimum
// number of operations required
int solve(int array[], int size)
{
    int operations = 0;
    for (int i = 0; i < size - 1; i++) {

        // Operation needs to be performed
        if (parity(array[i]) == parity(array[i + 1])) {

            operations++;
            if (i + 2 < size) {

                // Parity of previous element
                int pari1 = parity(array[i]);

                // Parity of next element
                int pari2 = parity(array[i + 2]);

                // Update parity of current element to be other than
                // the parities of the previous and the next number
                if (pari1 == pari2) {
                    if (pari1 == 0)
                        array[i + 1] = 1;
                    else if (pari1 == 1)
                        array[i + 1] = 0;
                    else
                        array[i + 1] = 1;
                }
                else {
                    if ((pari1 == 0 && pari2 == 1)
                        || (pari1 == 1 && pari2 == 0))
                        array[i + 1] = 2;
                    if ((pari1 == 1 && pari2 == 2)
                        || (pari1 == 2 && pari2 == 1))
                        array[i + 1] = 0;
                    if ((pari1 == 2 && pari2 == 0)
                        || (pari1 == 0 && pari2 == 2))
                        array[i + 1] = 1;
                }
            }
        }
    }

    return operations;
}

// Driver Code
int main()
{
    int array[] = { 2, 1, 3, 0 };
    int size = sizeof(array) / sizeof(array[0]);
    cout << solve(array, size) << endl;

  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to return the parity of a number
    static int parity(int a)
    {
        return a % 3;
    }

    // Function to return the minimum
    // number of operations required
    static int solve(int []array, int size)
    {
        int operations = 0;
        for (int i = 0; i < size - 1; i++)
        {

            // Operation needs to be performed
            if (parity(array[i]) == parity(array[i + 1]))
            {

                operations++;
                if (i + 2 < size)
                {

                    // Parity of previous element
                    int pari1 = parity(array[i]);

                    // Parity of next element
                    int pari2 = parity(array[i + 2]);

                    // Update parity of current
                    // element to be other than
                    // the parities of the previous
                    // and the next number
                    if (pari1 == pari2)
                    {
                        if (pari1 == 0)
                            array[i + 1] = 1;
                        else if (pari1 == 1)
                            array[i + 1] = 0;
                        else
                            array[i + 1] = 1;
                    }
                    else
                    {
                        if ((pari1 == 0 && pari2 == 1) ||
                            (pari1 == 1 && pari2 == 0))
                            array[i + 1] = 2;
                        if ((pari1 == 1 && pari2 == 2)
                            || (pari1 == 2 && pari2 == 1))
                            array[i + 1] = 0;
                        if ((pari1 == 2 && pari2 == 0)
                            || (pari1 == 0 && pari2 == 2))
                            array[i + 1] = 1;
                    }
                }
            }
        }

        return operations;
    }

    // Driver Code
    public static void main (String arg[])
    {
        int []array = { 2, 1, 3, 0 };
        int size = array.length;
        System.out.println(solve(array, size));
    }
}

// This code is contributed by Ryuga
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the parity
# of a number
def parity(a):
    return a % 3

# Function to return the minimum
# number of operations required
def solve(array, size):

    operations = 0
    for i in range(0, size - 1):

        # Operation needs to be performed
        if parity(array[i]) == parity(array[i + 1]):

            operations += 1
            if i + 2 < size:

                # Parity of previous element
                pari1 = parity(array[i])

                # Parity of next element
                pari2 = parity(array[i + 2])

                # Update parity of current element to
                # be other than the parities of the
                # previous and the next number
                if pari1 == pari2:
                    if pari1 == 0:
                        array[i + 1] = 1
                    elif pari1 == 1:
                        array[i + 1] = 0
                    else:
                        array[i + 1] = 1

                else:
                    if ((pari1 == 0 and pari2 == 1) or
                        (pari1 == 1 and pari2 == 0)):
                        array[i + 1] = 2
                    if ((pari1 == 1 and pari2 == 2) or
                        (pari1 == 2 and pari2 == 1)):
                        array[i + 1] = 0
                    if ((pari1 == 2 and pari2 == 0) and
                        (pari1 == 0 and pari2 == 2)):
                        array[i + 1] = 1

    return operations

# Driver Code
if __name__ == "__main__":

    array = [2, 1, 3, 0]
    size = len(array)
    print(solve(array, size))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the parity of a number
static int parity(int a)
{
    return a % 3;
}

// Function to return the minimum
// number of operations required
static int solve(int []array, int size)
{
    int operations = 0;
    for (int i = 0; i < size - 1; i++)
    {

        // Operation needs to be performed
        if (parity(array[i]) == parity(array[i + 1]))
        {

            operations++;
            if (i + 2 < size)
            {

                // Parity of previous element
                int pari1 = parity(array[i]);

                // Parity of next element
                int pari2 = parity(array[i + 2]);

                // Update parity of current
                // element to be other than
                // the parities of the previous
                // and the next number
                if (pari1 == pari2)
                {
                    if (pari1 == 0)
                        array[i + 1] = 1;
                    else if (pari1 == 1)
                        array[i + 1] = 0;
                    else
                        array[i + 1] = 1;
                }
                else
                {
                    if ((pari1 == 0 && pari2 == 1) ||
                        (pari1 == 1 && pari2 == 0))
                        array[i + 1] = 2;
                    if ((pari1 == 1 && pari2 == 2)
                        || (pari1 == 2 && pari2 == 1))
                        array[i + 1] = 0;
                    if ((pari1 == 2 && pari2 == 0)
                        || (pari1 == 0 && pari2 == 2))
                        array[i + 1] = 1;
                }
            }
        }
    }

    return operations;
}

// Driver Code
public static void Main()
{
    int []array = { 2, 1, 3, 0 };
    int size = array.Length;
    Console.WriteLine(solve(array, size));
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the parity of a number
function parity($a)
{
    return $a % 3;
}

// Function to return the minimum
// number of operations required
function solve($array, $size)
{
    $operations = 0;
    for ($i = 0; $i < $size - 1; $i++)
    {

        // Operation needs to be performed
        if (parity($array[$i]) == parity($array[$i + 1]))
        {

            $operations++;
            if ($i + 2 < $size)
            {

                // Parity of previous element
                $pari1 = parity($array[$i]);

                // Parity of next element
                $pari2 = parity($array[$i + 2]);

                // Update parity of current element to be
                // other than the parities of the previous
                // and the next number
                if ($pari1 == $pari2)
                {
                    if ($pari1 == 0)
                        $array[$i + 1] = 1;
                    else if ($pari1 == 1)
                        $array[$i + 1] = 0;
                    else
                        $array[$i + 1] = 1;
                }
                else
                {
                    if (($pari1 == 0 && $pari2 == 1) ||
                        ($pari1 == 1 && $pari2 == 0))
                        $array[$i + 1] = 2;
                    if (($pari1 == 1 && $pari2 == 2) ||
                        ($pari1 == 2 && $pari2 == 1))
                        $array[$i + 1] = 0;
                    if (($pari1 == 2 && $pari2 == 0) ||
                        ($pari1 == 0 && $pari2 == 2))
                        $array[$i + 1] = 1;
                }
            }
        }
    }

    return $operations;
}

// Driver Code
$array = array(2, 1, 3, 0 );
$size = count($array);
echo solve($array, $size);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the parity of a number
function parity(a)
{
    return a % 3;
}

// Function to return the minimum
// number of operations required
function solve(array, size)
{
    var operations = 0;
    for (var i = 0; i < size - 1; i++) {

        // Operation needs to be performed
        if (parity(array[i]) == parity(array[i + 1])) {

            operations++;
            if (i + 2 < size) {

                // Parity of previous element
                var pari1 = parity(array[i]);

                // Parity of next element
                var pari2 = parity(array[i + 2]);

                // Update parity of current element to be other than
                // the parities of the previous and the next number
                if (pari1 == pari2) {
                    if (pari1 == 0)
                        array[i + 1] = 1;
                    else if (pari1 == 1)
                        array[i + 1] = 0;
                    else
                        array[i + 1] = 1;
                }
                else {
                    if ((pari1 == 0 && pari2 == 1)
                        || (pari1 == 1 && pari2 == 0))
                        array[i + 1] = 2;
                    if ((pari1 == 1 && pari2 == 2)
                        || (pari1 == 2 && pari2 == 1))
                        array[i + 1] = 0;
                    if ((pari1 == 2 && pari2 == 0)
                        || (pari1 == 0 && pari2 == 2))
                        array[i + 1] = 1;
                }
            }
        }
    }

    return operations;
}

// Driver Code
var array = [2, 1, 3, 0];
var size = array.length;
document.write( solve(array, size));

</script>
```

**Output:** 

```
1
```

**时间复杂度:** O(N)

**辅助空间:** O(1)