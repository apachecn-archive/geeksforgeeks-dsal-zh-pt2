# 找到要用 1 替换的 0 的索引，得到二进制数组中最长的连续 1 序列| Set-2

> 原文:[https://www . geesforgeks . org/find-index-of-0-to-replaced-1-to-get-最长的二进制数组中的连续 1 序列-set-2/](https://www.geeksforgeeks.org/find-index-of-0-to-be-replaced-with-1-to-get-longest-continuous-sequence-of-1s-in-a-binary-array-set-2/)

给定一个由 0 和 1 组成的数组，找到 0 的位置并用 1 替换，得到最长的连续 1 序列。期望时间复杂度为 O(n)，辅助空间为 O(1)。
**例:**

```
Input : arr[] =  {1, 1, 0, 0, 1, 0, 1, 1, 1, 0, 1, 1, 1}
Output : Index 9
Assuming array index starts from 0, replacing 0 with 1 at 
index 9 causes the maximum continuous sequence of 1s.

Input : arr[] =  {1, 1, 1, 1, 0}
Output : Index 4
```

[Recommended : Please try your approach first on IDE and then look at the solution.](https://ide.geeksforgeeks.org)

我们在[之前的帖子](https://www.geeksforgeeks.org/find-index-0-replaced-1-get-longest-continuous-sequence-1s-binary-array/)中已经讨论过这个问题的解决方案。在这篇文章中，讨论了另外两种解决问题的方法。
**方法 1(利用零两边 1 的计数):**想法是在每个零两边计数 1 的数量。所需的索引是零的索引，其周围有最大数量的 1。实施中使用了以下变量:

*   **leftCnt:** 在所考虑的当前元素零的左侧存储 1 的计数。
*   **rightCnt:** 将 1 的计数存储在所考虑的当前元素 0 的右侧。
*   **最大指数:**指数为零，周围有最大数量的 1。
*   **最后一个:**看到的最后一个零元素的索引
*   **maxCnt:** 如果索引 maxInd 处的 0 被 1 替换，则计数为 1。

继续向右递增，直到输入数组中出现一个。让下一个零出现在索引 I 处。检查这个零元素是否是第一个零元素。如果 lastInd 没有任何有效的索引值，则它是第一个零元素。在这种情况下，用 I 更新 lastInd。现在 rightCnt 的值是这个零左侧的零的数量。所以 leftCnt 等于 rightCnt，然后再求出 rightCnt 的值。如果当前零元素不是第一个零，则索引最后一个零附近的 1 的数量由 leftCnt + rightCnt 给出。如果该值小于 maxCnt 当前持有的值，maxCnt 将取值 leftCnt + rightCnt + 1，maxIndex = lastInd。现在，在索引 I 处，rightCnt 将变为 leftCnt，表示零，lastInd 将等于 I。再次找到 rightCnt 的值，将 1 的数量与 maxcnt 进行比较，并相应地更新 maxCnt 和 maxIndex。对数组的每个后续零元素重复此过程。请注意，lastInd 存储零的索引，计算当前的左 Cnt 和右 Cnt。要替换为 1 的所需索引 0 存储在 maxIndex 中。
以下是上述算法的实现。

## C++

```
// C++ program to find index of zero
// to be replaced by one to get longest
// continuous sequence of ones.
#include <bits/stdc++.h>
using namespace std;

// Returns index of 0 to be replaced
// with 1 to get longest continuous
// sequence of 1s. If there is no 0
// in array, then it returns -1.
int maxOnesIndex(bool arr[], int n)
{
    int i = 0;

    // To store count of ones on left
    // side of current element zero
    int leftCnt = 0;

    // To store count of ones on right
    // side of current element zero
    int rightCnt = 0;

    // Index of zero with maximum number
    // of ones around it.
    int maxIndex = -1;

    // Index of last zero element seen
    int lastInd = -1;

    // Count of ones if zero at index
    // maxInd is replaced by one.
    int maxCnt = 0;

    while (i < n) {

        // Keep incrementing count until
        // current element is 1.
        if (arr[i]) {
            rightCnt++;
        }

        else {

            // If current zero element
            // is not first zero element,
            // then count number of ones
            // obtained by replacing zero at
            // index lastInd. Update maxCnt
            // and maxIndex if required.
            if (lastInd != -1) {
                if (rightCnt + leftCnt + 1 > maxCnt) {
                    maxCnt = leftCnt + rightCnt + 1;
                    maxIndex = lastInd;
                }
            }
            lastInd = i;
            leftCnt = rightCnt;
            rightCnt = 0;
        }

        i++;
    }

    // Find number of ones in continuous
    // sequence when last zero element is
    // replaced by one.
    if (lastInd != -1) {
        if (leftCnt + rightCnt + 1 > maxCnt) {
            maxCnt = leftCnt + rightCnt + 1;
            maxIndex = lastInd;
        }
    }

    return maxIndex;
}

// Driver function
int main()
{
    bool arr[] = { 1, 1, 0, 0, 1, 0, 1, 1, 1, 0, 1, 1, 1 };
    // bool arr[] = {1, 1, 1, 1, 0};

    int n = sizeof(arr) / sizeof(arr[0]);
    cout << "Index of 0 to be replaced is "
        << maxOnesIndex(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find index of zero
// to be replaced by one to get longest
// continuous sequence of ones.

class GFG {

// Returns index of 0 to be replaced
// with 1 to get longest continuous
// sequence of 1s. If there is no 0
// in array, then it returns -1.
    static int maxOnesIndex(boolean arr[], int n) {
        int i = 0;

        // To store count of ones on left
        // side of current element zero
        int leftCnt = 0;

        // To store count of ones on right
        // side of current element zero
        int rightCnt = 0;

        // Index of zero with maximum number
        // of ones around it.
        int maxIndex = -1;

        // Index of last zero element seen
        int lastInd = -1;

        // Count of ones if zero at index
        // maxInd is replaced by one.
        int maxCnt = 0;

        while (i < n) {

            // Keep incrementing count until
            // current element is 1.
            if (arr[i]) {
                rightCnt++;
            } else {

                // If current zero element
                // is not first zero element,
                // then count number of ones
                // obtained by replacing zero at
                // index lastInd. Update maxCnt
                // and maxIndex if required.
                if (lastInd != -1) {
                    if (rightCnt + leftCnt + 1 > maxCnt) {
                        maxCnt = leftCnt + rightCnt + 1;
                        maxIndex = lastInd;
                    }
                }
                lastInd = i;
                leftCnt = rightCnt;
                rightCnt = 0;
            }

            i++;
        }

        // Find number of ones in continuous
        // sequence when last zero element is
        // replaced by one.
        if (lastInd != -1) {
            if (leftCnt + rightCnt + 1 > maxCnt) {
                maxCnt = leftCnt + rightCnt + 1;
                maxIndex = lastInd;
            }
        }

        return maxIndex;
    }

    // Driver function
    public static void main(String[] args) {
        boolean arr[] = {true, true, false, false, true,
            false, true, true, true, false, true, true, true,};

        int n = arr.length;
        System.out.println("Index of 0 to be replaced is "
                + maxOnesIndex(arr, n));
    }
}
//This code contribute by Shikha Singh
```

## 蟒蛇 3

```
# Python3 program to find index of zero
# to be replaced by one to get longest
# continuous sequence of ones.

# Returns index of 0 to be replaced
# with 1 to get longest continuous
# sequence of 1s. If there is no 0
# in array, then it returns -1.
def maxOnesIndex(arr, n):

    i = 0

    # To store count of ones on left
    # side of current element zero
    leftCnt = 0

    # To store count of ones on right
    # side of current element zero
    rightCnt = 0

    # Index of zero with maximum number
    # of ones around it.
    maxIndex = -1

    # Index of last zero element seen
    lastInd = -1

    # Count of ones if zero at index
    # maxInd is replaced by one.
    maxCnt = 0

    while i < n:

        # Keep incrementing count until
        # current element is 1.
        if arr[i] == 1:
            rightCnt += 1

        else:
            # If current zero element
            # is not first zero element,
            # then count number of ones
            # obtained by replacing zero at
            # index lastInd. Update maxCnt
            # and maxIndex if required.
            if lastInd != -1:
                if rightCnt + leftCnt + 1 > maxCnt:
                    maxCnt = leftCnt + rightCnt + 1
                    maxIndex = lastInd

            lastInd = i
            leftCnt = rightCnt
            rightCnt = 0

        i += 1

    # Find number of ones in continuous
    # sequence when last zero element is
    # replaced by one.
    if lastInd != -1:
        if leftCnt + rightCnt + 1 > maxCnt:
            maxCnt = leftCnt + rightCnt + 1
            maxIndex = lastInd

    return maxIndex

# Driver code
if __name__ == "__main__":

    arr = [1, 1, 0, 0, 1, 0, 1,
              1, 1, 0, 1, 1, 1]

    n = len(arr)
    print("Index of 0 to be replaced is",
                    maxOnesIndex(arr, n))

# This code is contributed
# by Rituraj Jain
```

## C#

```
// C# program to find index of zero
// to be replaced by one to get longest
// continuous sequence of ones.

using System;

public class GFG{

// Returns index of 0 to be replaced
// with 1 to get longest continuous
// sequence of 1s. If there is no 0
// in array, then it returns -1.
    static int maxOnesIndex(bool []arr, int n) {
        int i = 0;

        // To store count of ones on left
        // side of current element zero
        int leftCnt = 0;

        // To store count of ones on right
        // side of current element zero
        int rightCnt = 0;

        // Index of zero with maximum number
        // of ones around it.
        int maxIndex = -1;

        // Index of last zero element seen
        int lastInd = -1;

        // Count of ones if zero at index
        // maxInd is replaced by one.
        int maxCnt = 0;

        while (i < n) {

            // Keep incrementing count until
            // current element is 1.
            if (arr[i]) {
                rightCnt++;
            } else {

                // If current zero element
                // is not first zero element,
                // then count number of ones
                // obtained by replacing zero at
                // index lastInd. Update maxCnt
                // and maxIndex if required.
                if (lastInd != -1) {
                    if (rightCnt + leftCnt + 1 > maxCnt) {
                        maxCnt = leftCnt + rightCnt + 1;
                        maxIndex = lastInd;
                    }
                }
                lastInd = i;
                leftCnt = rightCnt;
                rightCnt = 0;
            }

            i++;
        }

        // Find number of ones in continuous
        // sequence when last zero element is
        // replaced by one.
        if (lastInd != -1) {
            if (leftCnt + rightCnt + 1 > maxCnt) {
                maxCnt = leftCnt + rightCnt + 1;
                maxIndex = lastInd;
            }
        }

        return maxIndex;
    }

    // Driver function
    static public void Main (){
        bool []arr = {true, true, false, false, true,
            false, true, true, true, false, true, true, true,};

        int n = arr.Length;
        Console.WriteLine("Index of 0 to be replaced is "
                + maxOnesIndex(arr, n));
    }
}
//This code contribute by ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find index of zero
// to be replaced by one to get longest
// continuous sequence of ones.

// Returns index of 0 to be replaced
// with 1 to get longest continuous
// sequence of 1s. If there is no 0
// in array, then it returns -1.
function maxOnesIndex($arr, $n)
{
    $i = 0;

    // To store count of ones on left
    // side of current element zero
    $leftCnt = 0;

    // To store count of ones on right
    // side of current element zero
    $rightCnt = 0;

    // Index of zero with maximum number
    // of ones around it.
    $maxIndex = -1;

    // Index of last zero element seen
    $lastInd = -1;

    // Count of ones if zero at index
    // maxInd is replaced by one.
    $maxCnt = 0;

    while ($i < $n)
    {

        // Keep incrementing count until
        // current element is 1.
        if ($arr[$i])
        {
            $rightCnt++;
        }

        else
        {

            // If current zero element
            // is not first zero element,
            // then count number of ones
            // obtained by replacing zero at
            // index lastInd. Update maxCnt
            // and maxIndex if required.
            if ($lastInd != -1)
            {
                if ($rightCnt + $leftCnt + 1 > $maxCnt)
                {
                    $maxCnt = $leftCnt + $rightCnt + 1;
                    $maxIndex = $lastInd;
                }
            }
            $lastInd = $i;
            $leftCnt = $rightCnt;
            $rightCnt = 0;
        }

        $i++;
    }

    // Find number of ones in continuous
    // sequence when last zero element is
    // replaced by one.
    if ($lastInd != -1)
    {
        if ($leftCnt + $rightCnt + 1 > $maxCnt)
        {
            $maxCnt = $leftCnt + $rightCnt + 1;
            $maxIndex = $lastInd;
        }
    }

    return $maxIndex;
}

// Driver Code
$arr = array(1, 1, 0, 0, 1, 0,
            1, 1, 1, 0, 1, 1, 1);
// bool arr[] = {1, 1, 1, 1, 0};

$n = sizeof($arr);
echo "Index of 0 to be replaced is ".
              maxOnesIndex($arr, $n);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// Javascript program to find index of zero
// to be replaced by one to get longest
// continuous sequence of ones.

// Returns index of 0 to be replaced
// with 1 to get longest continuous
// sequence of 1s. If there is no 0
// in array, then it returns -1.
function maxOnesIndex(arr, n)
{
    var i = 0;

    // To store count of ones on left
    // side of current element zero
    var leftCnt = 0;

    // To store count of ones on right
    // side of current element zero
    var rightCnt = 0;

    // Index of zero with maximum number
    // of ones around it.
    var maxIndex = -1;

    // Index of last zero element seen
    var lastInd = -1;

    // Count of ones if zero at index
    // maxInd is replaced by one.
    var maxCnt = 0;

    while (i < n) {

        // Keep incrementing count until
        // current element is 1.
        if (arr[i]) {
            rightCnt++;
        }

        else {

            // If current zero element
            // is not first zero element,
            // then count number of ones
            // obtained by replacing zero at
            // index lastInd. Update maxCnt
            // and maxIndex if required.
            if (lastInd != -1) {
                if (rightCnt + leftCnt + 1 > maxCnt) {
                    maxCnt = leftCnt + rightCnt + 1;
                    maxIndex = lastInd;
                }
            }
            lastInd = i;
            leftCnt = rightCnt;
            rightCnt = 0;
        }

        i++;
    }

    // Find number of ones in continuous
    // sequence when last zero element is
    // replaced by one.
    if (lastInd != -1) {
        if (leftCnt + rightCnt + 1 > maxCnt) {
            maxCnt = leftCnt + rightCnt + 1;
            maxIndex = lastInd;
        }
    }

    return maxIndex;
}

// Driver function
var arr = [ 1, 1, 0, 0, 1, 0, 1, 1, 1, 0, 1, 1, 1 ];

// bool arr[] = {1, 1, 1, 1, 0};
var n = arr.length;
document.write( "Index of 0 to be replaced is "
    + maxOnesIndex(arr, n));

// This code is contributed by itsok.
</script>
```

**输出:**

```
Index of 0 to be replaced is 9
```

**时间复杂度:** O(n)
**辅助空间:** O(1)
**方法二(使用滑动窗口):**滑动窗口用于查找最长连续序列中通过替换一个零得到的 1 的个数。其思想是不断增加滑动窗口的结束点，直到一个出现在输入数组中。当发现零时，检查它是否是第一个零元素。如果它是第一个零元素，则滑动窗口进一步扩展。如果不是，那就求推拉窗的长度。这个长度是通过替换滑动窗口中的零元素得到的一个数。请注意，该长度给出了通过替换先前的零元素而不是当前的零元素获得的 1 的数量。对于当前零元素，滑动窗口的起点是前一个零元素索引旁边的索引。
以下是上述算法的实现。

## C++

```
// C++ program to find index of zero
// to be replaced by one to get longest
// continuous sequence of ones.
#include <bits/stdc++.h>
using namespace std;

// Returns index of 0 to be replaced
// with 1 to get longest continuous
// sequence of 1s.  If there is no 0
// in array, then it returns -1.
int maxOnesIndex(bool arr[], int n)
{

    // To store starting point of
    // sliding window.
    int start = 0;

    // To store ending point of
    // sliding window.
    int end = 0;

    // Index of zero with maximum number
    // of ones around it.
    int maxIndex = -1;

    // Index of last zero element seen
    int lastInd = -1;

    // Count of ones if zero at index
    // maxInd is replaced by one.
    int maxCnt = 0;

    while (end < n) {

        // Keep increasing ending point
        // of sliding window until one is
        // present in input array.
        while (end < n && arr[end]) {
            end++;
        }

        // If this is not first zero element
        // then number of ones obtained by
        // replacing zero at lastInd is
        // equal to length of window.
        // Compare this with maximum number
        // of ones in a previous window so far.
        if (maxCnt < end - start && lastInd != -1) {
            maxCnt = end - start;
            maxIndex = lastInd;
        }

        // The new starting point of next window
        // is from index position next to last
        // zero which is stored in lastInd.
        start = lastInd + 1;
        lastInd = end;
        end++;
    }

    // For the case when only one zero is
    // present in input array and is at
    // last position.
    if (maxCnt < end - start && lastInd != -1) {
        maxCnt = end - start;
        maxIndex = lastInd;
    }

    return maxIndex;
}

// Driver function
int main()
{
    bool arr[] = { 1, 1, 0, 0, 1, 0, 1, 1, 1, 0, 1, 1, 1 };
    // bool arr[] = {1, 1, 1, 1, 0};

    int n = sizeof(arr) / sizeof(arr[0]);
    cout << "Index of 0 to be replaced is "
         << maxOnesIndex(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find index of zero
// to be replaced by one to get longest
// continuous sequence of ones.

public class GFG {

// Returns index of 0 to be replaced
// with 1 to get longest continuous
// sequence of 1s. If there is no 0
// in array, then it returns -1.
    static int maxOnesIndex(boolean arr[], int n) {

        // To store starting point of
        // sliding window.
        int start = 0;

        // To store ending point of
        // sliding window.
        int end = 0;

        // Index of zero with maximum number
        // of ones around it.
        int maxIndex = -1;

        // Index of last zero element seen
        int lastInd = -1;

        // Count of ones if zero at index
        // maxInd is replaced by one.
        int maxCnt = 0;

        while (end < n) {

            // Keep increasing ending point
            // of sliding window until one is
            // present in input array.
            while (end < n && arr[end]) {
                end++;
            }

            // If this is not first zero element
            // then number of ones obtained by
            // replacing zero at lastInd is
            // equal to length of window.
            // Compare this with maximum number
            // of ones in a previous window so far.
            if (maxCnt < end - start && lastInd != -1) {
                maxCnt = end - start;
                maxIndex = lastInd;
            }

            // The new starting point of next window
            // is from index position next to last
            // zero which is stored in lastInd.
            start = lastInd + 1;
            lastInd = end;
            end++;
        }

        // For the case when only one zero is
        // present in input array and is at
        // last position.
        if (maxCnt < end - start && lastInd != -1) {
            maxCnt = end - start;
            maxIndex = lastInd;
        }

        return maxIndex;
    }

    // Driver function
    static public void main(String[] args) {
        boolean arr[] = {true, true, false, false, true,
            false, true, true, true, false, true, true, true,};

        // bool arr[] = {1, 1, 1, 1, 0};
        int n = arr.length;
        System.out.println("Index of 0 to be replaced is "
                + maxOnesIndex(arr, n));
    }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to find index of zero
# to be replaced by one to get longest
# continuous sequence of ones.

# Returns index of 0 to be replaced
# with 1 to get longest continuous
# sequence of 1s. If there is no 0
# in array, then it returns -1.
def maxOnesIndex(arr, n):

    # To store starting point of
    # sliding window.
    start = 0

    # To store ending point of
    # sliding window.
    end = 0

    # Index of zero with maximum
    # number of ones around it.
    maxIndex = -1

    # Index of last zero element seen
    lastInd = -1

    # Count of ones if zero at index
    # maxInd is replaced by one.
    maxCnt = 0

    while (end < n) :

        # Keep increasing ending point
        # of sliding window until one is
        # present in input array.
        while (end < n and arr[end]) :
            end += 1

        # If this is not first zero element
        # then number of ones obtained by
        # replacing zero at lastInd is
        # equal to length of window.
        #Compare this with maximum number
        # of ones in a previous window so far.
        if (maxCnt < end - start and lastInd != -1) :
            maxCnt = end - start
            maxIndex = lastInd

        # The new starting point of next window
        # is from index position next to last
        # zero which is stored in lastInd.
        start = lastInd + 1
        lastInd = end
        end += 1

    # For the case when only one zero is
    # present in input array and is at
    # last position.
    if (maxCnt < end - start and lastInd != -1) :
        maxCnt = end - start
        maxIndex = lastInd

    return maxIndex

# Driver Code
if __name__ == "__main__":

    arr = [1, 1, 0, 0, 1, 0, 1,
              1, 1, 0, 1, 1, 1 ]
    # arr= [1, 1, 1, 1, 0]

    n = len(arr)
    print ("Index of 0 to be replaced is ",
                      maxOnesIndex(arr, n))

# This code is contributed by ChitraNayal
```

## C#

```
using System;

// c# program to find index of zero 
// to be replaced by one to get longest 
// continuous sequence of ones.

public class GFG
{

// Returns index of 0 to be replaced 
// with 1 to get longest continuous 
// sequence of 1s. If there is no 0 
// in array, then it returns -1. 
    public static int maxOnesIndex(bool[] arr, int n)
    {

        // To store starting point of 
        // sliding window. 
        int start = 0;

        // To store ending point of 
        // sliding window. 
        int end = 0;

        // Index of zero with maximum number 
        // of ones around it. 
        int maxIndex = -1;

        // Index of last zero element seen 
        int lastInd = -1;

        // Count of ones if zero at index 
        // maxInd is replaced by one. 
        int maxCnt = 0;

        while (end < n)
        {

            // Keep increasing ending point 
            // of sliding window until one is 
            // present in input array. 
            while (end < n && arr[end])
            {
                end++;
            }

            // If this is not first zero element 
            // then number of ones obtained by 
            // replacing zero at lastInd is 
            // equal to length of window. 
            // Compare this with maximum number 
            // of ones in a previous window so far. 
            if (maxCnt < end - start && lastInd != -1)
            {
                maxCnt = end - start;
                maxIndex = lastInd;
            }

            // The new starting point of next window 
            // is from index position next to last 
            // zero which is stored in lastInd. 
            start = lastInd + 1;
            lastInd = end;
            end++;
        }

        // For the case when only one zero is 
        // present in input array and is at 
        // last position. 
        if (maxCnt < end - start && lastInd != -1)
        {
            maxCnt = end - start;
            maxIndex = lastInd;
        }

        return maxIndex;
    }

        // Driver function 
    public static void Main(string[] args)
    {
        bool[] arr = new bool[] {true, true, false, false, true, false, true, true, true, false, true, true, true};

        // bool arr[] = {1, 1, 1, 1, 0}; 
        int n = arr.Length;
        Console.WriteLine("Index of 0 to be replaced is " + maxOnesIndex(arr, n));
    }
}

// This code is contributed by Shrikant13
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find index of zero
// to be replaced by one to get longest
// continuous sequence of ones.

// Returns index of 0 to be replaced
// with 1 to get longest continuous
// sequence of 1s. If there is no 0
// in array, then it returns -1.
function maxOnesIndex($arr, $n)
{

    // To store starting point of
    // sliding window.
    $start = 0;

    // To store ending point of
    // sliding window.
    $end = 0;

    // Index of zero with maximum
    // number of ones around it.
    $maxIndex = -1;

    // Index of last zero element seen
    $lastInd = -1;

    // Count of ones if zero at index
    // maxInd is replaced by one.
    $maxCnt = 0;

    while ($end < $n)
    {

        // Keep increasing ending point
        // of sliding window until one is
        // present in input array.
        while ($end < $n && $arr[$end])
        {
            $end++;
        }

        // If this is not first zero element
        // then number of ones obtained by
        // replacing zero at lastInd is
        // equal to length of window.
        // Compare this with maximum number
        // of ones in a previous window so far.
        if ($maxCnt < $end - $start &&
                      $lastInd != -1)
        {
            $maxCnt = $end - $start;
            $maxIndex = $lastInd;
        }

        // The new starting point of next window
        // is from index position next to last
        // zero which is stored in lastInd.
        $start = $lastInd + 1;
        $lastInd = $end;
        $end++;
    }

    // For the case when only one zero is
    // present in input array and is at
    // last position.
    if ($maxCnt < $end - $start && $lastInd != -1)
    {
        $maxCnt = $end - $start;
        $maxIndex = $lastInd;
    }

    return $maxIndex;
}

// Driver Code
$arr = array( 1, 1, 0, 0, 1, 0, 1,
              1, 1, 0, 1, 1, 1 );
// bool arr[] = {1, 1, 1, 1, 0};

$n = sizeof($arr);
echo "Index of 0 to be replaced is ",
maxOnesIndex($arr, $n);

// This code is contributed
// by Sach_Code
?>
```

## java 描述语言

```
<script>

// Javascript program to find index of zero
// to be replaced by one to get longest
// continuous sequence of ones.

// Returns index of 0 to be replaced
// with 1 to get longest continuous
// sequence of 1s.  If there is no 0
// in array, then it returns -1.
function maxOnesIndex( arr, n)
{

    // To store starting point of
    // sliding window.
    var start = 0;

    // To store ending point of
    // sliding window.
    var end = 0;

    // Index of zero with maximum number
    // of ones around it.
    var maxIndex = -1;

    // Index of last zero element seen
    var lastInd = -1;

    // Count of ones if zero at index
    // maxInd is replaced by one.
    var maxCnt = 0;

    while (end < n) {

        // Keep increasing ending point
        // of sliding window until one is
        // present in input array.
        while (end < n && arr[end]) {
            end++;
        }

        // If this is not first zero element
        // then number of ones obtained by
        // replacing zero at lastInd is
        // equal to length of window.
        // Compare this with maximum number
        // of ones in a previous window so far.
        if (maxCnt < end - start && lastInd != -1) {
            maxCnt = end - start;
            maxIndex = lastInd;
        }

        // The new starting point of next window
        // is from index position next to last
        // zero which is stored in lastInd.
        start = lastInd + 1;
        lastInd = end;
        end++;
    }

    // For the case when only one zero is
    // present in input array and is at
    // last position.
    if (maxCnt < end - start && lastInd != -1) {
        maxCnt = end - start;
        maxIndex = lastInd;
    }

    return maxIndex;
}

// Driver function
var arr = [ 1, 1, 0, 0, 1, 0, 1, 1, 1, 0, 1, 1, 1 ];
// bool arr[] = {1, 1, 1, 1, 0};
var n = arr.length;
document.write( "Index of 0 to be replaced is "
     + maxOnesIndex(arr, n));

</script>
```

**输出:**

```
Index of 0 to be replaced is 9
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)