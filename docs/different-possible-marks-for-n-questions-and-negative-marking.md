# n 道题的不同可能标记和否定标记

> 原文:[https://www . geeksforgeeks . org/不同-可能-n 分-问题-否定-标记/](https://www.geeksforgeeks.org/different-possible-marks-for-n-questions-and-negative-marking/)

给定问题数量为![n  ](img/31d70d7c99878a33c601d487c9b6eb43.png "Rendered by QuickLaTeX.com")，正确答案标记为![p  ](img/c3104404e764ce050ed72b31b498fffc.png "Rendered by QuickLaTeX.com")，错误答案标记为![q  ](img/469590ca2ccc8ec2f3b0ccffa8739a5c.png "Rendered by QuickLaTeX.com")。一个人可以尝试在考试中解决问题，如果答案是对的，可以得到![p  ](img/c3104404e764ce050ed72b31b498fffc.png "Rendered by QuickLaTeX.com")分，如果答案是错的，可以得到![q  ](img/469590ca2ccc8ec2f3b0ccffa8739a5c.png "Rendered by QuickLaTeX.com")分，或者让问题无人问津，可以得到![0  ](img/1957d0c119c059733abddeb117432e40.png "Rendered by QuickLaTeX.com")分。任务是找出一个人在考试中可能得分的所有不同分数的计数。
**举例:**

```
Input: n = 2, p = 1, q = -1
Output: 5
The different possible marks are: -2, -1, 0, 1, 2

Input: n = 4, p = 2, q = -1
Output: 12
```

**方法:**
迭代所有可能的正确解决和未解决的问题。将分数存储在包含不同元素的集合中，记住有正数量的错误解决的问题。
以下是上述办法的实施:

## C++

```
// CPP program to find the count of
// all the different possible marks
// that one can score in the examination
#include<bits/stdc++.h>

using namespace std;

    // Function to return
    // the count of distinct scores
    int scores(int n, int p, int q)
    {
        // Set to store distinct values
        set<int> hset;

        // iterate through all
        // possible pairs of (p, q)
        for (int i = 0; i <= n; i++)
        {
            for (int j = 0; j <= n; j++)
            {

                int correct = i;
                int not_solved = j;
                int incorrect = n - i - j;

                // if there are positive number
                // of incorrectly solved problems
                if (incorrect >= 0)
                    hset.insert(p * correct
                            + q * incorrect);
                else
                    break;
            }
        }

        // return the size of the set
        // containing distinct elements
        return hset.size();
    }

    // Driver code
    int main()
    {

        // Get the number of questions
        int n = 4;

        // Get the marks for correct answer
        int p = 2;

        // Get the marks for incorrect answer
        int q = -1;

        // Get the count and print it
        cout << (scores(n, p, q));
    }

// This code is contributed by
// Surendra_Gangwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the count of
// all the different possible marks
// that one can score in the examination

import java.util.*;

class GFG {

    // Function to return
    // the count of distinct scores
    static int scores(int n, int p, int q)
    {
        // Set to store distinct values
        HashSet<Integer>
            hset = new HashSet<Integer>();

        // iterate through all
        // possible pairs of (p, q)
        for (int i = 0; i <= n; i++) {
            for (int j = 0; j <= n; j++) {

                int correct = i;
                int not_solved = j;
                int incorrect = n - i - j;

                // if there are positive number
                // of incorrectly solved problems
                if (incorrect >= 0)
                    hset.add(p * correct
                             + q * incorrect);
                else
                    break;
            }
        }

        // return the size of the set
        // containing distinct elements
        return hset.size();
    }

    // Driver code
    public static void main(String[] args)
    {

        // Get the number of questions
        int n = 4;

        // Get the marks for correct answer
        int p = 2;

        // Get the marks for incorrect answer
        int q = -1;

        // Get the count and print it
        System.out.println(scores(n, p, q));
    }
}
```

## 蟒蛇 3

```
# Python3 program to find the count of
# all the different possible marks
# that one can score in the examination

# Function to return the count of
# distinct scores
def scores(n, p, q):

    # Set to store distinct values
    hset = set()

    # Iterate through all possible
    # pairs of (p, q)
    for i in range(0, n + 1):
        for j in range(0, n + 1):

            correct = i
            not_solved = j
            incorrect = n - i - j

            # If there are positive number
            # of incorrectly solved problems
            if incorrect >= 0:
                hset.add(p * correct +
                         q * incorrect)
            else:
                break

    # return the size of the set
    # containing distinct elements
    return len(hset)

# Driver code
if __name__ == "__main__":

    # Get the number of questions
    n = 4

    # Get the marks for correct answer
    p = 2

    # Get the marks for incorrect answer
    q = -1

    # Get the count and print it
    print(scores(n, p, q))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to find the count of
// all the different possible marks
// that one can score in the examination
using System;
using System.Collections.Generic;

class GFG
{

    // Function to return
    // the count of distinct scores
    static int scores(int n, int p, int q)
    {
        // Set to store distinct values
        HashSet<int>
            hset = new HashSet<int>();

        // iterate through all
        // possible pairs of (p, q)
        for (int i = 0; i <= n; i++)
        {
            for (int j = 0; j <= n; j++)
            {

                int correct = i;
                int not_solved = j;
                int incorrect = n - i - j;

                // if there are positive number
                // of incorrectly solved problems
                if (incorrect >= 0)
                    hset.Add(p * correct
                            + q * incorrect);
                else
                    break;
            }
        }

        // return the size of the set
        // containing distinct elements
        return hset.Count;
    }

    // Driver code
    public static void Main()
    {

        // Get the number of questions
        int n = 4;

        // Get the marks for correct answer
        int p = 2;

        // Get the marks for incorrect answer
        int q = -1;

        // Get the count and print it
        Console.WriteLine(scores(n, p, q));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// JavaScript program to find the count of
// all the different possible marks
// that one can score in the examination

    // Function to return
    // the count of distinct scores
    function scores(n, p, q)
    {
        // Set to store distinct values
        let hset = new Set();

        // iterate through all
        // possible pairs of (p, q)
        for (let i = 0; i <= n; i++) {
            for (let j = 0; j <= n; j++) {

                let correct = i;
                let not_solved = j;
                let incorrect = n - i - j;

                // if there are positive number
                // of incorrectly solved problems
                if (incorrect >= 0)
                    hset.add(p * correct
                             + q * incorrect);
                else
                    break;
            }
        }

        // return the size of the set
        // containing distinct elements
        return hset.size;
    }

// Driver Code

           // Get the number of questions
        let n = 4;

        // Get the marks for correct answer
        let p = 2;

        // Get the marks for incorrect answer
        let q = -1;

        // Get the count and prlet it
        document.write(scores(n, p, q));

</script>
```

**Output:** 

```
12
```