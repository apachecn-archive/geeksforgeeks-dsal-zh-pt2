# 不重复分配所有球

> 原文:[https://www . geesforgeks . org/distribution-all-balls-not-repeat/](https://www.geeksforgeeks.org/distributing-all-balls-without-repetition/)

给定 N 个球。为了方便起见，我们将每个球的颜色表示为——小写字母。我们必须在 K 人中分发 N 个球。如果他们得到两个颜色相同的球，他们会很沮丧。我们可以给人们任何数量的球，即使他们没有得到任何球，他们也不会感到不安，但是，我们必须分发所有的球，这样没有人会感到不安——如果可能，打印“是”，否则打印“否”。

**示例:**

```
Input : 4 2 // value of N and K
        aabb // colors of given balls
Output : YES
We can give 1st and 3rd ball to the first person,
and 2nd and 4th to the second.

Input : 6 3 // value of N and K
        aacaab // colors of given balls
Output : NO
We need to give all balls of color a, but one 
ball will stay, that's why answer is NO 
```

方法将非常简单。我们将创建一个计数数组来记录出现的每种颜色的计数，然后我们将检查是否有任何颜色的出现超过了我们的人数。如果发生这种情况，我们将打印“否”或“是”。

下面给出了上述思想的实现。

## C++

```
// CPP program to find if its possible to
// distribute balls without repitiion
#include <bits/stdc++.h>
using namespace std;

const int MAX_CHAR = 26;

// function to find if its possible to
// distribute balls or not
bool distributingBalls(int k, int n, string str)
{  
    // count array to count how many times
    // each color has occurred
    int a[MAX_CHAR] = {0};
    for (int i = 0; i < n; i++){

        // increasing count of each color
        // every time it appears
        a[str[i] - 'a']++; 
    }

    for (int i = 0; i < MAX_CHAR; i++)  

        // to check if any color appears
        // more than K times if it does
        // we will print NO
        if (a[i] > k)
          return false;

    return true;
}

// Driver code
int main()
{
    long long int n = 6, k = 3;
    string str = "aacaab";

    if (distributingBalls(k, n, str))
        cout << "YES";
    else
        cout << "NO";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find if its possible
// to distribute balls without repitiio
import java.io.*;

public class GFG {

    static int MAX_CHAR = 26;

    // function to find if its possible
    // to distribute balls or not
    static boolean distributingBalls(long k,
                         long n, String str)
    {

        // count array to count how many
        // times each color has occurred
        int []a = new int[MAX_CHAR];

        for (int i = 0; i < n; i++)
        {

            // increasing count of each
            // color every time it appears
            a[str.charAt(i) - 'a']++;
        }

        for (int i = 0; i < MAX_CHAR; i++)

            // to check if any color appears
            // more than K times if it does
            // we will print NO
            if (a[i] > k)
                return false;

        return true;
    }

    // Driver code
    static public void main (String[] args)
    {
        long n = 6, k = 3;
        String str = "aacaab";

        if (distributingBalls(k, n, str))
            System.out.println("YES");
        else
            System.out.println("NO");
    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python3 program to find if its possible to
# distribute balls without repitiion

MAX_CHAR = 26

# function to find if its possible to
# distribute balls or not
def distributingBalls(k, n, string) :

    # count array to count how many times
    # each color has occurred
    a = [0] * MAX_CHAR

    for i in range(n) :
        # increasing count of each color
        # every time it appears
        a[ord(string[i]) - ord('a')] += 1

    for i in range(MAX_CHAR) :
        # to check if any color appears
        # more than K times if it does
        # we will print NO
        if (a[i] > k) :
            return False

    return True

# Driver code
if __name__ == "__main__" :

    n, k = 6, 3
    string = "aacaab"

    if (distributingBalls(k, n, string)) :
        print("YES")
    else :
        print("NO")

# This code is contributed by Ryuga
```

## C#

```
// C# program to find if its possible to
// distribute balls without repitiion
using System;

public class GFG {

    static int MAX_CHAR = 26;

    // function to find if its possible
    // to distribute balls or not
    static bool distributingBalls(long k,
                       long n, string str)
    {

        // count array to count how many
        // times each color has occurred
        int []a = new int[MAX_CHAR];

        for (int i = 0; i < n; i++)
        {

            // increasing count of each
            // color every time it appears
            a[str[i] - 'a']++;
        }

        for (int i = 0; i < MAX_CHAR; i++)

            // to check if any color
            // appears more than K
            // times if it does we
            // will print NO
            if (a[i] > k)
                return false;

        return true;
    }

    // Driver code
    static public void Main ()
    {
        long n = 6, k = 3;
        string str = "aacaab";

        if (distributingBalls(k, n, str))
            Console.WriteLine("YES");
        else
            Console.WriteLine("NO");
    }
}

// This code is contributed by vt_m.
```

## java 描述语言

```
<script>
    // Javascript program to find if its possible to
    // distribute balls without repitiion

    let MAX_CHAR = 26;

    // function to find if its possible
    // to distribute balls or not
    function distributingBalls(k, n, str)
    {

        // count array to count how many
        // times each color has occurred
        let a = new Array(MAX_CHAR);
        a.fill(0);

        for (let i = 0; i < n; i++)
        {

            // increasing count of each
            // color every time it appears
            a[str[i].charCodeAt() - 'a'.charCodeAt()]++;
        }

        for (let i = 0; i < MAX_CHAR; i++)

            // to check if any color
            // appears more than K
            // times if it does we
            // will print NO
            if (a[i] > k)
                return false;

        return true;
    }

    let n = 6, k = 3;
    let str = "aacaab";

    if (distributingBalls(k, n, str))
      document.write("YES");
    else
      document.write("NO");

</script>
```

**输出:**

```
NO
```

本文由**萨尔特哈克·科利**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。