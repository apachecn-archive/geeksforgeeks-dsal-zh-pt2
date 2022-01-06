# 找到数组中的一个元素，使元素形成严格的递减和递增序列

> 原文:[https://www . geeksforgeeks . org/find-a-element-in-a-a-array-so-elements-form-a-严格递减递增序列/](https://www.geeksforgeeks.org/find-an-element-in-an-array-such-that-elements-form-a-strictly-decreasing-and-increasing-sequence/)

给定一个正整数数组，任务是找到一个点/元素，直到这些元素形成一个严格递减的序列，然后是一个严格递增的整数序列。

*   两个序列的长度必须至少为 2(考虑公共元素)。
*   递减序列的最后一个值是递增序列的第一个值。

**注意:**如果没有找到，打印“不存在这样的元素”。
**例:**

```
Input: arr[] = {3, 2, 1, 2}
Output: 1
{3, 2, 1} is strictly decreasing 
then {1, 2} is strictly increasing.

Input: arr[] = {3, 2, 1}
Output: No such element exist
```

**进场:**

1.  首先开始遍历数组，并一直遍历，直到元素严格按降序排列。
2.  如果下一个元素大于前一个元素，则将该元素存储在*点*变量中。
3.  从那个点开始遍历元素，并一直遍历，直到元素按严格递增的顺序排列。
4.  在步骤 3 之后，如果所有的元素都被遍历了，那么打印那个点。
5.  否则打印“不存在这样的元素。”

**注意:**如果两个元素中的任何一个相等，那么也打印“不存在这样的元素”，因为它应该严格地递减和递增。

**以下是上述方法的实施:**

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check such sequence
int findElement(int a[], int n)
{

    // set increasing/decreasing sequence counter to 1
    int inc = 1, dec = 1, point;

    // for loop counter from 1 to last index of list
    for (int i = 1; i < n; i++) {

        // check if current int is
        // smaller than previous int
        if (a[i] < a[i - 1]) {

            // if inc is 1, i.e., increasing
            // seq. never started
            if (inc == 1)
                // increase dec by 1
                dec++;

            else
                return -1;
        }

        // check if current int is greater than previous int
        else if (a[i] > a[i - 1]) {

            // if inc is 1, i.e., increasing seq.
            // starting for first time,
            if (inc == 1)

                // store a[i-1] in point
                point = a[i - 1];

            // only if decreasing seq. minimum
            // count has been met,
            if (dec >= 2)

                // increase inc by 1
                inc++;

            else

                // return -1 as decreasing seq.
                // min. count must be 2
                return -1;
        }

        // check if current int is equal
        // to previous int, if so,
        else if (a[i] == a[i - 1])
            return -1;
    }

    // check if inc >= 2 and dec >= 2
    // return point
    if (inc >= 2 && dec >= 2)
        return point;

    // otherwise return -1
    else
        return -1;
}

// Driver code
int main()
{

    int arr[] = { 3, 2, 1, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);

    int ele = findElement(arr, n);

    if (ele == -1)
        cout << "No such element exist";
    else
        cout << ele;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach 

public class GFG {

    // Function to check such sequence
    static int findElement(int a[], int n)
    {

        // set increasing/decreasing sequence counter to 1
        int inc = 1, dec = 1, point = 0;

        // for loop counter from 1 to last index of list
        for (int i = 1; i < n; i++) {

            // check if current int is
            // smaller than previous int
            if (a[i] < a[i - 1]) {

                // if inc is 1, i.e., increasing
                // seq. never started
                if (inc == 1)
                    // increase dec by 1
                    dec++;

                else
                    return -1;
            }

            // check if current int is greater than previous int
            else if (a[i] > a[i - 1]) {

                // if inc is 1, i.e., increasing seq.
                // starting for first time,
                if (inc == 1)

                    // store a[i-1] in point
                    point = a[i - 1];

                // only if decreasing seq. minimum
                // count has been met,
                if (dec >= 2)

                    // increase inc by 1
                    inc++;

                else

                    // return -1 as decreasing seq.
                    // min. count must be 2
                    return -1;
            }

            // check if current int is equal
            // to previous int, if so,
            else if (a[i] == a[i - 1])
                return -1;
        }

        // check if inc >= 2 and dec >= 2
        // return point
        if (inc >= 2 && dec >= 2)
            return point;

        // otherwise return -1
        else
            return -1;
    }

    // Driver code
    public static void main(String args[])
    {
          int arr[] = { 3, 2, 1, 2 };
            int n = arr.length ;

            int ele = findElement(arr, n);

            if (ele == -1)
                 System.out.println("No such element exist");
            else
                System.out.println(ele);

    }
    // This Code is contributed by ANKITRAI1
}

```

## 计算机编程语言

```
# Python implementation of above approach
def findElement(a, n):

    # set increasing sequence counter to 1
    inc = 1

    # set decreasing sequence counter to 1
    dec = 1

    # for loop counter from 1 to last
    # index of list [len(array)-1]
    for i in range(1, n):

        # check if current int is smaller than previous int
        if(a[i] < a[i-1]):

            # if inc is 1, i.e., increasing seq. never started,
            if inc == 1:

                # increase dec by 1
                dec = dec + 1
            else:

                # return -1 since if increasing seq. has started,
                # there cannot be a decreasing seq. in a valley
                return -1

        # check if current int is greater than previous int
        elif(a[i] > a[i-1]):

            # if inc is 1, i.e., increasing seq.
            # starting for first time,
            if inc == 1:

                # store a[i-1] in point
                point = a[i-1]

            # only if decreasing seq. minimum count has been met,
            if dec >= 2:
                # increase inc by 1
                inc = inc + 1
            else:

                # return -1 as decreasing seq. min. count must be 2
                return -1

        # check if current int is equal to previous int, if so,
        elif(a[i] == a[i-1]):

            # return false as valley is always
            # strictly increasing / decreasing
            return -1

    # check if inc >= 2 and dec >= 2,
    if(inc >= 2 and dec >= 2):

        # return point
        return point
    else:

        # otherwise return -1
        return -1

a = [2, 1, 2]
n = len(a)
ele = findElement(a, n)
if ( ele == -1 ):
    print("No such element exist")
else:
    print(ele)
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

// Function to check such sequence
static int findElement(int []a, int n)
{

    // set increasing/decreasing
    // sequence counter to 1
    int inc = 1, dec = 1, point = 0;

    // for loop counter from 1 to
    // last index of list
    for (int i = 1; i < n; i++)
    {

        // check if current int is
        // smaller than previous int
        if (a[i] < a[i - 1])
        {

            // if inc is 1, i.e., increasing
            // seq. never started
            if (inc == 1)
                // increase dec by 1
                dec++;

            else
                return -1;
        }

        // check if current int is greater
        // than previous int
        else if (a[i] > a[i - 1])
        {

            // if inc is 1, i.e., increasing
            // seq. starting for first time,
            if (inc == 1)

                // store a[i-1] in point
                point = a[i - 1];

            // only if decreasing seq.
            // minimum count has been met,
            if (dec >= 2)

                // increase inc by 1
                inc++;

            else

                // return -1 as decreasing 
                // seq. min. count must be 2
                return -1;
        }

        // check if current int is equal
        // to previous int, if so,
        else if (a[i] == a[i - 1])
            return -1;
    }

    // check if inc >= 2 and
    // dec >= 2, return point
    if (inc >= 2 && dec >= 2)
        return point;

    // otherwise return -1
    else
        return -1;
}

// Driver code
public static void Main()
{
    int []arr = { 3, 2, 1, 2 };
    int n = arr.Length ;

    int ele = findElement(arr, n);

    if (ele == -1)
        Console.WriteLine("No such element exist");
    else
        Console.WriteLine(ele);

}
}

// This code is contributed by Shashank
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Function to check such sequence
function findElement(&$a, $n)
{

    // set increasing/decreasing
    // sequence counter to 1
    $inc = 1;
    $dec = 1;

    // for loop counter from 1
    // to last index of list
    for ($i = 1; $i < $n; $i++)
    {

        // check if current int is
        // smaller than previous int
        if ($a[$i] < $a[$i - 1])
        {

            // if inc is 1, i.e., increasing
            // seq. never started
            if ($inc == 1)

                // increase dec by 1
                $dec++;

            else
                return -1;
        }

        // check if current int is greater
        // than previous int
        else if ($a[$i] > $a[$i - 1])
        {

            // if inc is 1, i.e., increasing
            // seq. starting for first time,
            if ($inc == 1)

                // store a[i-1] in point
                $point = $a[$i - 1];

            // only if decreasing seq.
            // minimum count has been met,
            if ($dec >= 2)

                // increase inc by 1
                $inc++;

            else

                // return -1 as decreasing
                // seq. min. count must be 2
                return -1;
        }

        // check if current int is equal
        // to previous int, if so,
        else if ($a[$i] == $a[$i - 1])
            return -1;
    }

    // check if inc >= 2 and
    // dec >= 2, return point
    if ($inc >= 2 && $dec >= 2)
        return $point;

    // otherwise return -1
    else
        return -1;
}

// Driver code
$arr = array(3, 2, 1, 2);
$n = sizeof($arr);

$ele = findElement($arr, $n);

if ($ele == -1)
    echo "No such element exist";
else
    echo $ele;

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>
// Java Script implementation of above approach

    // Function to check such sequence
    function findElement(a,n)
    {

        // set increasing/decreasing sequence counter to 1
        let inc = 1, dec = 1, point = 0;

        // for loop counter from 1 to last index of list
        for (let i = 1; i < n; i++) {

            // check if current int is
            // smaller than previous int
            if (a[i] < a[i - 1]) {

                // if inc is 1, i.e., increasing
                // seq. never started
                if (inc == 1)
                    // increase dec by 1
                    dec++;

                else
                    return -1;
            }

            // check if current int is greater than previous int
            else if (a[i] > a[i - 1]) {

                // if inc is 1, i.e., increasing seq.
                // starting for first time,
                if (inc == 1)

                    // store a[i-1] in point
                    point = a[i - 1];

                // only if decreasing seq. minimum
                // count has been met,
                if (dec >= 2)

                    // increase inc by 1
                    inc++;

                else

                    // return -1 as decreasing seq.
                    // min. count must be 2
                    return -1;
            }

            // check if current int is equal
            // to previous int, if so,
            else if (a[i] == a[i - 1])
                return -1;
        }

        // check if inc >= 2 and dec >= 2
        // return point
        if (inc >= 2 && dec >= 2)
            return point;

        // otherwise return -1
        else
            return -1;
    }

    // Driver code

        let arr = [3, 2, 1, 2 ];
            let n = arr.length ;

            let ele = findElement(arr, n);

            if (ele == -1)
                document.write("No such element exist");
            else
                document.write(ele);

// This code is contributed by sravan kumar Gottumukkala
</script>
```

**Output:** 

```
1
```