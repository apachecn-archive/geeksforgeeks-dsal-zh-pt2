# 制作 k 号

的所有组合

> 原文:[https://www.geeksforgeeks.org/make-combinations-size-k/](https://www.geeksforgeeks.org/make-combinations-size-k/)

给定两个数字 n 和 k，你必须从 1…n 中找出 k 个数字的所有可能组合。示例:

```
Input : n = 4 
        k = 2
Output : 1 2 
         1 3 
         1 4 
         2 3 
         2 4 
         3 4 

Input : n = 5 
        k = 3
Output : 1 2 3 
         1 2 4 
         1 2 5 
         1 3 4 
         1 3 5 
         1 4 5 
         2 3 4 
         2 3 5 
         2 4 5 
         3 4 5 
```

我们已经在下面的帖子中讨论了一种方法。
[打印给定大小为 n 的数组中 r 元素的所有可能组合](https://www.geeksforgeeks.org/print-all-possible-combinations-of-r-elements-in-a-given-array-of-size-n/)
在这种情况下，我们使用基于 [DFS](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 的方法。我们要从 1 到 n 的所有数字，我们首先推 tmp_vector 中从 1 到 k 的所有数字，一旦 k 等于 0，我们就推 tmp_vector 到 ans_vector 的所有数字。之后，我们从 tmp_vector 中移除最后一个元素，并进行所有剩余的组合。

## C++

```
// C++ program to print all combinations of size
// k of elements in set 1..n
#include <bits/stdc++.h>
using namespace std;

void makeCombiUtil(vector<vector<int> >& ans,
    vector<int>& tmp, int n, int left, int k)
{
    // Pushing this vector to a vector of vector
    if (k == 0) {
        ans.push_back(tmp);
        return;
    }

    // i iterates from left to n. First time
    // left will be 1
    for (int i = left; i <= n; ++i)
    {
        tmp.push_back(i);
        makeCombiUtil(ans, tmp, n, i + 1, k - 1);

        // Popping out last inserted element
        // from the vector
        tmp.pop_back();
    }
}

// Prints all combinations of size k of numbers
// from 1 to n.
vector<vector<int> > makeCombi(int n, int k)
{
    vector<vector<int> > ans;
    vector<int> tmp;
    makeCombiUtil(ans, tmp, n, 1, k);
    return ans;
}

// Driver code
int main()
{
    // given number
    int n = 5;
    int k = 3;
    vector<vector<int> > ans = makeCombi(n, k);
    for (int i = 0; i < ans.size(); i++) {
        for (int j = 0; j < ans[i].size(); j++) {
            cout << ans.at(i).at(j) << " ";
        }
        cout << endl;
    }
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print all combinations of size
// k of elements in set 1..n
import java.util.*;
public class Main
{
    static Vector<Vector<Integer>> ans = new Vector<Vector<Integer>>();
    static Vector<Integer> tmp = new Vector<Integer>();

    static void makeCombiUtil(int n, int left, int k)
    {

        // Pushing this vector to a vector of vector
        if (k == 0) {
            ans.add(tmp);
            for(int i = 0; i < tmp.size(); i++)
            {
                System.out.print(tmp.get(i) + " ");
            }
            System.out.println();
            return;
        }

        // i iterates from left to n. First time
        // left will be 1
        for (int i = left; i <= n; ++i)
        {
            tmp.add(i);
            makeCombiUtil(n, i + 1, k - 1);

            // Popping out last inserted element
            // from the vector
            tmp.remove(tmp.size() - 1);
        }
    }

    // Prints all combinations of size k of numbers
    // from 1 to n.
    static Vector<Vector<Integer>> makeCombi(int n, int k)
    {
        makeCombiUtil(n, 1, k);
        return ans;
    }

    public static void main(String[] args)
    {

        // given number
        int n = 5;
        int k = 3;
        ans = makeCombi(n, k);
    }
}

// This code is contributed by suresh07.
```

## 蟒蛇 3

```
# Python3 program to print all combinations of size
# k of elements in set 1..n
ans = []
tmp = []

def makeCombiUtil(n, left, k):
    # Pushing this vector to a vector of vector
    if (k == 0):
        ans.append(tmp)
        for i in range(len(tmp)):
            print(tmp[i], end = " ")
        print()
        return

    # i iterates from left to n. First time
    # left will be 1
    for i in range(left, n + 1):
        tmp.append(i)
        makeCombiUtil(n, i + 1, k - 1)

        # Popping out last inserted element
        # from the vector
        tmp.pop()

# Prints all combinations of size k of numbers
# from 1 to n.
def makeCombi(n, k):
    makeCombiUtil(n, 1, k)
    return ans

# given number
n = 5
k = 3
ans = makeCombi(n, k)

# This code is contributed by divyeshrabadiya07.
```

## C#

```
// C# program to print all combinations of size
// k of elements in set 1..n
using System;
using System.Collections.Generic;
class GFG {

    static List<List<int>> ans = new List<List<int>>();
    static List<int> tmp = new List<int>();

    static void makeCombiUtil(int n, int left, int k)
    {

        // Pushing this vector to a vector of vector
        if (k == 0) {
            ans.Add(tmp);
            for(int i = 0; i < tmp.Count; i++)
            {
                Console.Write(tmp[i] + " ");
            }
            Console.WriteLine();
            return;
        }

        // i iterates from left to n. First time
        // left will be 1
        for (int i = left; i <= n; ++i)
        {
            tmp.Add(i);
            makeCombiUtil(n, i + 1, k - 1);

            // Popping out last inserted element
            // from the vector
            tmp.RemoveAt(tmp.Count - 1);
        }
    }

    // Prints all combinations of size k of numbers
    // from 1 to n.
    static List<List<int>> makeCombi(int n, int k)
    {
        makeCombiUtil(n, 1, k);
        return ans;
    }

  static void Main()
  {

    // given number
    int n = 5;
    int k = 3;
    ans = makeCombi(n, k);
  }
}

// This code is contributed by rameshtravel07.
```

## java 描述语言

```
<script>
    // Javascript program to print all combinations of size
    // k of elements in set 1..n
    let ans = [];
      let tmp = [];

    function makeCombiUtil(n, left, k)
    {
        // Pushing this vector to a vector of vector
        if (k == 0) {
            ans.push(tmp);
            for(let i = 0; i < tmp.length; i++)
            {
                document.write(tmp[i] + " ");
            }
            document.write("</br>");
            return;
        }

        // i iterates from left to n. First time
        // left will be 1
        for (let i = left; i <= n; ++i)
        {
            tmp.push(i);
            makeCombiUtil(n, i + 1, k - 1);

            // Popping out last inserted element
            // from the vector
            tmp.pop();
        }
    }

    // Prints all combinations of size k of numbers
    // from 1 to n.
    function makeCombi(n, k)
    {
        makeCombiUtil(n, 1, k);
        return ans;
    }

    // given number
    let n = 5;
    let k = 3;
    ans = makeCombi(n, k);

// This code is contributed by divyesh072019.
</script>
```

输出:

```
1 2 3 
1 2 4 
1 2 5 
1 3 4 
1 3 5 
1 4 5 
2 3 4 
2 3 5 
2 4 5 
3 4 5 
```

本文由 **Roshni Agarwal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。