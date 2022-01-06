# 按字典序最小排列的{1，..n}编号和位置不匹配

> 原文:[https://www . geesforgeks . org/按字典顺序排列-最小-排列-1-n-无位置-不匹配/](https://www.geeksforgeeks.org/lexicographically-smallest-permutation-1-n-no-position-not-match/)

给定正整数 n，求{1，2，..n}这样 p <sub>i</sub> ！=即，我不应该在 I 从 1 到 n 变化的第 I 个位置。

**示例:**

```
Input : 5
Output : 2 1 4 5 3
Consider the two permutations that follow
the requirement that position and numbers
should not be same.
p = (2, 1, 4, 5, 3) and q = (2, 4, 1, 5, 3).  
Since p is lexicographically smaller, our 
output is p.

Input  : 6
Output : 2 1 4 3 6 5

```

因为我们需要字典上最小的(1 不能出现在位置 1)，我们把 2 放在第一个位置。2 之后，我们放下一个最小的元素，即 1。在那之后，下一个最小的考虑它不违反我们的圆周率条件！= i.
现在，如果我们的 n 是偶数，我们简单地取两个变量，一个包含我们的偶数计数，一个包含我们的奇数计数，然后我们将它们加入向量中，直到我们到达 n。

但是，如果我们的 n 是奇数，我们做同样的任务，直到我们到达 n-1，因为如果我们加到 n，那么最终我们将得到 p <sub>i</sub> = i。所以当我们到达 n-1 时，我们首先将 n 加到 n-1 位置，然后在 n 位置上，我们将放 n-2。

下面给出了上述程序的实现。

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the permutation
void findPermutation(vector<int> a, int n)
{
    vector<int> res;  

    // Initial numbers to be pushed to result
    int en = 2, on = 1;

    // If n is even
    if (n % 2 == 0) {
        for (int i = 0; i < n; i++) {
            if (i % 2 == 0) {
                res.push_back(en);
                en += 2;
            } else {
                res.push_back(on);
                on += 2;
            }
        }
    }

    // If n is odd
    else {
        for (int i = 0; i < n - 2; i++) {
            if (i % 2 == 0) {
                res.push_back(en);
                en += 2;
            } else {
                res.push_back(on);
                on += 2;
            }
        }
        res.push_back(n);
        res.push_back(n - 2);
    }

    // Print result
    for (int i = 0; i < n; i++)
        cout << res[i] << " ";   
    cout << "\n";
}

// Driver Code
int main()
{
    long long int n = 9;
    findPermutation(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.Vector;

class GFG {

// Function to print the permutation
    static void findPermutation(int n) {
        Vector<Integer> res = new Vector<Integer>();

        // Initial numbers to be pushed to result
        int en = 2, on = 1;

        // If n is even
        if (n % 2 == 0) {
            for (int i = 0; i < n; i++) {
                if (i % 2 == 0) {
                    res.add(en);
                    en += 2;
                } else {
                    res.add(on);
                    on += 2;
                }
            }
        } // If n is odd
        else {
            for (int i = 0; i < n - 2; i++) {
                if (i % 2 == 0) {
                    res.add(en);
                    en += 2;
                } else {
                    res.add(on);
                    on += 2;
                }
            }
            res.add(n);
            res.add(n - 2);
        }

        // Print result
        for (int i = 0; i < n; i++) {
            System.out.print(res.get(i) + " ");
        }
        System.out.println("");
    }

// Driver Code
    public static void main(String[] args) {
        int n = 9;
        findPermutation(n);
    }
}
// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to print the permutation
def findPermutation(n) :

    res = []

    # Initial numbers to be pushed to result
    en, on = 2, 1

    # If n is even
    if (n % 2 == 0) :
        for i in range(n) :
            if (i % 2 == 0) :
                res.append(en)
                en += 2
            else :
                res.append(on)
                on += 2

    # If n is odd
    else :
        for i in range(n-2) :
            if (i % 2 == 0) :
                res.append(en)
                en += 2
            else :
                res.append(on)
                on += 2

        res.append(n)
        res.append(n - 2)

    # Print result
    for i in range(n) :
        print(res[i] ,end = " ")    
    print()

# Driver Code
if __name__ == "__main__" :

    n = 9;
    findPermutation(n)

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the above approach
using System;
using System.Collections;
public class GFG {

// Function to print the permutation
    static void findPermutation(int n) {
        ArrayList res = new ArrayList();

        // Initial numbers to be pushed to result
        int en = 2, on = 1;

        // If n is even
        if (n % 2 == 0) {
            for (int i = 0; i < n; i++) {
                if (i % 2 == 0) {
                    res.Add(en);
                    en += 2;
                } else {
                    res.Add(on);
                    on += 2;
                }
            }
        } // If n is odd
        else {
            for (int i = 0; i < n - 2; i++) {
                if (i % 2 == 0) {
                    res.Add(en);
                    en += 2;
                } else {
                    res.Add(on);
                    on += 2;
                }
            }
            res.Add(n);
            res.Add(n - 2);
        }

        // Print result
        for (int i = 0; i < n; i++) {
            Console.Write(res[i] + " ");
        }
        Console.WriteLine("");
    }

// Driver Code
    public static void Main() {
        int n = 9;
        findPermutation(n);
    }
}
// This code is contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to print the permutation
function findPermutation($n)
{
    $res = array();

    // Initial numbers to be pushed
    // to result
    $en = 2;
    $on = 1;

    // If n is even
    if ($n % 2 == 0)
    {
        for ($i = 0; $i < $n; $i++)
        {
            if (i % 2 == 0)
            {
                array_push($res, $en);
                $en += 2;
            } else
            {
                array_push($res, $on);
                $on += 2;
            }
        }
    }

    // If n is odd
    else
    {
        for ($i = 0; $i < $n - 2; $i++)
        {
            if ($i % 2 == 0)
            {
                array_push($res, $en);
                $en += 2;
            }
            else
            {
                array_push($res, $on);
                $on += 2;
            }
        }
        array_push($res, $n);
        array_push($res, $n - 2);
    }

    // Print result
    for ($i = 0; $i < $n; $i++)
        echo $res[$i] . " ";
    echo "\n";
}

// Driver Code
$n = 9;
findPermutation($n);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to print the permutation
function findPermutation(n)
{
    let res = [];

    // Initial numbers to be pushed to result
    let en = 2, on = 1;

    // If n is even
    if (n % 2 == 0)
    {
        for(let i = 0; i < n; i++)
        {
            if (i % 2 == 0)
            {
                res.push(en);
                en += 2;
            }
            else
            {
                res.push(on);
                on += 2;
            }
        }
    }
    // If n is odd
    else
    {
        for(let i = 0; i < n - 2; i++)
        {
            if (i % 2 == 0)
            {
                res.push(en);
                en += 2;
            }
            else
            {
                res.push(on);
                on += 2;
            }
        }
        res.push(n);
        res.push(n - 2);
    }

    // Print result
    for(let i = 0; i < n; i++)
    {
        document.write(res[i] + " ");
    }
    document.write("");
}

// Driver Code
let n = 9;

findPermutation(n);

// This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
2 1 4 3 6 5 8 9 7
```

**时间复杂度:** O(n)

本文由**萨尔特哈克·科利**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。