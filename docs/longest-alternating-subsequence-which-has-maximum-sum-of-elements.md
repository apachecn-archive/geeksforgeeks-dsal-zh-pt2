# 元素和最大的最长交替子序列

> 原文:[https://www . geeksforgeeks . org/最长交替子序列具有最大元素总和/](https://www.geeksforgeeks.org/longest-alternating-subsequence-which-has-maximum-sum-of-elements/)

给定长度为 **N** 的正负整数列表。任务是选择给定序列中最长的交替子序列(即每个下一个元素的符号与当前元素的符号相反)。在所有这样的子序列中，我们必须选择一个具有最大元素总和的子序列，并显示该总和。

**示例:**

> **输入:**列表= [-2 10 3 -8 -4 -1 5 -2 -3 1]
> **输出:** 11
> **解释:**
> 和最大的最大子序列是长度为 6 的[-2 10 -1 5 -2 1]。
> 
> **输入:**列表=【12 4-5 7-9】
> **输出:** 5
> **解释:**
> 最大和最大的子序列是长度为 4 的【12 -5 7 -9】。

**方法:**可通过以下方法解决

*   为了得到最大长度和最大和的交替子序列，我们将遍历整个列表(列表的长度)-1 次来比较连续元素的符号。
*   在遍历过程中，如果我们得到 1 个以上相同符号的连续元素(exp。1 2 4)，那么我们将把其中最大的元素追加到另一个名为**的大列表**中。所以从 1 2 和 4 开始，我们将把 4 追加到另一个列表中。
*   如果我们有符号相反的连续元素，我们只需将这些元素添加到名为**的大列表**中。
*   最后，名为**大**的列表将具有最长的交替子序列和最大的元素。
*   现在，我们必须从名为**的大型**列表中计算所有元素的总和。

> 举个例子，我们有一个列表[1，2，3，-2，-5，1，-7，-1]。
> 
> 1.  在遍历这个列表长度-1 次时，我们得到了 1，2，3，符号相同，所以我们将把其中最大的一个(即 3)附加到另一个这里命名为 large 的列表中。
>     因此大=[3]
> 2.  现在-2 和-5 有相同的符号，所以我们将把-2 附加到另一个列表中。
>     大=[3，-2]
> 3.  现在，1 和-7 的符号是相反的，所以我们将把 1 附加到大号上。
>     大=[3，-2，1]
> 4.  对于-7，-1 符号是相同的，因此在大的后面加上-1。
>     大=[3，-2，1，-1]
> 5.  计算总和= 3–2+1–1 =**1**

下面是上述方法的实现:

## C++

```
// C++ implementation to find the
// longest alternating subsequence
// which has the maximum sum
#include<bits/stdc++.h>
using namespace std;

int calculateMaxSum(int n, int li[])
{

    // Creating a temporary list ar to
    // every time store same sign element
    // to calculate maximum element from
    // that list ar
    vector<int> ar;

    // Appending 1st element of list li
    // to the ar
    ar.push_back(li[0]);

    // Creating list to store maximum
    // values
    vector<int> large;

    for(int j = 0; j < n - 1; j++)
    {

       // If both number are positive
       // then append (j + 1)th element
       // to temporary list ar
       if(li[j] > 0 and li[j + 1] > 0)
       {
           ar.push_back(li[j + 1]);
       }
       else if(li[j] > 0 and li[j + 1] < 0)
       {

           // If opposite elements found
           // then append maximum element
           // to large list
           large.push_back(*max_element(ar.begin(),
                                        ar.end()));

           // Empty ar list to re-append
           // next elements
           ar.clear();
           ar.push_back(li[j + 1]);
       }
       else if(li[j] < 0 and li[j + 1] > 0)
       {

           // If opposite elements found
           // then append maximum element
           // to large list
           large.push_back(*max_element(ar.begin(),
                                        ar.end()));

           // Empty ar list to re-append
           // next elements
           ar.clear();
           ar.push_back(li[j + 1]);
       }
       else
       {
           // If both number are negative
           // then append (j + 1)th element
           // to temporary list ar
           ar.push_back(li[j + 1]);
       }
    }

    // The final Maximum element in ar list
    // also needs to be appended to large list
    large.push_back(*max_element(ar.begin(),
                                 ar.end()));

    // Returning the sum of all elements
    // from largest elements list with
    // largest alternating subsequence size
    int sum = 0;
    for(int i = 0; i < large.size(); i++)
       sum += large[i];
    return sum;
}

// Driver code
int main()
{
    int list[] = { -2, 8, 3, 8, -4, -15,
                    5, -2, -3, 1 };
    int N = sizeof(list) / sizeof(list[0]);

    cout << (calculateMaxSum(N, list));
}

// This code is contributed by Bhupendra_Singh
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// longest alternating subsequence
// which has the maximum sum
import java.util.*;

class GFG{

static int calculateMaxSum(int n, int li[])
{

    // Creating a temporary list ar to
    // every time store same sign element
    // to calculate maximum element from
    // that list ar
    Vector<Integer> ar = new Vector<>();

    // Appending 1st element of list li
    // to the ar
    ar.add(li[0]);

    // Creating list to store maximum
    // values
    Vector<Integer> large = new Vector<>();

    for(int j = 0; j < n - 1; j++)
    {

        // If both number are positive
        // then append (j + 1)th element
        // to temporary list ar
        if(li[j] > 0 && li[j + 1] > 0)
        {
            ar.add(li[j + 1]);
        }
        else if(li[j] > 0 && li[j + 1] < 0)
        {

            // If opposite elements found
            // then append maximum element
            // to large list
            large.add(Collections.max(ar));

            // Empty ar list to re-append
            // next elements
            ar.clear();
            ar.add(li[j + 1]);
        }
        else if(li[j] < 0 && li[j + 1] > 0)
        {

            // If opposite elements found
            // then append maximum element
            // to large list
            large.add(Collections.max(ar));

            // Empty ar list to re-append
            // next elements
            ar.clear();
            ar.add(li[j + 1]);
        }
        else
        {
            // If both number are negative
            // then append (j + 1)th element
            // to temporary list ar
            ar.add(li[j + 1]);
        }
    }

    // The final Maximum element in ar list
    // also needs to be appended to large list
    large.add(Collections.max(ar));

    // Returning the sum of all elements
    // from largest elements list with
    // largest alternating subsequence size
    int sum = 0;
    for(int i = 0; i < large.size(); i++)
        sum += (int)large.get(i);

    return sum;
}

// Driver code
public static void main(String args[])
{
    int list[] = { -2, 8, 3, 8, -4, -15,
                    5, -2, -3, 1 };
    int N = (list.length);

    System.out.print(calculateMaxSum(N, list));
}
}

// This code is contributed by Stream_Cipher
```

## 蟒蛇 3

```
# Python3 implementation to find the
# longest alternating subsequence
# which has the maximum sum

def calculateMaxSum(n, li):
    # Creating a temporary list ar to every
    # time store same sign element to
    # calculate maximum element from
    # that list ar
    ar =[]

    # Appending 1st element of list li
    # to the ar
    ar.append(li[0])

    # Creating list to store maximum
    # values
    large =[]

    for j in range(0, n-1):

        # If both number are positive
        # then append (j + 1)th element
        # to temporary list ar
        if(li[j]>0 and li[j + 1]>0):
            ar.append(li[j + 1])
        elif(li[j]>0 and li[j + 1]<0):

            # If opposite elements found
            # then append maximum element
            # to large list
            large.append(max(ar))

            # Empty ar list to re-append
            # next elements 
            ar =[]
            ar.append(li[j + 1])
        elif(li[j]<0 and li[j + 1]>0):

            # If opposite elements found
            # then append maximum element
            # to large list
            large.append(max(ar))

            # Empty ar list to re-append
            # next elements
            ar =[]
            ar.append(li[j + 1])
        else:
            # If both number are negative
            # then append (j + 1)th element
            # to temporary list ar
            ar.append(li[j + 1])

    # The final Maximum element in ar list
    # also needs to be appended to large list
    large.append(max(ar))

    # returning the sum of all elements
    # from largest elements list with
    # largest alternating subsequence size
    return sum(large)

# Driver code
list =[-2, 8, 3, 8, -4, -15, 5, -2, -3, 1]
N = len(list)

print(calculateMaxSum(N, list))
```

## C#

```
// C# implementation to find the
// longest alternating subsequence
// which has the maximum sum
using System;
using System.Collections.Generic;

class GFG{

static int find_max(List<int> ar)
{
    int mx = -1000000;
    foreach(var i in ar)
    {
        if(i > mx)
           mx = i;
    }
    return mx;
}

static int calculateMaxSum(int n, int []li)
{

    // Creating a temporary list ar to
    // every time store same sign element
    // to calculate maximum element from
    // that list ar
    List<int> ar = new List<int>();

    // Appending 1st element of list li
    // to the ar
    ar.Add(li[0]);

    // Creating list to store maximum
    // values
    List<int> large = new List<int>();

    for(int j = 0; j < n - 1; j++)
    {

        // If both number are positive
        // then append (j + 1)th element
        // to temporary list ar
        if(li[j] > 0 && li[j + 1] > 0)
        {
            ar.Add(li[j + 1]);
        }
        else if(li[j] > 0 && li[j + 1] < 0)
        {

            // If opposite elements found
            // then append maximum element
            // to large list
            large.Add(find_max(ar));

            // Empty ar list to re-append
            // next elements
            ar.Clear();
            ar.Add(li[j + 1]);
        }
        else if(li[j] < 0 && li[j + 1] > 0)
        {

            // If opposite elements found
            // then append maximum element
            // to large list
            large.Add(find_max(ar));

            // Empty ar list to re-append
            // next elements
            ar.Clear();
            ar.Add(li[j + 1]);
        }
        else
        {

            // If both number are negative
            // then append (j + 1)th element
            // to temporary list ar
            ar.Add(li[j + 1]);
        }
    }

    // The final Maximum element in ar list
    // also needs to be appended to large list
    large.Add(find_max(ar));

    // Returning the sum of all elements
    // from largest elements list with
    // largest alternating subsequence size
    int sum = 0;
    foreach(var i in large)
    {
        sum += i;
    }
    return sum;
}

// Driver code
public static void Main()
{
    int []list = { -2, 8, 3, 8, -4, -15,
                    5, -2, -3, 1 };
    int N = (list.Length);

    Console.WriteLine(calculateMaxSum(N, list));
}
}

// This code is contributed by Stream_Cipher   
```

## java 描述语言

```
<script>
    // Javascript implementation to find the
    // longest alternating subsequence
    // which has the maximum sum

    function find_max(ar)
    {
        let mx = -1000000;
        for(let i = 0; i < ar.length; i++)
        {
            if(ar[i] > mx)
               mx = ar[i];
        }
        return mx;
    }

    function calculateMaxSum(n, li)
    {

        // Creating a temporary list ar to
        // every time store same sign element
        // to calculate maximum element from
        // that list ar
        let ar = [];

        // Appending 1st element of list li
        // to the ar
        ar.push(li[0]);

        // Creating list to store maximum
        // values
        let large = [];

        for(let j = 0; j < n - 1; j++)
        {

            // If both number are positive
            // then append (j + 1)th element
            // to temporary list ar
            if(li[j] > 0 && li[j + 1] > 0)
            {
                ar.push(li[j + 1]);
            }
            else if(li[j] > 0 && li[j + 1] < 0)
            {

                // If opposite elements found
                // then append maximum element
                // to large list
                large.push(find_max(ar));

                // Empty ar list to re-append
                // next elements
                ar = [];
                ar.push(li[j + 1]);
            }
            else if(li[j] < 0 && li[j + 1] > 0)
            {

                // If opposite elements found
                // then append maximum element
                // to large list
                large.push(find_max(ar));

                // Empty ar list to re-append
                // next elements
                ar = [];
                ar.push(li[j + 1]);
            }
            else
            {

                // If both number are negative
                // then append (j + 1)th element
                // to temporary list ar
                ar.push(li[j + 1]);
            }
        }

        // The final Maximum element in ar list
        // also needs to be appended to large list
        large.push(find_max(ar));

        // Returning the sum of all elements
        // from largest elements list with
        // largest alternating subsequence size
        let sum = 0;
        for(let i = 0; i < large.length; i++)
        {
            sum += large[i];
        }
        return sum;
    }

    let list = [ -2, 8, 3, 8, -4, -15, 5, -2, -3, 1 ];
    let N = (list.length);

    document.write(calculateMaxSum(N, list));

</script>
```

**Output:** 

```
6
```

**时间复杂度:** O(N)