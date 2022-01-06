# 通过移除最小元素

使两个集合不相交

> 原文:[https://www . geesforgeks . org/make-two-set-distanced-remove-minimum-elements/](https://www.geeksforgeeks.org/make-two-sets-disjoint-removing-minimum-elements/)

给定两个整数集作为大小为 m 和 n 的两个数组。找出应该从集合中移除的最小数字的计数，以便两个集合变得不相交或不包含任何公共元素。我们可以从任何集合中移除元素。我们需要找到需要移除的最小元素总数。
**例:**

```
Input : set1[] = {20, 21, 22}
        set2[] = {22, 23, 24, 25}
Output : 1
We need to remove at least 1 element
which is 22 from set1 to make two 
sets disjoint.

Input : set1[] = {20, 21, 22}
        set2[] = {22, 23, 24, 25, 20}
Output : 2

Input : set1[] = {6, 7}
        set2[] = {12, 13, 14, 15}
Output : 0
```

如果我们仔细观察这个问题，我们可以观察到这个问题简化为寻找两个集合的交集。
一个**简单的解决方案**是迭代第一个集合的每个元素，对于每个元素，检查它是否存在于第二个集合中。如果存在，增加要移除的元素的计数。

## C++

```
// C++ simple program to find total elements
// to be removed to make two sets disjoint.
#include<bits/stdc++.h>
using namespace std;

// Function for find minimum elements to be
// removed from both sets so that they become
// disjoint
int makeDisjoint(int set1[], int set2[], int n, int m)
{
    int result = 0;
    for (int i=0; i<n; i++)
    {
        int j;
        for (j=0; j<m; j++)
            if (set1[i] == set2[j])
                break;

        if (j != m)
            result++;
    }

    return result;
}

// Driven code
int main()
{
    int set1[] = {20, 21, 22};
    int set2[] =  {22, 23, 24, 25, 20};
    int n = sizeof(set1)/sizeof(set1[0]);
    int m = sizeof(set2)/sizeof(set2[1]);
    cout << makeDisjoint(set1, set2, n, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java simple program to find
// total elements to be removed
// to make two sets disjoint.
import java.io.*;

public class GFG{

// Function for find minimum elements
// to be removed from both sets
// so that they become disjoint
static int makeDisjoint(int []set1,
                        int []set2,
                        int n,
                        int m)
{
    int result = 0;
    for (int i = 0; i < n; i++)
    {
        int j;
        for (j = 0; j < m; j++)
            if (set1[i] == set2[j])
                break;

        if (j != m)
            result++;
    }

    return result;
}

    // Driver code
    static public void main (String[] args)
    {
    int []set1 = {20, 21, 22};
    int []set2 = {22, 23, 24, 25, 20};
    int n = set1.length;
    int m = set2.length;
    System.out.println(makeDisjoint(set1, set2,
                                    n, m));
    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python 3 simple program to find
# total elements to be removed to
# make two sets disjoint.

# Function for find minimum elements
# to be removed from both sets so that
# they become disjoint
def makeDisjoint(set1, set2, n, m):

    result = 0;
    for i in range (0, n - 1):
        for j in range(0, m - 1):
            if (set1[i] == set2[j]):
                break

        if (j != m):
            result += 1

    return result

# Driver Code
set1 = [20, 21, 22]
set2 = [22, 23, 24, 25, 20]
n = len(set1)
m = len(set2)
print(makeDisjoint(set1, set2, n, m))

# This code is contributed
# by Akanksha Rai
```

## C#

```
// C# simple program to find
// total elements to be removed
// to make two sets disjoint.
using System;

public class GFG{

// Function for find minimum elements
// to be removed from both sets
// so that they become disjoint
static int makeDisjoint(int []set1,
                        int []set2,
                        int n,
                        int m)
{
    int result = 0;
    for (int i = 0; i < n; i++)
    {
        int j;
        for (j = 0; j < m; j++)
            if (set1[i] == set2[j])
                break;

        if (j != m)
            result++;
    }

    return result;
}

    // Driver code
    static public void Main ()
    {
    int []set1 = {20, 21, 22};
    int []set2 = {22, 23, 24, 25, 20};
    int n = set1.Length;
    int m = set2.Length;
    Console.WriteLine(makeDisjoint(set1, set2,
                                   n, m));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP simple program to find
// total elements to be removed
// to make two sets disjoint.

// Function for find minimum
// elements to be removed from
// both sets so that they become disjoint
function makeDisjoint( $set1, $set2, $n, $m)
{
    $result = 0;
    for ( $i = 0; $i < $n; $i++)
    {
        $j;
        for ($j = 0; $j < $m; $j++)
            if ($set1[$i] == $set2[$j])
                break;

        if ($j != $m)
            $result++;
    }

    return $result;
}

// Driven code
$set1 = array(20, 21, 22);
$set2 = array(22, 23, 24, 25, 20);
$n = count($set1);
$m = count($set2);
echo makeDisjoint($set1, $set2, $n, $m);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Javascript simple program to find
// total elements to be removed
// to make two sets disjoint.

    // Function for find minimum elements
    // to be removed from both sets
    // so that they become disjoint
    function makeDisjoint(set1,set2,n,m)
    {
        let result = 0;
        for (let i = 0; i < n; i++)
        {
            let j;
            for (j = 0; j < m; j++)
                if (set1[i] == set2[j])
                    break;

            if (j != m)
                result++;
        }

        return result;
    }

    // Driver code
    let set1=[20, 21, 22];
    let set2=[22, 23, 24, 25, 20];
    let n = set1.length;
    let m = set2.length;
    document.write(makeDisjoint(set1, set2,
                                    n, m));

    // This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
2
```

**时间复杂度:**O(m * n)
T3】辅助空间: O(1)
一个**高效的解决方案**就是使用哈希。我们创建一个空散列，并在其中插入集合 1 的所有项目。现在遍历集合 2，对于每个元素，检查它是否是散列。如果存在，增加要移除的元素的计数。

## C++

```
// C++ efficient program to find total elements
// to be removed to make two sets disjoint.
#include<bits/stdc++.h>
using namespace std;

// Function for find minimum elements to be
// removed from both sets so that they become
// disjoint
int makeDisjoint(int set1[], int set2[], int n, int m)
{
    // Store all elements of first array in a hash
    // table
    unordered_set <int> s;
    for (int i = 0; i < n; i++)
        s.insert(set1[i]);

    // We need to remove all those elements from
    // set2 which are in set1.
    int result = 0;
    for (int i = 0;  i < m; i++)
        if (s.find(set2[i]) != s.end())
            result++;

    return result;
}

// Driver code
int main()
{
    int set1[] = {20, 21, 22};
    int set2[] =  {22, 23, 24, 25, 20};
    int n = sizeof(set1)/sizeof(set1[0]);
    int m = sizeof(set2)/sizeof(set2[1]);
    cout << makeDisjoint(set1, set2, n, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java efficient program to find total elements
// to be removed to make two sets disjoint.
import java.util.*;
class GFG {

// Function for find minimum elements to be
// removed from both sets so that they become
// disjoint
    static int makeDisjoint(int set1[], int set2[], int n, int m) {
        // Store all elements of first array in a hash
        // table
        LinkedHashSet<Integer> s = new LinkedHashSet<Integer>();
        for (int i = 0; i < n; i++) {
            s.add(set1[i]);
        }

        // We need to remove all those elements from
        // set2 which are in set1.
        int result = 0;
        for (int i = 0; i < m; i++) {
            if (s.contains(set2[i])) {
                result++;
            }
        }

        return result;
    }

// Driver code
    public static void main(String[] args) {
        int set1[] = {20, 21, 22};
        int set2[] = {22, 23, 24, 25, 20};
        int n = set1.length;
        int m = set2.length;
        System.out.println(makeDisjoint(set1, set2, n, m));
    }
}
// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python 3 efficient program to find
# total elements to be removed to
# make two sets disjoint.

# Function for find minimum elements
# to be removed from both sets so
# that they become disjoint
def makeDisjoint(set1, set2, n, m):

    # Store all elements of first array
    # in a hash table
    s = []
    for i in range(n):
        s.append(set1[i])

    # We need to remove all those elements
    # from set2 which are in set1.
    result = 0
    for i in range(m):
        if set2[i] in s:
            result += 1

    return result

# Driver code
if __name__ =="__main__":

    set1 = [20, 21, 22]
    set2 = [22, 23, 24, 25, 20]
    n = len(set1)
    m = len(set2)
    print(makeDisjoint(set1, set2, n, m))

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# efficient program to find total elements
// to be removed to make two sets disjoint.
using System;
using System.Collections.Generic;            

class GFG
{

    // Function for find minimum elements to be
    // removed from both sets so that they become
    // disjoint
    static int makeDisjoint(int []set1, int []set2,
                            int n, int m)
    {
        // Store all elements of first array in a hash
        // table
        HashSet<int> s = new HashSet<int>();
        for (int i = 0; i < n; i++)
        {
            s.Add(set1[i]);
        }

        // We need to remove all those elements from
        // set2 which are in set1.
        int result = 0;
        for (int i = 0; i < m; i++)
        {
            if (s.Contains(set2[i]))
            {
                result++;
            }
        }
        return result;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []set1 = {20, 21, 22};
        int []set2 = {22, 23, 24, 25, 20};
        int n = set1.Length;
        int m = set2.Length;
        Console.WriteLine(makeDisjoint(set1, set2, n, m));
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

//  JavaScript program to find total elements
// to be removed to make two sets disjoint.

// Function for find minimum elements to be
// removed from both sets so that they become
// disjoint
    function makeDisjoint(set1, set2, n, m) {
        // Store all elements of first array in a hash
        // table
        let s = new Set();
        for (let i = 0; i < n; i++) {
            s.add(set1[i]);
        }

        // We need to remove all those elements from
        // set2 which are in set1.
        let result = 0;
        for (let i = 0; i < m; i++) {
            if (s.has(set2[i])) {
                result++;
            }
        }

        return result;
    }

    // Driver code

    let set1 = [20, 21, 22];
        let set2 = [22, 23, 24, 25, 20];
        let n = set1.length;
        let m = set2.length;
        document.write(makeDisjoint(set1, set2, n, m));

</script>
```

**输出:**

```
2
```

**时间复杂度:**O(m+n)
T3】辅助空间: O(m)
本文由**smarackchopdar**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。