# 使用最小替换的不同元素的字典最小排列

> 原文:[https://www . geeksforgeeks . org/按字典顺序排列-最小排列-不同元素-使用最小替换/](https://www.geeksforgeeks.org/lexicographically-smallest-permutation-distinct-elements-using-minimum-replacements/)

给定一个由 n 个正整数组成的数组，使得一个整数的每个元素都是从 1 到 n。通过替换数组中最小数量的元素，使得数组的每个元素在整个数组中恰好出现一次，从而找到可以获得的字典排列。首先，打印所需的最小替换数量，然后打印最终的词典式数组。
**例:**

```
Input arr[] = {2, 3, 4, 3, 2}
Output 2
           1 3 4 5 2
Explanation
Replace number '2' at position 1st with number 
'1' and '3' at position 4th with number '5'. 
The array that we obtain is [1, 3, 4, 5, 2]
which is lexicographically smallest among all 
the possible suitable.

Input arr[] = {2, 1, 2, 1, 2}
Output 3
           2 1 3 4 5 
```

**天真的方法**是生成从 1 到 n 的所有排列，并选择最小的一个来呈现最小的替换。这种方法的时间复杂度是 O(n！)这肯定会使大量的 n.
**超时有效的方法**是贪婪地挑选想要的元素。首先初始化 cnt[]数组，它将包含数组中元素出现的频率。对于数组中多次出现的每个元素(a <sub>i</sub> ，由于得到了字典上的最小排列，所以按升序将数字相加。例如，
迭代数组中的所有元素。让当前数组的个数是一个 <sub>i</sub> 。如果 <sub>i</sub> 的计数等于 1，则移动到下一个数组编号。如果 a <sub>i</sub> 的计数大于 1，则仅当**元素<a<sub>I</sub>T21 时，才使用元素**元素**替换数字 a <sub>i</sub> (数组中不出现的最小数字)。同时，减少 cnt[]阵列中 <sub>i</sub> 的数量。
如果 ele > a <sub>i</sub> 那么标记数字 a <sub>i</sub> ，这样我们就可以在下一次迭代中替换它。*这一步这个需要是因为我们需要进行最小的字典式排列*。** 

> 例如，让我们假设 arr[] = {1，5，4，5，3，7，3}
> **在第一次迭代中**“5”在数组中出现两次(索引 1)
> ，因此我们必须将“2”位置的“5”替换为“2”(2<5)。
> 现在更新后的数组= {1，2，4，5，3，7，3}
> **在下一次迭代**中，【3】将被视为在数组中出现了两次
> 。但是这次替换的下一个元素
> 将等于 6，大于 3。因此，访问布尔数组 vis[]中的元素
> 3，并迭代其他元素。
> 现在第 7 <sup>位第</sup>位再次出现“3”，这次用
> 号“6”代替。
> 最终数组是 arr[] = {1，2，4，5，3，7，6}

## C++

```
// C++ program to print lexicographically
// permutation array by replacing minimum
// element of array
#include <bits/stdc++.h>
using namespace std;

// Function to calculate lexicographically permutation
// in array
void lexicoSmallestPermuatation(int arr[], int n)
{
    // Calculate frequency of array elements
    int cnt[n + 1];
    memset(cnt, 0, sizeof(cnt));
    for (int i = 0; i < n; ++i)
        ++cnt[arr[i]];

    int ele = 1, replacement = 0;
    bool vis[n + 1];
    memset(vis, 0, sizeof(vis));
    for (int i = 0; i < n; ++i) {

        // If count of element is 1, no
        // need to replace
        if (cnt[arr[i]] == 1)
            continue;

        // Find the element that has not
        // occurred in array
        while (cnt[ele])
            ++ele;

        // If replacement element is greater
        // than current arr[i] then visit
        // that element for next iteration
        if (ele > arr[i] && !vis[arr[i]])
            vis[arr[i]] = 1;

        else {

            // Decrement count and assign the element
            // to array
            --cnt[arr[i]];
            arr[i] = ele;

            // Increment the replacement count
            ++replacement;

            // Increment element after assigning
            // to the array
            ++ele;
        }
    }

    cout << replacement << "\n";
    for (int i = 0; i < n; ++i)
        cout << arr[i] << " ";
}

// Driver code
int main()
{
    int arr[] = { 2, 3, 4, 3, 2 };
    int sz = sizeof(arr) / sizeof(arr[0]);
    lexicoSmallestPermuatation(arr, sz);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print lexicographically
// permutation array by replacing minimum
// element of array

class GFG {

// Function to calculate lexicographically permutation
// in array
    static void lexicoSmallestPermuatation(int arr[], int n) {
        // Calculate frequency of array elements
        int cnt[] = new int[n + 1];
        for (int i = 0; i < n; ++i) {
            ++cnt[arr[i]];
        }

        int ele = 1, replacement = 0;
        boolean vis[] = new boolean[n + 1];
        for (int i = 0; i < n; ++i) {

            // If count of element is 1, no
            // need to replace
            if (cnt[arr[i]] == 1) {
                continue;
            }

            // Find the element that has not
            // occurred in array
            while (cnt[ele]>0) {
                ++ele;
            }

            // If replacement element is greater
            // than current arr[i] then visit
            // that element for next iteration
            if (ele > arr[i] && !vis[arr[i]]) {
                vis[arr[i]] = true;
            } else {

                // Decrement count and assign the element
                // to array
                --cnt[arr[i]];
                arr[i] = ele;

                // Increment the replacement count
                ++replacement;

                // Increment element after assigning
                // to the array
                ++ele;
            }
        }

        System.out.print(replacement + "\n");
        for (int i = 0; i < n; ++i) {
            System.out.print(arr[i] + " ");
        }
    }

// Driver code
    public static void main(String[] args) {
        int arr[] = {2, 3, 4, 3, 2};
        int sz = arr.length;
        lexicoSmallestPermuatation(arr, sz);

    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program to print lexicographically
# permutation array by replacing minimum
# element of array

# Function to calculate lexicographically
# permutation in array
def lexicoSmallestPermuatation(arr, n):

    # Calculate frequency of array elements
    cnt = [0 for i in range(n + 1)]
    for i in range(n):
        cnt[arr[i]] += 1

    ele = 1
    replacement = 0
    vis = [0 for i in range(n + 1)]
    for i in range(n):

        # If count of element is 1, no
        # need to replace
        if (cnt[arr[i]] == 1):
            continue

        # Find the element that has not
        # occurred in array
        while (cnt[ele]):
            ele += 1

        # If replacement element is greater
        # than current arr[i] then visit
        # that element for next iteration
        if (ele > arr[i] and vis[arr[i]] == 0):
            vis[arr[i]] = 1;

        else:

            # Decrement count and assign
            # the element to array
            cnt[arr[i]] -= 1
            arr[i] = ele

            # Increment the replacement count
            replacement += 1

            # Increment element after assigning
            # to the array
            ele += 1

    print(replacement)
    for i in range(n):
        print(arr[i], end = " ")

# Driver code
if __name__ == '__main__':
    arr = [2, 3, 4, 3, 2]
    sz = len(arr)
    lexicoSmallestPermuatation(arr, sz)

# This code is contributed by
# Shashank_Sharma
```

## C#

```

// C# program to print lexicographically
// permutation array by replacing minimum
// element of array 
using System;
public class GFG {

// Function to calculate lexicographically permutation
// in array
    static void lexicoSmallestPermuatation(int []arr, int n) {
        // Calculate frequency of array elements
        int []cnt= new int[n + 1];
        for (int i = 0; i < n; ++i) {
            ++cnt[arr[i]];
        }

        int ele = 1, replacement = 0;
        bool []vis = new bool[n + 1];
        for (int i = 0; i < n; ++i) {

            // If count of element is 1, no
            // need to replace
            if (cnt[arr[i]] == 1) {
                continue;
            }

            // Find the element that has not
            // occurred in array
            while (cnt[ele]>0) {
                ++ele;
            }

            // If replacement element is greater
            // than current arr[i] then visit
            // that element for next iteration
            if (ele > arr[i] && !vis[arr[i]]) {
                vis[arr[i]] = true;
            } else {

                // Decrement count and assign the element
                // to array
                --cnt[arr[i]];
                arr[i] = ele;

                // Increment the replacement count
                ++replacement;

                // Increment element after assigning
                // to the array
                ++ele;
            }
        }

        Console.Write(replacement + "\n");
        for (int i = 0; i < n; ++i) {
            Console.Write(arr[i] + " ");
        }
    }

// Driver code
    public static void Main() {
        int []arr = {2, 3, 4, 3, 2};
        int sz = arr.Length;
        lexicoSmallestPermuatation(arr, sz);

    }
}

// This code is contributed by Rajput-Ji//
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print lexicographically
// permutation array by replacing minimum
// element of array

// Function to calculate lexicographically
// permutation in array
function lexicoSmallestPermuatation(&$arr, $n)
{
    // Calculate frequency of array elements
    $cnt = array_fill(0, $n + 1, NULL);
    for ($i = 0; $i < $n; ++$i)
        ++$cnt[$arr[$i]];

    $ele = 1;
    $replacement = 0;
    $vis = array_fill(0, $n + 1, NULL);
    for ($i = 0; $i < $n; ++$i)
    {

        // If count of element is 1, no
        // need to replace
        if ($cnt[$arr[$i]] == 1)
            continue;

        // Find the element that has not
        // occurred in array
        while ($cnt[$ele])
            ++$ele;

        // If replacement element is greater
        // than current arr[i] then visit
        // that element for next iteration
        if ($ele > $arr[$i] && !$vis[$arr[$i]])
            $vis[$arr[$i]] = 1;

        else
        {

            // Decrement count and assign the
            // element to array
            --$cnt[$arr[$i]];
            $arr[$i] = $ele;

            // Increment the replacement count
            ++$replacement;

            // Increment element after assigning
            // to the array
            ++$ele;
        }
    }

    echo $replacement. "\n";
    for ($i = 0; $i < $n; ++$i)
        echo $arr[$i] . " ";
}

// Driver code
$arr = array(2, 3, 4, 3, 2 );
$sz = sizeof($arr);
lexicoSmallestPermuatation($arr, $sz);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>

// Javascript program to
// print lexicographically
// permutation array by
// replacing minimum
// element of array

// Function to calculate
// lexicographically permutation
// in array
    function lexicoSmallestPermuatation(arr, n)
    {
        // Calculate frequency of
        // array elements
        let cnt = Array.from({length: n + 1},
                 (_, i) => 0);
        for (let i = 0; i < n; ++i)
        {
            ++cnt[arr[i]];
        }

        let ele = 1, replacement = 0;
        let vis = Array.from({length: n + 1},
                  (_, i) => 0);
        for (let i = 0; i < n; ++i) {

            // If count of element is 1, no
            // need to replace
            if (cnt[arr[i]] == 1) {
                continue;
            }

            // Find the element that has not
            // occurred in array
            while (cnt[ele]>0) {
                ++ele;
            }

            // If replacement element is greater
            // than current arr[i] then visit
            // that element for next iteration
            if (ele > arr[i] && !vis[arr[i]]) {
                vis[arr[i]] = true;
            } else {

                // Decrement count and
                // assign the element
                // to array
                --cnt[arr[i]];
                arr[i] = ele;

                // Increment the
                // replacement count
                ++replacement;

                // Increment element
                // after assigning
                // to the array
                ++ele;
            }
        }

        document.write(replacement + "<br/>");
        for (let i = 0; i < n; ++i) {
            document.write(arr[i] + " ");
        }
    }

// driver program

        let arr = [2, 3, 4, 3, 2];
        let sz = arr.length;
        lexicoSmallestPermuatation(arr, sz);

</script>
```

**输出**

```
2
1 3 4 5 2 
```

**时间复杂度:** O(n)
本文由 [Shubham Bansal](https://www.quora.com/profile/Shubham-Bansal-209) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。