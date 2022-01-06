# 在不改变顺序的情况下，将数组分为递增和递减子序列

> 原文:[https://www . geesforgeks . org/将数组划分为不改变顺序的递增和递减子序列/](https://www.geeksforgeeks.org/divide-array-into-increasing-and-decreasing-subsequence-without-changing-the-order/)

给定一个由两个被合并的序列组成的合并序列，其中一个严格递增，另一个严格递减。递增序列的元素被插入递减序列的元素之间，而不改变顺序。

> 序列[1，3，4]和[10，4，2]可以产生以下结果序列:
> [10，1，3，4，2，4]，[1，3，4，10，4，2]。
> 以下序列不可能是这些插入的结果:
> 【1，10，4，4，3，2】因为递增序列中元素的顺序被改变了。

给定一个合并序列，任务是找到任意两个合适的初始序列，其中一个应该严格递增，另一个应该严格递减。
**注**:空序列和由一个元素组成的序列可以认为是递增或递减的。
**示例:**

> **输入:** arr[] = {5，1，3，6，8，2，9，0，10}
> **输出:**【1，3，6，8，9，10】【5，2，0】
> 
> **输入:** arr[] = {1，2，4，0，2}
> **输出:** -1
> 不可能有这样的序列。

**方法一:**我们可以修改[最长递增序列](https://www.geeksforgeeks.org/longest-monotonically-increasing-subsequence-size-n-log-n/)，解决需要的问题。这需要时间。

**方法二:**我们也可以只用一次遍历来解决这个问题。这里使用的思想是维护两个排序的数组。
为新元素 **x** ，

*   如果它只能追加到一个数组中，那么就追加它。
*   如果都不能追加，那么答案是 **-1** 。
*   如果可以将它附加到两者上，那么检查下一个元素 **y** ，如果 **y > x** 那么将 **x** 附加到递增的元素上，否则将 **x** 附加到递减的元素上。

现在，当我们遇到一个可以包含在两个序列中的元素时，我们需要根据下一个元素的值来决定。让我们考虑这样一种情况，我们需要迭代剩余的值 x，y，z，其中(x < z < y)，并且我们已经将递增和递减序列的最后一个元素分别作为数组访问部分的 inc 和 dec。

案例 1 : x

所以我们可以在任何序列中包含 x。

如果我们以递减顺序包括它，那么 dec 将变成 x。然后对于 y，我们只有一个选择，即以递增顺序包括它，因为 y>dec，inc 变成 y。如果我们这样做，我们不能以 z>dec 和 z

但是，如果我们按照同样的逻辑，把 x 加到递增序列(inc 变成 x)，把 y 加到递减序列(dec 变成 y)，那么我们可以把 z 放在任何序列中，得到一个答案。

案例 2 : x>=y，inc

它遵循与上面相同的逻辑。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to print strictly increasing and
// strictly decreasing sequence if possible
void Find_Sequence(int arr[], int n)
{
    // Arrays to store strictly increasing and
    // decreasing sequence
    vector<int> inc_arr, dec_arr;

    // Initializing last element of both sequence
    int flag = 0;
    long inc = -1, dec = 1e7;

    // Iterating through the array
    for (int i = 0; i < n; i++)
    {
        // If current element can be appended
        // to both the sequences
        if (inc < arr[i] && arr[i] < dec)
        {
            // If next element is greater than
            // the current element
            // Then append it to the strictly
            // increasing array
            if (arr[i] < arr[i + 1])
            {
                inc = arr[i];
                inc_arr.emplace_back(arr[i]);
            }

            // Otherwise append it to the
            // strictly decreasing array
            else
            {
                dec = arr[i];
                dec_arr.emplace_back(arr[i]);
            }
        }

        // If current element can be appended
        // to the increasing sequence only
        else if (inc < arr[i])
        {
            inc = arr[i];
            inc_arr.emplace_back(arr[i]);
        }

        // If current element can be appended
        // to the decreasing sequence only
        else if (dec > arr[i])
        {
            dec = arr[i];
            dec_arr.emplace_back(arr[i]);
        }

        // Else we can not make such sequences
        // from the given array
        else
        {
            cout << -1 << endl;
            flag = 1;
            break;
        }
    }

    // Print the required sequences
    if (!flag)
    {
        for (auto i = inc_arr.begin();
                  i != inc_arr.end(); i++)
            cout << *i << " ";
        cout << endl;

        for (auto i = dec_arr.begin();
                  i != dec_arr.end(); i++)
            cout << *i << " ";
        cout << endl;
    }
}

// Driver code
int main()
{
    int arr[] = { 5, 1, 3, 6, 8, 2, 9, 0, 10 };
    int n = sizeof(arr) / sizeof(arr[0]);
    Find_Sequence(arr, n);
}

// This code is contributed by sanjeev2552
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

    // Function to print strictly increasing and
    // strictly decreasing sequence if possible
    static void Find_Sequence(int[] arr, int n)
    {

        // Arrays to store strictly increasing and
        // decreasing sequence
        Vector<Integer> inc_arr = new Vector<>(),
                        dec_arr = new Vector<>();

        // Initializing last element of both sequence
        int flag = 0;
        long inc = -1, dec = (long) 1e7;

        // Iterating through the array
        for (int i = 0; i < n; i++)
        {

            // If current element can be appended
            // to both the sequences
            if (inc < arr[i] && arr[i] < dec)
            {

                // If next element is greater than
                // the current element
                // Then append it to the strictly
                // increasing array
                if (arr[i] < arr[i + 1])
                {
                    inc = arr[i];
                    inc_arr.add(arr[i]);
                }

                // Otherwise append it to the
                // strictly decreasing array
                else
                {
                    dec = arr[i];
                    dec_arr.add(arr[i]);
                }
            }

            // If current element can be appended
            // to the increasing sequence only
            else if (inc < arr[i])
            {
                inc = arr[i];
                inc_arr.add(arr[i]);
            }

            // If current element can be appended
            // to the decreasing sequence only
            else if (dec > arr[i])
            {
                dec = arr[i];
                dec_arr.add(arr[i]);
            }

            // Else we can not make such sequences
            // from the given array
            else
            {
                System.out.println(-1);
                flag = 1;
                break;
            }
        }

        // Print the required sequences
        if (flag == 0)
        {
            for (int i : inc_arr)
                System.out.print(i + " ");
            System.out.println();

            for (int i : dec_arr)
                System.out.print(i + " ");
            System.out.println();
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = { 5, 1, 3, 6, 8, 2, 9, 0, 10 };
        int n = arr.length;
        Find_Sequence(arr, n);
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to print strictly increasing and
# strictly decreasing sequence if possible
def Find_Sequence(array, n):

    # Arrays to store strictly increasing and
    # decreasing sequence
    inc_arr, dec_arr =[], []

    # Initializing last element of both sequence
    inc, dec = -1, 1e7

    # Iterating through the array
    for i in range(n):

        # If current element can be appended
        # to both the sequences
        if inc < array[i] < dec:

            # If next element is greater than
            # the current element
            # Then append it to the strictly
            # increasing array
            if array[i] < array[i + 1]:
                inc = array[i]
                inc_arr.append(array[i])

            # Otherwise append it to the
            # strictly decreasing array
            else:
                dec = array[i]
                dec_arr.append(array[i])

        # If current element can be appended
        # to the increasing sequence only
        elif inc < array[i]:
            inc = array[i]
            inc_arr.append(array[i])

        # If current element can be appended
        # to the decreasing sequence only
        elif dec > array[i]:
            dec = array[i]
            dec_arr.append(array[i])

        # Else we can not make such sequences
        # from the given array
        else:
            print('-1')
            break

    # Print the required sequences
    else:
        print(inc_arr, dec_arr)

# Driver code
arr = [5, 1, 3, 6, 8, 2, 9, 0, 10]
n = len(arr)
Find_Sequence(arr, n)
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections;
using System.Collections.Generic; 

class GFG{

// Function to print strictly increasing and
// strictly decreasing sequence if possible
static void Find_Sequence(int[] arr, int n)
{

    // Arrays to store strictly increasing and
    // decreasing sequence
    ArrayList inc_arr = new ArrayList();
    ArrayList dec_arr = new ArrayList();

    // Initializing last element of both sequence
    int flag = 0;
    long inc = -1, dec = (long)1e7;

    // Iterating through the array
    for(int i = 0; i < n; i++)
    {

        // If current element can be appended
        // to both the sequences
        if (inc < arr[i] && arr[i] < dec)
        {

            // If next element is greater than
            // the current element
            // Then append it to the strictly
            // increasing array
            if (arr[i] < arr[i + 1])
            {
                inc = arr[i];
                inc_arr.Add(arr[i]);
            }

            // Otherwise append it to the
            // strictly decreasing array
            else
            {
                dec = arr[i];
                dec_arr.Add(arr[i]);
            }
        }

        // If current element can be appended
        // to the increasing sequence only
        else if (inc < arr[i])
        {
            inc = arr[i];
            inc_arr.Add(arr[i]);
        }

        // If current element can be appended
        // to the decreasing sequence only
        else if (dec > arr[i])
        {
            dec = arr[i];
            dec_arr.Add(arr[i]);
        }

        // Else we can not make such sequences
        // from the given array
        else
        {
            Console.Write(-1);
            flag = 1;
            break;
        }
    }

    // Print the required sequences
    if (flag == 0)
    {
        foreach(int i in inc_arr)
            Console.Write(i + " ");

        Console.Write('\n');

        foreach(int i in dec_arr)
            Console.Write(i + " ");

        Console.Write('\n');
    }
}

// Driver Code
public static void Main(string[] args)
{
    int[] arr = { 5, 1, 3, 6, 8,
                  2, 9, 0, 10 };
    int n = arr.Length;

    Find_Sequence(arr, n);
}
}

// This code is contributed by rutvik_56
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Php implementation of the approach

// Function to print strictly increasing and
// strictly decreasing sequence if possible
function Find_Sequence($arr, $n)
{

    // Arrays to store strictly increasing and
    // decreasing sequence
    $inc_arr = array(); $dec_arr = array();

    // Initializing last element of both sequence
    $inc = -1; $dec = 1e7;

    // Iterating through the array
    for ($i = 0; $i < $n ; $i++)
    {

        // If current element can be appended
        // to both the sequences
        if ($inc < $arr[$i] && $arr[$i] < $dec)
        {

            // If next element is greater than
            // the current element
            // Then append it to the strictly
            // increasing array
            if ($arr[$i] < $arr[$i + 1])
            {
                $inc = $arr[$i];
                array_push($inc_arr, $arr[$i]);
            }

            // Otherwise append it to the
            // strictly decreasing array
            else
            {
                $dec = $arr[$i];
                array_push($dec_arr, $arr[$i]);
            }
        }

        // If current element can be appended
        // to the increasing sequence only
        else if ($inc < $arr[$i])
        {
            $inc = $arr[$i];
            array_push($inc_arr, $arr[$i]);
        }

        // If current element can be appended
        // to the decreasing sequence only
        else if($dec > $arr[$i])
        {
            $dec = $arr[$i];
            array_push($dec_arr, $arr[$i]);
        }

        // Else we can not make such sequences
        // from the given array
        else
        {
            echo '-1';
            break;
        }
    }

    // Print the required sequences
    print_r($inc_arr);
    print_r($dec_arr);
}

// Driver code
$arr = array(5, 1, 3, 6, 8, 2, 9, 0, 10);
$n = count($arr);
Find_Sequence($arr, $n);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

    // Function to print strictly increasing and
    // strictly decreasing sequence if possible
    function Find_Sequence(arr, n)
    {

        // Arrays to store strictly increasing and
        // decreasing sequence
        let inc_arr =[],
                        dec_arr = [];

        // Initializing last element of both sequence
        let flag = 0;
        let inc = -1, dec = 1e7;

        // Iterating through the array
        for (let i = 0; i < n; i++)
        {

            // If current element can be appended
            // to both the sequences
            if (inc < arr[i] && arr[i] < dec)
            {

                // If next element is greater than
                // the current element
                // Then append it to the strictly
                // increasing array
                if (arr[i] < arr[i + 1])
                {
                    inc = arr[i];
                    inc_arr.push(arr[i]);
                }

                // Otherwise append it to the
                // strictly decreasing array
                else
                {
                    dec = arr[i];
                    dec_arr.push(arr[i]);
                }
            }

            // If current element can be appended
            // to the increasing sequence only
            else if (inc < arr[i])
            {
                inc = arr[i];
                inc_arr.push(arr[i]);
            }

            // If current element can be appended
            // to the decreasing sequence only
            else if (dec > arr[i])
            {
                dec = arr[i];
                dec_arr.push(arr[i]);
            }

            // Else we can not make such sequences
            // from the given array
            else
            {
               document.write(-1);
                flag = 1;
                break;
            }
        }

        // Print the required sequences
        if (flag == 0)
        {
             document.write("[");
            for (let i in inc_arr)
                document.write( inc_arr[i] + " ");
            document.write("] ");

             document.write("[");
            for (let i in dec_arr)
                document.write( dec_arr[i] + " ");
            document.write("]");
        }
    }   

// Driver Code

        let arr = [ 5, 1, 3, 6, 8, 2, 9, 0, 10 ];
        let n = arr.length;
        Find_Sequence(arr, n);

// This code is contributed by target_2.
</script>
```

**Output:** 

```
[1, 3, 6, 8, 9, 10] [5, 2, 0]
```